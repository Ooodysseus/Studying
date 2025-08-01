# Electron JS Cheatsheet

## CLI & Project Setup
npm install -g electron  
npm init -y  
npm install electron --save-dev  
npx electron .  

## Entry Point (main.js)
const { app, BrowserWindow } = require('electron');  
function createWindow() {  
  const win = new BrowserWindow({ width: 800, height: 600 });  
  win.loadFile('index.html');  
}  
app.whenReady().then(createWindow);  

## Main & Renderer Process
Main: Node.js APIs, controls windows  
Renderer: Runs in BrowserWindow, like a browser page  

## Create BrowserWindow
new BrowserWindow({ width: 1024, height: 768 })  
new BrowserWindow({ show: false })  
win.setAlwaysOnTop(true)  
win.setFullScreen(true)  
win.setResizable(false)  
win.webContents.openDevTools()  
win.loadURL('https://example.com')  
win.loadFile('index.html')  
win.on('closed', () => { win = null })  

## IPC Communication
const { ipcMain } = require('electron');  
ipcMain.on('event-name', (event, arg) => { event.reply('reply-event', 'message') });  
// Renderer
const { ipcRenderer } = require('electron');  
ipcRenderer.send('event-name', 'data');  
ipcRenderer.on('reply-event', (event, data) => { /* ... */ });  

## Menu
const { Menu } = require('electron');  
const template = [  
  { label: 'File', submenu: [ { role: 'quit' } ] },  
  { label: 'Edit', submenu: [ { role: 'copy' }, { role: 'paste' } ] }  
];  
const menu = Menu.buildFromTemplate(template);  
Menu.setApplicationMenu(menu);  

## Tray
const { Tray } = require('electron');  
const tray = new Tray('icon.png');  
tray.setToolTip('App Name');  
tray.on('click', () => { mainWindow.show(); });  

## Dialog
const { dialog } = require('electron');  
dialog.showOpenDialog({ properties: ['openFile'] }).then(result => { /* ... */ });  
dialog.showMessageBox({ message: 'Hello!', buttons: ['OK'] });  

## Notifications
new Notification({ title: 'Title', body: 'Message' }).show();  

## File System
const fs = require('fs');  
fs.readFile('file.txt', (err, data) => { /* ... */ });  
fs.writeFile('file.txt', 'content', () => {});  

## App Events
app.on('window-all-closed', () => { if (process.platform !== 'darwin') app.quit(); });  
app.on('activate', () => { if (BrowserWindow.getAllWindows().length === 0) createWindow(); });  
app.on('ready', createWindow);  

## Auto Update
const { autoUpdater } = require('electron-updater');  
autoUpdater.checkForUpdatesAndNotify();  
autoUpdater.on('update-downloaded', () => { autoUpdater.quitAndInstall(); });  

## Store Data
localStorage.setItem('key', 'value');  
localStorage.getItem('key');  
sessionStorage.setItem('session', 'val');  

## Open External Links
const { shell } = require('electron');  
shell.openExternal('https://github.com');  

## Shortcut Keys
const { globalShortcut } = require('electron');  
globalShortcut.register('CmdOrCtrl+X', () => { /* ... */ });  

## Power Save Blocker
const { powerSaveBlocker } = require('electron');  
const id = powerSaveBlocker.start('prevent-app-suspension');  
powerSaveBlocker.stop(id);  

## Crash Reporter
const { crashReporter } = require('electron');  
crashReporter.start({ submitURL: 'https://yourdomain.com/url' });  

## Screen Capture
const { desktopCapturer } = require('electron');  
desktopCapturer.getSources({ types: ['screen', 'window'] }).then(sources => { /* ... */ });  

## Webview Tag
<webview src="https://electronjs.org" style="width:100%; height:600px"></webview>  
webview.addEventListener('did-finish-load', () => { /* ... */ });  

## Security
win.webContents.session.setPermissionRequestHandler((webContents, permission, callback) => {  
  if (permission === 'notifications') callback(false);  
  else callback(true);  
});  
win.webContents.setWindowOpenHandler(({ url }) => { return { action: 'deny' }; });  
contextIsolation: true  
nodeIntegration: false  
enableRemoteModule: false  

