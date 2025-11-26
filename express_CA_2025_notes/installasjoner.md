## Installasjoner

- Start et nytt node.js prosjekt: npm init -y
- Legg til "type": "module", i package.json filen.
- npm install express
- npm install —save-dev typescript @types/node @types/express tsx
  - Dette legger til devDependencies i package.json filen.
  - tsx kjører typescript. Står for TypeScript Execute. Har watch mode.
- npx tsc —init

  - Lager en tsconfig.json fil
  - tsconfig er en config fil for typescript. Den forteller typescript compiler hvordan den skal prosessere koden. Hvilket språk, hvor finne source files, hvor den skal plassere compiled output. Å justere denne filen hjelper å sikre at prosjektet kjøre smertefritt med TS og Express.
  - Vi kan oppdatere tsconfig.json filen slik:

  `{
"compilerOptions": {
"target": "ES2020",
"module": "ES2020",
"moduleResolution": "node",
"outDir": "./dist",
"rootDir": "./src",
"strict": true,
"esModuleInterop": true,
"allowSyntheticDefaultImports": true
}
}`

- mkdir src ← Lager en src folder
- touch src/index.ts ← Lager en fil inn i src mappen som heter index.ts.

## mySql

- npm install mysql2

## CORS

- npm install cors + npm install <-- Installeres under "dependencies" i package.json
- npm install -D @types/cors <-- Installeres som dev dependencies i package.json

### CORS forklaring

Cors - Middelware som faktisk håndterer CORS headers.

CORS står for Cross-Origin Resource Sharing og er en nettlesersikkerhetsmekanisme som styrer om en nettadresse kan hente ressurser fra et annet domene. Den forhindrer at et nettsted kan gjøre forespørsler til et annet domene, for å beskytte brukere mot ondsinnet aktivitet som cross-site request forgery (CSRF). Dette gjøres ved å bruke HTTP-overskrifter som forteller nettleseren om en ressurs kan deles mellom ulike domener.

Hvordan det fungerer
"Same-Origin" vs. "Cross-Origin": Nettleseren godkjenner forespørsler automatisk hvis de kommer fra samme opprinnelse (domene, protokoll, og port). CORS er nødvendig når en forespørsel er "cross-origin".

HTTP-overskrifter: Serveren som hoster ressursen, bruker CORS-overskrifter (som Access-Control-Allow-Origin) til å spesifisere hvilke andre domener som får lov til å hente ressursene.

Sikkerhetstiltak: Nettleseren sjekker disse overskriftene og blokkerer forespørselen hvis serveren ikke har tillatt det

## Dotenv

### Local

- npm install dotenv
- Lag en .env fil i root. Legg til .env filen i .gitignore!
- Legg til PORT=3000 f.eks
- import dotenv from "dotenv"
  dotenv.config(); <--Last inn .env filen
- const PORT = process.env.PORT || 4000 <-- Bruker porten fra .env filen eller default hvis jeg ikke satt port.

### Production

DATABASE_URL=postgresql://prod-server:5432/prod_db
API_KEY=real_api_key_abc123

### Eksempel fra oppgave

Her har jeg laget en database.ts fil

import mysql, { Pool } from "mysql2/promise";
import dotenv from "dotenv";
dotenv.config();

const pool: Pool = mysql.createPool({
host: process.env.DB_HOST || "localhost",
user: process.env.DB_USER || "root",
password: process.env.DB_PASSWORD || "",
database: process.env.DB_NAME || "haugerestaurant",
waitForConnections: true,
connectionLimit: 10,
queueLimit: 0,
});

export { pool };

### Dotenv forklaring

dotenv pakken loader automatisk enviroment variabler fra en .env fil til process.env når appen starter.

## Zod

- npm install zod

### Zod forklaring

Zod er et TypeScript-first-skjema valideringsbibliotek. Det lar deg definere valideringsregler i skjemaer. Den erstatter det å bruke manuelle og flere "if statements". man beskriver hvordan valid data ser ut som, og Zod håndterer sjekken for oss.

Zod har TypeScript types bygget inn, så vi trenger ikke bruke separat @types/zod.

Man kan bruke Zod i både backend og frontend og i React. I frontend kan den validere inputs f.eks.

## bcrypt

- npm install bcrypt jsonwebtoken
- npm install --save-dev @types/bcrypt @types/jsonwebtoken

### bcrypt forklaring

Man kan aldri lagre passord i klartekst. Bcrypt hasher (krypterer) passordet og returnerer en token.

Passord uten bcrypt: 123mittpassord
Passord med bcrypt: $2b$10$N9qo8uLOickgx2ZMRZoMy.ZjRnKZ9...

# Swagger UI OpenAPI Documentation

- npm install swagger-ui-express swagger-jsdoc
- npm install --save-dev @types/swagger-ui-express @types/swagger-jsdoc

### Swagger forklaring

importer swaggerUI og swaggerJSDoc til src/index.ts.

<i>Swagger Config</i>
const swaggerOptions = {
definition: {
openapi: "3.0.0",
info: {
title: "Dev platforms API",
version: "1.0.0",
description: "A simple API for managing users and posts",
},
servers: [{ url: `http://localhost:${PORT}` }],
},
apis: ["./src/routes/*.ts"],
};

const swaggerSpec = swaggerJSDoc(swaggerOptions);

<i>API documentation endpoint</i>
app.use("/api-docs", swaggerUi.serve, swaggerUi.setup(swaggerSpec));

Når man skal lage dokumentasjon kan man bruke AI.
Hvis man f.eks skal lage dokumentasjon på routes/users får man en slik kode:

/\*\*

- @swagger
- /users:
- get:
-     summary: Get all users
-     responses:
-       200:
-         description: List of users
  \*/
  router.get("/", async (req, res) => {
  // code
  });

/\*\*

- @swagger
- /users/{id}:
- get:
-     summary: Get user by ID
-     parameters:
-       - in: path
-         name: id
-         required: true
-         schema:
-           type: integer
-     responses:
-       200:
-         description: User details
-       400:
-         description: Invalid user ID
-       404:
-         description: User not found
  \*/
  router.get("/:id", validateUserId, async (req, res) => {
  // code
  });
