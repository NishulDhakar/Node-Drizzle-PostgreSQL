# Node + Drizzle ORM + PostgreSQL Starter

Minimal, production-ready backend boilerplate using:

- Node.js
- Express
- TypeScript
- Drizzle ORM (SQL-first, type-safe)
- PostgreSQL
- tsx (fast dev runner)

---

## Project Structure

```
src/
├─ db/
│  ├─ index.ts        # database connection
│  ├─ schema.ts       # tables
│ 
│
├─ routes/
│  └─ user.routes.ts  # example CRUD routes
│
├─ app.ts             # express config
└─ server.ts          # entry point

drizzle.config.ts
.env
```

---

## Setup

### 1. Install dependencies

```bash
npm install
```

### 2. Create `.env`

```env
DATABASE_URL=postgresql://postgres:password@localhost:5432/mydb
PORT=
```

### 3. Generate migrations

```bash
npm run db:generate
```

### 4. Run migrations

```bash
npm run db:migrate
```

This creates your tables in PostgreSQL.

### 5. Start development server

```bash
npm run dev
```

Server runs at: `http://localhost:5000`

---

## Available Scripts

```bash
npm run dev          # start dev server
npm run build        # compile TypeScript
npm start            # run production build
npm run db:generate  # create migration files
npm run db:migrate   # apply migrations
```

---

## Database Schema Example

### Users Table

```ts
export const users = pgTable("users", {
  id: uuid("id").defaultRandom().primaryKey(),
  name: text("name").notNull(),
  email: text("email").notNull().unique(),
  createdAt: timestamp("created_at").defaultNow(),
});
```

---

## API Endpoints

### Get all users

```
GET /users
```

### Create user

```
POST /users
Content-Type: application/json
```

Body:

```json
{
  "name": "John",
  "email": "john@test.com"
}
```

---

## Testing with curl

```bash
curl -X POST http://localhost:5000/users \
-H "Content-Type: application/json" \
-d '{"name":"John","email":"john@test.com"}'
```

---

## Recommended Additions

For production apps, consider adding:

- JWT authentication
- Password hashing (bcrypt)
- Zod validation
- Role-based access
- Docker setup
- Logging (pino)
- Rate limiting
- Error middleware
- Seed scripts

---

## Why Drizzle?

Drizzle is:

- SQL-first
- Lightweight
- Fully type-safe
- No heavy ORM magic
- Great performance

You write real SQL, not abstractions.

---

## Deployment

Works great with:

- Docker
- Railway
- Render
- Fly.io
- AWS
- DigitalOcean

Just set `DATABASE_URL` as an environment variable.

---

## License

MIT