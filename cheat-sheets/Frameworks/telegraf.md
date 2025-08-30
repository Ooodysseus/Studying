# TELEGRAF (Telegram Bot, Node.js)

Telegraf — популярна бібліотека для створення Telegram-ботів на Node.js з підтримкою middleware, сцен, inline-режиму, клавіатур, роботи з API Telegram.

## Категорія: Встановлення та старт

| Команда/метод                            | Опис                  | Приклад/Аутпут                                  |
| ---------------------------------------- | --------------------- | ----------------------------------------------- |
| npm install telegraf                     | встановити бібліотеку | npm install telegraf                            |
| import { Telegraf }                      | імпорт ES6            | import { Telegraf } from 'telegraf'             |
| const { Telegraf } = require('telegraf') | імпорт CommonJS       | const { Telegraf } = require('telegraf')        |
| new Telegraf(token)                      | створити бота         | const bot = new Telegraf('TOKEN')               |
| bot.launch()                             | запуск бота           | bot.launch()                                    |
| process.env.BOT_TOKEN                    | токен з env           | const bot = new Telegraf(process.env.BOT_TOKEN) |

## Категорія: Обробка повідомлень та команд

| Команда/метод            | Опис               | Приклад/Аутпут                   |
| ------------------------ | ------------------ | -------------------------------- |
| bot.command('start', fn) | команда /start     | bot.command('start', ctx=>{...}) |
| bot.hears('hi', fn)      | реагувати на текст | bot.hears('hi', ctx=>{...})      |
| bot.on('text', fn)       | будь-який текст    | bot.on('text', ctx=>{...})       |
| bot.action('btn', fn)    | callback-кнопка    | bot.action('btn', ctx=>{...})    |
| bot.use(mw)              | middleware         | bot.use((ctx,next)=>{...})       |
| ctx.reply('msg')         | відповісти         | ctx.reply('Hello!')              |
| ctx.message.text         | текст повідомлення | ctx.message.text                 |
| ctx.from.id              | id користувача     | ctx.from.id                      |

## Категорія: Клавіатури та кнопки

| Команда/метод                | Опис                    | Приклад/Аутпут                                               |
| ---------------------------- | ----------------------- | ------------------------------------------------------------ |
| Markup.keyboard([...])       | звичайна клавіатура     | Markup.keyboard([['A','B']])                                 |
| Markup.inlineKeyboard([...]) | inline-клавіатура       | Markup.inlineKeyboard([[Markup.button.callback('OK','ok')]]) |
| Markup.button.callback       | callback-кнопка         | Markup.button.callback('OK','ok')                            |
| Markup.button.url            | кнопка-посилання        | Markup.button.url('Site','https://')                         |
| ctx.replyWithMarkdown        | markdown-відповідь      | ctx.replyWithMarkdown('_bold_')                              |
| ctx.editMessageText          | редагувати повідомлення | ctx.editMessageText('new')                                   |

## Категорія: Робота з медіа

| Команда/метод         | Опис       | Приклад/Аутпут                    |
| --------------------- | ---------- | --------------------------------- |
| ctx.replyWithPhoto    | фото       | ctx.replyWithPhoto('url.jpg')     |
| ctx.replyWithVideo    | відео      | ctx.replyWithVideo('url.mp4')     |
| ctx.replyWithAudio    | аудіо      | ctx.replyWithAudio('url.mp3')     |
| ctx.replyWithDocument | файл       | ctx.replyWithDocument('file.pdf') |
| ctx.replyWithLocation | геолокація | ctx.replyWithLocation(50,30)      |

## Категорія: Middleware, сцени, сесії

| Команда/метод | Опис                | Приклад/Аутпут                                |
| ------------- | ------------------- | --------------------------------------------- |
| bot.use(mw)   | middleware          | bot.use((ctx,next)=>{...})                    |
| session()     | сесії               | const session = require('telegraf/session')   |
| Scenes, Stage | сцени               | const { Scenes, Stage } = require('telegraf') |
| enter/leave   | вхід/вихід зі сцени | ctx.scene.enter('scene')                      |
| ctx.session   | дані сесії          | ctx.session.counter = 1                       |

## Категорія: Inline-режим, callback, API

| Команда/метод            | Опис                   | Приклад/Аутпут                    |
| ------------------------ | ---------------------- | --------------------------------- |
| bot.inlineQuery(fn)      | inline-запит           | bot.inlineQuery((ctx)=>{...})     |
| ctx.answerInlineQuery    | відповісти inline      | ctx.answerInlineQuery([...])      |
| ctx.answerCbQuery        | відповісти на callback | ctx.answerCbQuery('OK')           |
| ctx.telegram.sendMessage | API Telegram           | ctx.telegram.sendMessage(id,'hi') |
| ctx.telegram.getChat     | отримати чат           | ctx.telegram.getChat(id)          |

## Категорія: Обробка помилок, best practices

| Команда/метод          | Опис                    | Приклад/Аутпут                        |
| ---------------------- | ----------------------- | ------------------------------------- |
| bot.catch(fn)          | глобальний catch        | bot.catch((err,ctx)=>{...})           |
| try/catch              | локальна обробка        | try { ... } catch(e) { ... }          |
| process.once('SIGINT') | коректне завершення     | process.once('SIGINT',()=>bot.stop()) |
| .env для токена        | безпека                 | BOT_TOKEN=...                         |
| async/await            | асинхронність           | await ctx.reply('hi')                 |
| Логування              | console.log(ctx.update) |                                       |
| Валідація даних        | перевірка input         | if(!ctx.message.text) return          |

## Категорія: Advanced/Інше

| Команда/метод                         | Опис                 | Приклад/Аутпут                        |
| ------------------------------------- | -------------------- | ------------------------------------- |
| bot.telegram                          | прямий доступ до API | bot.telegram.sendPhoto(id, url)       |
| bot.stop()                            | зупинити бота        | bot.stop()                            |
| bot.context                           | розширення контексту | bot.context.myProp = ...              |
| bot.launch({dropPendingUpdates:true}) | ігнорувати старі     | bot.launch({dropPendingUpdates:true}) |
| bot.use(rateLimit())                  | rate limiting        | bot.use(rateLimit({window:1000}))     |
| bot.webhookCallback()                 | для серверів         | app.use(bot.webhookCallback('/tg'))   |

---

> Шпаргалка складена за інструкціями: компактно, категоріями, з короткими прикладами та описами.
