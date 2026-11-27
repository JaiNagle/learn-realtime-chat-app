# Realtime Chat App (MERN + Socket.IO)

A real-time one-to-one chat application built with the MERN stack and **Socket.IO**, following the AsAProgrammer YouTube tutorial. It supports authentication, image messages, live online presence and switchable themes.

## Features

- Sign up, log in and log out with JWT authentication stored in HTTP cookies
- Real-time messaging over WebSockets
- Live online/offline user indicators
- Send images in messages and update your profile picture (uploaded to Cloudinary)
- Theme picker (DaisyUI themes), remembered in the browser via localStorage
- Loading skeletons and toast notifications
- Seed script for creating sample users

## Tech stack

| Layer | Tools |
| --- | --- |
| Frontend | React 19, Vite, Tailwind CSS, DaisyUI, Zustand, Axios, React Router, lucide-react |
| Backend | Node.js, Express, Socket.IO, JWT, bcryptjs |
| Database / storage | MongoDB (Mongoose), Cloudinary |

## Getting started

### Prerequisites

Node.js 18+, a MongoDB database and a Cloudinary account.

### Environment

Create `backend/.env`:

```
PORT=5001   # the frontend expects the API on 5001 in development
MONGODB_URI=<your mongodb connection string>
JWT_SECRET=<long random string>
NODE_ENV=development

CLOUDINARY_CLOUD_NAME=<name>
CLOUDINARY_API_KEY=<key>
CLOUDINARY_API_SECRET=<secret>
```

### Install and run

```bash
npm install --prefix backend
npm install --prefix frontend

npm run dev --prefix backend    # API + Socket.IO
npm run dev --prefix frontend   # Vite dev server (second terminal)
```

### Production

```bash
npm run build
npm start
```

### Optional: seed sample users

```bash
node backend/src/seeds/user.seed.js
```

## API

Auth routes (`/api/auth`): `POST /signup`, `POST /login`, `POST /logout`, `PUT /update-profile`, `GET /check`.

Message routes (`/api/messages`): `GET /users` (sidebar list), `GET /:id` (conversation), `POST /send/:id`.

All routes except signup, login and logout require the auth cookie. Socket.IO broadcasts a `getOnlineUsers` event whenever someone connects or disconnects.

## Project structure

```
.
├── backend/src/
│   ├── controllers/   # auth + message logic
│   ├── lib/           # db, socket, cloudinary, token utils
│   ├── middleware/    # auth guard
│   ├── models/        # User, Message
│   ├── routes/
│   └── seeds/
└── frontend/src/
    ├── components/    # chat UI + skeletons
    ├── pages/         # Home, Login, SignUp, Profile, Settings
    └── store/         # Zustand stores (auth, chat, theme)
```

## Credits

Built while following the AsAProgrammer tutorial as a way to learn WebSockets and full-stack auth.
