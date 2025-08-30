# PRISMA

Prisma — ORM для Node.js та TypeScript, що дозволяє працювати з базами даних через типізовані запити.

## Категорія: Основні команди CLI

| Команда/метод            | Опис              | Приклад/Аутпут                        |
| ------------------------ | ----------------- | ------------------------------------- |
| npx prisma init          | ініціалізація     | створює prisma/schema.prisma          |
| npx prisma generate      | генерація клієнта | оновлює node_modules/@prisma/client   |
| npx prisma migrate dev   | міграція (dev)    | застосовує/створює міграції           |
| npx prisma migrate reset | скидання БД       | видаляє всі дані, застосовує міграції |
| npx prisma studio        | GUI для БД        | відкриває Prisma Studio               |
| npx prisma db seed       | сидування         | запускає seed-скрипт                  |
| npx prisma db pull       | імпорт схеми з БД | оновлює schema.prisma                 |
| npx prisma db push       | пуш схеми в БД    | оновлює структуру БД                  |

## Категорія: Типи полів у schema.prisma

| Тип/атрибут                                    | Опис               | Приклад/Аутпут                                          |
| ---------------------------------------------- | ------------------ | ------------------------------------------------------- |
| Int, String, DateTime, Boolean, Float, Decimal | базові типи        | age Int, name String, ...                               |
| @id                                            | первинний ключ     | id Int @id                                              |
| @default(autoincrement())                      | автоінкремент      | id Int @id @default(autoincrement())                    |
| @unique                                        | унікальне поле     | email String @unique                                    |
| @updatedAt                                     | автооновлення дати | updatedAt DateTime @updatedAt                           |
| @relation                                      | зв'язок            | user User @relation(fields: [userId], references: [id]) |
| @@index, @@unique                              | індекси            | @@index([email])                                        |
| @@map, @map                                    | мапінг імен        | @@map("users")                                          |
| enum Role { ... }                              | перелік            | enum Role {USER,ADMIN}                                  |

## Категорія: Зв’язки (relations)

| Тип зв’язку | Опис               | Приклад/Аутпут                                |
| ----------- | ------------------ | --------------------------------------------- |
| 1:1         | один до одного     | user User? @relation                          |
| 1:N         | один до багатьох   | posts Post[]                                  |
| M:N         | багато до багатьох | categories Category[]                         |
| @relation   | явний зв’язок      | @relation(fields: [userId], references: [id]) |

## Категорія: Prisma Client (JS/TS)

| Команда/метод                      | Опис                    | Приклад/Аутпут                                   |
| ---------------------------------- | ----------------------- | ------------------------------------------------ |
| import {PrismaClient}              | імпорт клієнта          | import {PrismaClient} from '@prisma/client'      |
| const prisma = new PrismaClient()  | створення екземпляра    | const prisma = new PrismaClient()                |
| prisma.user.findMany()             | отримати всі            | prisma.user.findMany()                           |
| prisma.user.findUnique()           | знайти унікальний       | prisma.user.findUnique({where:{id:1}})           |
| prisma.user.findFirst()            | знайти перший           | prisma.user.findFirst({where:{...}})             |
| prisma.user.create()               | створити                | prisma.user.create({data:{...}})                 |
| prisma.user.createMany()           | створити багато         | prisma.user.createMany({data:[...]})             |
| prisma.user.update()               | оновити                 | prisma.user.update({where:{id:1},data:{...}})    |
| prisma.user.updateMany()           | оновити багато          | prisma.user.updateMany({where:{...},data:{...}}) |
| prisma.user.delete()               | видалити                | prisma.user.delete({where:{id:1}})               |
| prisma.user.deleteMany()           | видалити багато         | prisma.user.deleteMany({where:{...}})            |
| prisma.user.upsert()               | створити/оновити        | prisma.user.upsert({...})                        |
| prisma.user.count()                | підрахунок              | prisma.user.count()                              |
| prisma.user.aggregate()            | агрегація               | prisma.user.aggregate({ \_avg: {age:true} })     |
| prisma.user.groupBy()              | групування              | prisma.user.groupBy({by:['role']})               |
| prisma.user.findMany({skip, take}) | пагінація               | prisma.user.findMany({skip:10,take:5})           |
| prisma.user.findMany({orderBy})    | сортування              | prisma.user.findMany({orderBy:{age:'desc'}})     |
| prisma.user.findMany({select})     | вибір полів             | prisma.user.findMany({select:{id:true}})         |
| prisma.user.findMany({include})    | вкладені дані           | prisma.user.findMany({include:{posts:true}})     |
| prisma.$transaction([])            | транзакція              | prisma.$transaction([ ... ])                     |
| prisma.$queryRaw()                 | сирий SQL               | prisma.$queryRaw`SELECT * FROM User`             |
| prisma.$executeRaw()               | сирий SQL (зміни)       | prisma.$executeRaw`DELETE FROM ...`              |
| prisma.$connect()/$disconnect()    | підключення/відключення | prisma.$connect()                                |

## Категорія: Фільтрація та оператори

| Оператор/метод       | Опис              | Приклад/Аутпут                 |
| -------------------- | ----------------- | ------------------------------ |
| where                | фільтр            | where: {age: {gt: 18}}         |
| select               | вибір полів       | select: {id: true, name: true} |
| include              | вкладені дані     | include: {posts: true}         |
| orderBy              | сортування        | orderBy: {createdAt: 'desc'}   |
| skip/take            | пагінація         | skip: 10, take: 5              |
| distinct             | унікальні         | distinct: ['email']            |
| gt/gte/lt/lte/equals | порівняння        | age: {gte: 18}                 |
| in/notIn/contains    | множини/пошук     | name: {in: ['a','b']}          |
| AND/OR/NOT           | логічні оператори | where: {AND: [{a:1},{b:2}]}    |

## Категорія: Seed, Middleware, Extensions

| Команда/метод  | Опис         | Приклад/Аутпут                         |
| -------------- | ------------ | -------------------------------------- |
| prisma/seed.js | сидування    | module.exports = async()=>{...}        |
| middleware     | перехоплення | prisma.$use(async(params,next)=>{...}) |
| extension      | розширення   | prisma.$extends({...})                 |

## Категорія: Advanced/Best practices

| Команда/метод       | Опис              | Приклад/Аутпут                     |
| ------------------- | ----------------- | ---------------------------------- |
| soft delete         | м'яке видалення   | deletedAt DateTime?                |
| createdAt/updatedAt | аудиту поля       | createdAt DateTime @default(now()) |
| transaction         | транзакія         | prisma.$transaction([ ... ])       |
| raw SQL             | сирий SQL         | prisma.$queryRaw`...`              |
| env("DATABASE_URL") | змінна середовища | datasource db {url = env("...")}   |

---

> Шпаргалка складена за інструкціями: компактно, категоріями, з короткими прикладами та описами.