## Packaging
npm install electron-packager -g  
electron-packager . MyApp --platform=win32 --arch=x64  
npm install electron-builder --save-dev  
electron-builder  

## Environment
process.env.NODE_ENV  
process.platform  
process.version  

## Preload Script
preload.js  
contextBridge.exposeInMainWorld('api', { myMethod: () => { /* ... */ } });  

## Renderer Access Preload
window.api.myMethod()  

## Dev Tools
win.webContents.openDevTools();  
mainWindow.webContents.on('did-finish-load', () => { /* ... */ });  

## Window Controls
win.minimize()  
win.maximize()  
win.close()  
win.restore()  
win.setSize(800, 600)  
win.setPosition(100, 100)  
win.isMinimized()  
win.isMaximized()  
win.setFullScreen(true)  
win.setAlwaysOnTop(true)  

## Multi Window
let win1 = new BrowserWindow({ width: 800 });  
let win2 = new BrowserWindow({ width: 400 });  

## Splash Screen
const splash = new BrowserWindow({ width:300, height:300, frame:false });  
splash.loadFile('splash.html');  

## Drag & Drop
document.addEventListener('drop', (e) => { /* ... */ });  
document.addEventListener('dragover', (e) => { /* ... */ });  

## Clipboard
const { clipboard } = require('electron');  
clipboard.writeText('Copied text');  
clipboard.readText();  

## Native Image
const { nativeImage } = require('electron');  
let image = nativeImage.createFromPath('icon.png');  
win.setIcon(image);  

## Session
win.webContents.session.clearCache().then(() => { /* ... */ });  
win.webContents.session.cookies.get({})  

## Protocols
const { protocol } = require('electron');  
protocol.registerFileProtocol('atom', (request, callback) => { /* ... */ });  

## App Paths
app.getPath('userData')  
app.getPath('downloads')  
app.getAppPath()  

## Logging
console.log('Message');  
require('electron-log').info('Info');  

## Platform Checks
if (process.platform === 'darwin') { /* macOS */ }  
if (process.platform === 'win32') { /* Windows */ }  

## Dev/Prod Split
if (process.env.NODE_ENV === 'development') { win.webContents.openDevTools(); }  

## Best Practices
Use contextIsolation for security  
Disable nodeIntegration in renderer  
Always validate IPC data  
Catch window close events  
Don't block main process  
Keep dependencies up to date  
Use preload scripts  
Package for all target platforms  
Test on multiple OS  
Don't store sensitive data in localStorage  
Prefer secure dialogs  
Handle errors gracefully  
Document IPC channels  
Minimize permissions  
Update Electron regularly  
Lint code  
Use ESLint/Prettier  
Handle auto updates  
Provide user feedback  
Keep windows responsive  
Avoid synchronous code in main  
Handle crashes  
Log errors  
Use crashReporter  
Prefer async APIs  
Use main/renderer separation  
Test accessibility  
Minimize bundle size  
Compress assets  
Version your app  
Sign installers  
Test install/uninstall  
Handle app restart logic  
Keep user data safe  
Avoid eval()  
Monitor memory usage  
Avoid blocking UI  
Handle DPI scaling  
Support dark mode  
Use SVG for icons  
Provide help/about dialogs  
Test in sandbox mode  
Automate builds  
Script packaging  
Document dependencies  
Test drag and drop  
Handle clipboard gracefully  
Use platform-specific features  
Test notifications  
Support multiple users  
Keep session management clean  
Use semantic versioning  
Version release notes  
Keep changelog  
Review Electron security updates  
Support keyboard shortcuts  
Provide responsive UI  
Support high DPI displays  
Minimize startup time  
Test splash screens  
Handle tray events  
Test auto-launch  
Provide uninstall feedback  
Handle update rollback  
Test remote debugging  
Avoid deprecated APIs  
Document preload contracts  
Handle protocol registration  
Test custom protocols  
Provide error fallback UI  
Monitor for memory leaks  
Use nodeIntegration with caution  
Prefer contextBridge  
Audit third-party modules  
Keep code modular  
Organize main/renderer code  
Use TypeScript if possible  
Test in production build  
Document window options  
Review application menu  
Support multi-window  
Prefer async/await  
Use try/catch everywhere  
Document crash policy  
Test edge cases  
