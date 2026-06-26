# 🗣️ Speech Therapy — Interactive App (Backend)

A REST API for a **gamified speech-therapy platform**. Children (patients) complete daily
practice *missions* and earn points; speech therapists track each patient's progress, set goals
and leave notes. Built with **Node.js, Express and MongoDB**, with JWT authentication and
role-based access control.

![Node](https://img.shields.io/badge/Node.js-18+-339933?logo=node.js&logoColor=white)
![Express](https://img.shields.io/badge/Express-4-000000?logo=express&logoColor=white)
![MongoDB](https://img.shields.io/badge/MongoDB-Mongoose-47A248?logo=mongodb&logoColor=white)
![JWT](https://img.shields.io/badge/Auth-JWT-FB015B?logo=jsonwebtokens&logoColor=white)
![License](https://img.shields.io/badge/license-MIT-blue)

> UI mockups are in Portuguese (see [`docs/screenshots`](docs/screenshots)); code, API and docs are in English.

---

## ✨ Features

- **Authentication & roles** — register/login with JWT; three roles: `patient`, `therapist`, `admin`.
  Patients link to a therapist via a `therapistCode`.
- **Missions** — therapists create exercises and schedule **daily missions**; patients start and
  submit them.
- **Progress & gamification** — submissions feed each patient's progress and a points-based
  **ranking** (daily/weekly).
- **Therapist dashboard** — list patients, view detailed progress, add clinical notes and set goals.
- **Security** — password hashing (bcryptjs), input validation (express-validator), auth + role
  middleware guarding every protected route.

## 🧱 Architecture (layered)

```
server.js
  └─ src/
     ├─ config/        database connection (Mongoose)
     ├─ routes/        HTTP routes  → controllers
     ├─ controllers/   request handling / orchestration
     ├─ models/        Mongoose schemas (User, Mission, DailyMission, PatientProgress, …)
     ├─ middlewares/   auth (JWT) + role-based authorization
     └─ service/       domain logic (ranking)
```

## 🔌 API reference

**Auth** — `/api/auth`
| Method | Endpoint | Access |
|--------|----------|--------|
| `POST` | `/therapist/register` | public |
| `POST` | `/patient/register` | public |
| `POST` | `/login` | public |
| `GET` | `/profile` | authenticated |

**Missions** — `/api/missions`
| Method | Endpoint | Access |
|--------|----------|--------|
| `GET` | `/` | public |
| `GET` | `/daily` | authenticated |
| `POST` | `/start`, `/submit` | patient |
| `POST` | `/`, `/schedule` | therapist / admin |

**Progress** — `/api/progress`
| Method | Endpoint | Access |
|--------|----------|--------|
| `GET` | `/my-progress` | patient |
| `GET` | `/ranking` | authenticated |
| `GET` | `/therapist/stats` | therapist / admin |

**Therapist** — `/api/therapist`
| Method | Endpoint | Access |
|--------|----------|--------|
| `GET` | `/patients` | therapist / admin |
| `GET` | `/patients/:patientId/progress` | therapist / admin |
| `PUT` | `/patients/notes`, `/patients/goals` | therapist / admin |

## 🚀 Getting started

**Prerequisites:** Node.js 18+ and a running MongoDB instance.

```bash
cd speech-therapy-backend
npm install

cp .env.example .env          # set MONGODB_URI and JWT_SECRET

# optional: seed sample data
node databasescript.js

npm run dev                   # http://localhost:3000
```

### Environment

| Variable | Description |
|----------|-------------|
| `PORT` | HTTP port (default 3000) |
| `MONGODB_URI` | MongoDB connection string |
| `JWT_SECRET` | secret used to sign JWTs |

## 🖼️ Interface

UI concepts (Figma) live in [`docs/screenshots`](docs/screenshots).

## 🛠️ Tech stack

**Backend** · Node.js · Express · Mongoose/MongoDB · JWT · bcryptjs · express-validator ·
layered architecture (routes / controllers / services / models / middlewares)

## 🗺️ Roadmap

- [ ] Frontend client (React) wired to this API
- [ ] Audio capture for speech exercises (API key hooks already stubbed)
- [ ] Automated tests (Jest + supertest)
- [ ] OpenAPI/Swagger spec

---

<sub>Backend project to practise REST API design, authentication/authorization and MongoDB data modelling.</sub>
