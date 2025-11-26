# Start nytt express prosjekt

## Todo's før selve appen

### - npm init -y

Starter nytt node prosjekt.

### - npm tsc --init

Lager en typescript config fil (se installs for hva som skal inn i den filen).

### - mkdir src

### - touch src/index.ts

## I package.json

### - Legg "type": "module", til under name, version, main.

### - Legg til "scripts": \*{

"dev": "tsx watch src/index.ts",
"build": "tsc",
"start": "node dist/index.js"
}\*

## Lag filer

### - .env - root

### - .gitignore - root

### - src/routes

    - auth.ts
    - posts.ts (eller hva det måtte være)
    - users.ts

### - src/middleware

    - auth-validation.ts
    - user-validation

### - src/database

    - Inneholder database pool. F.eks sånn:

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

### - src/interfaces

Interfaces er strukturen/typen. Id er et tall, username er en string osv.

//Full bruker interface for database funksjoner/operasjoner (registering og loginvalideringer bl.a)
export interface User {
id: number;
username: string;
email: string;
password?: string;
}

### - src/types

    - express.d.ts

    Denne forteller typescript at hvis det finnes en user så inneholder den en id som er Number. Denne filen utvider express sin request-type slik at jeg kan legge til req.user i hele prosjektet. I Express finnes det ingen user-property på req som standard. Uten denne koden hadde typescript gitt meg feil (user does not exist).

    Denne koden forteller typescript at i HELE prosjektet, for hver gang TS bruker Request, så kan det finnes en user, og den har formen {id: number}. Den deklarerer globalt.

    Namespace Express{...} <-- TS vet at Express sin request-type ligger i et namespace som heter Express.

    Export gjør filen til en modul. Jeg trenger ikke importere den noe sted, men "export" MÅ være med. Ellers blir den oversett.

    Fordi du hadde en auth-middleware som puttet informasjon om brukeren på req, typisk slik:

req.user = { id: decodedToken.userId };

For å få TypeScript til å akseptere dette må du utvide type-definisjonen for Express.

Dette er helt standard når man lager:

JWT-auth

Session-auth

API med brukere

Middleware som lagrer noe på req.

KORT FORTALT: .d.ts brukes for å fortelle TypeScript mer informasjon.

Hvordan vet TypeScript om filen?

1. Så lenge den ligger i src mappen blir types/express.d.ts scannet.
2. Man kan legge til i ts.config (compilerOptions) sånn her:
   - "types": [],
   - "typeRoots": ["./node_modules/@types", "./src/types"]

_Jeg hadde ikke problemer på testprosjektet når jeg gjorde det på måte nr.1._

    declare global {

namespace Express {
interface Request {
user?: {
id: number;
};
}
}
}

export {};
