# Electron.js: сучасний конспект 2024+

---

## Зміст

-   [Вступ](#вступ)
-   [Що таке Electron.js](#що-таке-electronjs)
-   [Історія та роль Electron.js](#історія-та-роль-electronjs)
-   [Встановлення та старт проекту](#встановлення-та-старт-проекту)
-   [Структура проєкту, основні файли](#структура-проєкту-основні-файли)
-   [Головний процес (Main Process), рендерер (Renderer Process)](#головний-процес-main-process-рендерер-renderer-process)
-   [IPC (Inter-Process Communication), безпека та lifecycle](#ipc-inter-process-communication-безпека-та-lifecycle)
-   [Інтеграція з Node.js, доступ до файлової системи](#інтеграція-з-nodejs-доступ-до-файлової-системи)
-   [Створення вікон, BrowserWindow, конфігурація](#створення-вікон-browserwindow-конфігурація)
-   [Меню, контекстне меню, Tray, глобальні шорткати](#меню-контекстне-меню-tray-глобальні-шорткати)
-   [Робота з нотифікаціями, діалогами, shell, drag&drop](#робота-з-нотифікаціями-діалогами-shell-dragdrop)
-   [Автоматичне оновлення (autoUpdater), деплой, Squirrel, electron-builder](#автоматичне-оновлення-autoupdater-деплой-squirrel-electron-builder)
-   [Поглиблено: підкапотна робота Electron (Chromium, V8, Node.js, security traps, memory, perf)](#поглиблено-підкапотна-робота-electron)
-   [Інтеграція з Frontend-фреймворками (React, Vue, Svelte, Angular)](#інтеграція-з-frontend-фреймворками-react-vue-svelte-angular)
-   [Масштабування, багатовіконність, багатопроцесорність, Worker Threads](#масштабування-багатовіконність-багатопроцесорність-worker-threads)
-   [Тестування: Spectron, Playwright, Jest, Mocha, Vitest](#тестування-spectron-playwright-jest-mocha-vitest)
-   [Best practices](#best-practices)
-   [Типові підводні камені, security traps](#типові-підводні-камені-security-traps)
-   [Корисні ресурси та документація](#корисні-ресурси-та-документація)
-   [Короткий підсумок](#короткий-підсумок)

---

## Вступ

**Electron.js** — сучасний open-source фреймворк для створення кросплатформених desktop-додатків з використанням JavaScript, HTML, CSS, Node.js.  
Electron об'єднує рушії Chromium, V8 і Node.js, що дозволяє писати десктопні додатки на тому ж стеку, що й web.  
У 2024 році Electron — основний вибір для UI-heavy desktop apps: VS Code, Figma, Slack, Discord, Notion, GitHub Desktop та тисячі інших.

---

## Що таке Electron.js

-   **Electron.js** — це фреймворк, який дозволяє створювати desktop-додатки з web-інтерфейсом.
-   Кожен додаток має **Main Process** (контролює життєвий цикл, IPC, системні API) та **Renderer Process** (UI, браузерна сторінка).
-   Electron дозволяє поєднати доступ до OS-функцій (через Node.js API), web-UI (через Chromium), сучасний front-end.

---

## Історія та роль Electron.js

-   **2013:** Запуск Atom Shell (GitHub).
-   **2015:** Ребрендинг у Electron.
-   **2016-2024:** Electron стає стандартом для кросплатформених desktop apps, інтеграція з WebAssembly, ARM, sandbox, autoUpdater.
-   Electron активно використовується в enterprise, стартапах, open-source.

---

## Встановлення та старт проекту

### Встановлення Electron CLI

```bash
npm install --save-dev electron
```

### Швидкий старт нового проекту

```bash
npx create-electron-app my-electron-app
cd my-electron-app
npm start
```

### Мінімальний package.json

```json
{
    "name": "electron-demo",
    "main": "main.js",
    "scripts": { "start": "electron ." },
    "devDependencies": { "electron": "^29.0.0" }
}
```

### Перший запуск

```bash
npm start
```

---

## Структура проєкту, основні файли

```
my-electron-app/
├─ main.js            # Main Process — управління вікнами, системними API
├─ preload.js         # Міст для IPC (Inter-Process Communication), security
├─ renderer.js        # UI-логіка (Renderer Process)
├─ index.html         # UI-шаблон
├─ package.json
├─ assets/            # Іконки, зображення
├─ dist/              # Збірка для деплой
├─ node_modules/
├─ tests/             # Тестування
```

-   **main.js** — точка входу, створення BrowserWindow.
-   **preload.js** — безпечний міст для IPC.
-   **renderer.js** — UI-логіка, будь-який front-end фреймворк.
-   **tests/** — Spectron, Playwright, Jest.

---

## Головний процес (Main Process), рендерер (Renderer Process)

### Main Process

-   Відповідає за створення/управління BrowserWindow.
-   Доступ до Node.js API, системних функцій (fs, path, shell, process, net).
-   IPC через ipcMain.

```js
// main.js
const { app, BrowserWindow } = require("electron");
function createWindow() {
    const win = new BrowserWindow({
        width: 1000,
        height: 700,
        webPreferences: {
            preload: __dirname + "/preload.js",
            contextIsolation: true,
            sandbox: true,
        },
    });
    win.loadFile("index.html");
}
app.whenReady().then(createWindow);
app.on("window-all-closed", () => {
    if (process.platform !== "darwin") app.quit();
});
```

### Renderer Process

-   Відображає UI, працює як web-сторінка.
-   Має доступ до API лише через preload.js.
-   Можна використовувати React, Vue, Svelte, Angular.

```js
// renderer.js
document.getElementById("btn").onclick = () => {
    window.electronAPI.sendMsg("Привіт із renderer!");
};
```

---

## IPC (Inter-Process Communication), безпека та lifecycle

### IPC (Inter-Process Communication)

-   Зв’язок між main та renderer процесами через ipcMain/ipcRenderer.
-   Для передачі даних, команд, callback-ів.

```js
// preload.js
const { contextBridge, ipcRenderer } = require("electron");
contextBridge.exposeInMainWorld("electronAPI", {
    sendMsg: (msg) => ipcRenderer.send("msg", msg),
    onMsg: (cb) => ipcRenderer.on("msg-reply", (event, data) => cb(data)),
});
```

```js
// main.js
const { ipcMain } = require("electron");
ipcMain.on("msg", (event, msg) => {
    console.log("main отримав:", msg);
    event.sender.send("msg-reply", "Відповідь з main process");
});
```

### Безпека IPC

-   Не відкривай Node.js API напряму у renderer.
-   Використовуй contextBridge, preload.js.
-   Валідуй всі дані, що надсилаються через IPC.

### Lifecycle

-   app.whenReady, app.on('window-all-closed'), app.on('activate') — коректна робота на Mac/Linux/Win.
-   Закривай ресурси, BrowserWindow при завершенні.

---

## Інтеграція з Node.js, доступ до файлової системи

-   Main Process дозволяє працювати з файловою системою, OS API.

```js
// main.js
const fs = require("fs");
fs.writeFileSync("log.txt", "Старт Electron!");
```

-   Для взаємодії з renderer — IPC + preload.js.

```js
// preload.js
contextBridge.exposeInMainWorld("electronAPI", {
    readFile: (path) => ipcRenderer.invoke("read-file", path),
});

// main.js
ipcMain.handle("read-file", async (event, path) =>
    fs.promises.readFile(path, "utf8")
);
```

---

## Створення вікон, BrowserWindow, конфігурація

-   **BrowserWindow** — основний компонент для UI.
-   Параметри: width, height, frame, fullscreen, transparent, resizable, icon.

```js
const win = new BrowserWindow({
    width: 1024,
    height: 768,
    frame: false,
    transparent: true,
    icon: __dirname + "/assets/icon.png",
    resizable: true,
    webPreferences: {
        nodeIntegration: false,
        contextIsolation: true,
        preload: __dirname + "/preload.js",
    },
});
```

-   Child windows, modal, splash screen, draggable windows — все підтримується.
-   win.webContents — навігація, exec JS, контроль webview.

---

## Меню, контекстне меню, Tray, глобальні шорткати

### Меню

```js
const { Menu } = require("electron");
const template = [
    { label: "Файл", submenu: [{ label: "Вихід", role: "quit" }] },
    { label: "Правка", submenu: [{ label: "Копіювати", role: "copy" }] },
];
Menu.setApplicationMenu(Menu.buildFromTemplate(template));
```

### Контекстне меню

```js
const contextMenu = Menu.buildFromTemplate([
    { label: "Оновити", click: () => win.reload() },
]);
win.webContents.on("context-menu", () => contextMenu.popup());
```

### Tray (системний трей)

```js
const { Tray } = require("electron");
const tray = new Tray(__dirname + "/assets/icon.png");
tray.setToolTip("Мій Electron App");
tray.setContextMenu(contextMenu);
```

### Глобальні шорткати

```js
const { globalShortcut } = require("electron");
app.whenReady().then(() => {
    globalShortcut.register("CommandOrControl+Shift+X", () => {
        win.show();
    });
});
```

---

## Робота з нотифікаціями, діалогами, shell, drag&drop

### Нотифікації

```js
const { Notification } = require("electron");
new Notification({ title: "Статус", body: "Операція завершена." }).show();
```

### Діалоги

```js
const { dialog } = require("electron");
dialog.showOpenDialog({ properties: ["openFile"] }).then((result) => {
    if (!result.canceled) console.log("Обраний файл:", result.filePaths[0]);
});
```

### Shell

```js
const { shell } = require("electron");
shell.openExternal("https://electronjs.org");
```

### Drag&Drop

-   В HTML додавай атрибути drag/drop.
-   В main process — обробляй події "drop" через IPC, файлову систему.

```js
// renderer.js
document.addEventListener("drop", (event) => {
    event.preventDefault();
    window.electronAPI.handleDrop(event.dataTransfer.files);
});
```

---

## Автоматичне оновлення (autoUpdater), деплой, Squirrel, electron-builder

### autoUpdater

-   Для оновлення додатку використовуй electron-updater + electron-builder.

```js
import { autoUpdater } from "electron-updater";
autoUpdater.checkForUpdatesAndNotify();
autoUpdater.on("update-available", () => {
    new Notification({
        title: "Оновлення",
        body: "Доступна нова версія.",
    }).show();
});
```

### Деплой

-   Збірка для Windows/macOS/Linux — electron-builder, electron-forge.
-   Конфігуруй build у package.json (targets, icon, appId, files).

```json
"build": {
  "appId": "com.example.electronapp",
  "win": { "icon": "assets/icon.ico" },
  "mac": { "icon": "assets/icon.icns" },
  "linux": { "icon": "assets/icon.png" }
}
```

-   Для Squirrel — підтримка автооновлення на Windows.

### CI/CD

-   Налаштовуй GitHub Actions для автоматичної збірки/релізу.
-   Публікуй в GitHub Releases, AppImage, Snap, dmg, exe.

---

## Поглиблено: підкапотна робота Electron (Chromium, V8, Node.js, security traps, memory, perf)

### Архітектура Electron

-   Electron = Chromium (UI)+ Node.js (серверна логіка)+ V8 (JS engine).
-   Main Process — керує вікнами, IPC, системними функціями.
-   Кожен BrowserWindow — окремий процес, sandboxed.
-   Renderer — Chromium + V8 + preload.js.

#### Схема архітектури

```
[Main Process (Node.js)] <-> [Preload.js (contextBridge)] <-> [Renderer Process (Chromium, V8)]
       |                           |
  Node.js API                  IPC, Web API
```

### Внутрішні механізми

-   IPC — канал для передачі повідомлень, callback-ів, даних.
-   contextIsolation — ізоляція контексту виконання renderer.
-   sandbox — обмеження доступу до OS/Node.js API.
-   disable nodeIntegration — заборона require/import у renderer.
-   validate input — валідація даних з UI.
-   CSP (Content Security Policy) — захист від XSS.

### Memory management

-   Кожне вікно — окремий процес (RAM, CPU).
-   Відстежуй та закривай невикористані BrowserWindow.
-   Профілюй через Chrome DevTools (View → Toggle Developer Tools).
-   Використовуй process.getProcessMemoryInfo() для моніторингу.

### Performance traps

-   Велика кількість BrowserWindow — високий RAM/CPU.
-   Важкі JS-обчислення — використовуй worker threads/Web Workers.
-   Великі картинки, не оптимізовані ресурси — гальмують UI.
-   Не оптимізовані IPC — bottleneck для продуктивності.

#### Візуалізація Event Loop у Electron

```
[Main Process Event Loop]
    ↑       ↓
[IPC] <-> [Renderer Process Event Loop]
```

### Deep dive-матеріали

-   [Electron Security Docs](https://www.electronjs.org/docs/latest/tutorial/security)
-   [Electron Architecture](https://www.electronjs.org/docs/latest/tutorial/architecture)
-   [Memory & Performance](https://www.electronjs.org/docs/latest/tutorial/performance)
-   [Chromium V8](https://v8.dev/)
-   [Node.js Internals](https://nodejs.org/en/docs/)

---

## Інтеграція з Frontend-фреймворками (React, Vue, Svelte, Angular)

-   Electron підтримує будь-який front-end стек.
-   Для React/Vue/Svelte — збирай через Vite, Webpack, Parcel.
-   Renderer — це стандартний SPA/MPA, що працює у BrowserWindow.

### Приклад інтеграції React

```js
// main.js
win.loadURL('http://localhost:3000'); // старт dev-server React

// package.json
"scripts": {
  "start": "concurrently \"react-scripts start\" \"electron .\""
}
```

-   Для production — win.loadFile('build/index.html').
-   Для Vue/Svelte — аналогічно.

### Hot reload

-   В dev режимі — автоматичне оновлення UI через HMR (hot module replacement).

---

## Масштабування, багатовіконність, багатопроцесорність, Worker Threads

### Багатовіконність

-   Створюй декілька BrowserWindow:

```js
const win1 = new BrowserWindow({ width: 800, height: 600 });
const win2 = new BrowserWindow({ width: 400, height: 300 });
```

-   Для модальних/дочірніх вікон — parent, modal.

### Worker Threads

-   Для heavy tasks — використовуй worker_threads у main process.

```js
const { Worker } = require("worker_threads");
const worker = new Worker("./heavy-task.js");
worker.on("message", (result) => console.log("Результат:", result));
```

-   Для renderer — Web Workers.

### Масштабування

-   Використовуй app.setAppUserModelId для коректної роботи нотифікацій, tray, shortcuts на Windows.
-   Впроваджуй кешування даних, оптимізуй IPC.

---

## Тестування: Spectron, Playwright, Jest, Mocha, Vitest

### Spectron (офіційний, але deprecated)

-   Автоматизація e2e тестів Electron (на базі WebDriver).

```js
import { Application } from "spectron";
const app = new Application({ path: "/path/to/electron" });
app.start().then(() =>
    app.client.getWindowCount().then((count) => expect(count).toBe(1))
);
```

### Playwright

-   Тестуй UI, IPC, performance.

```js
import { test, expect, electron } from "@playwright/test";
test("main window open", async ({ electronApp }) => {
    const window = await electronApp.firstWindow();
    await expect(window.locator("text=Hello")).toBeVisible();
});
```

### Jest, Mocha, Vitest

-   Для unit-тестів main/renderer логіки.

```js
test("функція суми", () => {
    expect(sum(2, 3)).toBe(5);
});
```

---

## Best practices

-   Діли код на main, preload, renderer — не міксуй контексти.
-   Використовуй contextIsolation, sandbox, preload.
-   Валідуй дані між процесами (IPC).
-   Використовуй сучасні front-end фреймворки (React, Vue, Svelte) у renderer.
-   Профілюй пам’ять, закривай невикористані BrowserWindow.
-   Оновлюй Electron та залежності регулярно.
-   Впроваджуй autoUpdater для seamless updates.
-   Документуй IPC і структуру процесів.
-   Використовуй environment змінні для секретів.
-   Додавай тестування (unit, e2e) для main та renderer.
-   Використовуй ESLint, Prettier для підтримки якості коду.
-   Уникай nodeIntegration у renderer.
-   Використовуй security best practices (CSP, validation, rate limiting).

---

## Типові підводні камені, security traps

-   Не використовуйте nodeIntegration у renderer — XSS risk!
-   Не передавайте великі об’єкти через IPC.
-   Не відкривайте remote URLs у BrowserWindow без sandbox.
-   Слідкуйте за контекстом виконання (main/renderer).
-   Очищуйте ресурси при закритті вікон.
-   Перевіряйте всі дані із renderer перед обробкою у main.
-   Регулярно оновлюйте Electron — безпека!
-   Уникайте використання eval, new Function, небезпечних JS-конструкцій.
-   Впроваджуйте CSP у index.html.

---

## Корисні ресурси та документація

-   [Офіційна документація Electron.js](https://www.electronjs.org/docs/latest/)
-   [Electron API Reference](https://www.electronjs.org/docs/latest/api/)
-   [Electron Security](https://www.electronjs.org/docs/latest/tutorial/security)
-   [Electron Builder](https://www.electron.build/)
-   [Electron Forge](https://electronforge.io/)
-   [Electron Updater](https://www.electron.build/auto-update)
-   [Electron Deep Dive Blog](https://blog.electronjs.org/)
-   [Chromium Docs](https://www.chromium.org/developers/)
-   [Node.js Docs](https://nodejs.org/en/docs/)
-   [VS Code Architecture (Electron)](https://code.visualstudio.com/docs/architecture)
-   [Spectron Docs](https://www.electronjs.org/spectron)
-   [Playwright Docs](https://playwright.dev/docs/api/class-electron)
-   [Awesome Electron](https://github.com/sindresorhus/awesome-electron)

---

## Короткий підсумок

**Electron.js — потужний, сучасний фреймворк для кросплатформених desktop-додатків на web-стеку.**  
Глибоке розуміння архітектури, IPC, безпеки, пам’яті та продуктивності — ключ до професійної розробки.  
Дотримуйся best practices, профілюй, тестуй, розділяй main/renderer, впроваджуй security та auto update — і твій desktop-продукт буде відповідати вимогам 2024+!

---
