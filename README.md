# 🌱 StorySprout

**Personalized AI Story Generator for Kids**

StorySprout is a magical web application that uses Artificial Intelligence to generate unique, age-appropriate stories for children. By customizing characters, settings, and themes, users can create one-of-a-kind adventures and download them as beautifully formatted PDFs.

---

## ✨ Features

- **AI-Powered Storytelling:** Generates unique stories using Cohere's advanced language models.
- **Customizable Inputs:** Choose characters, settings, themes, and the child's age/gender.
- **PDF Download:** Export generated stories to read offline or print.
- **Secure Authentication:** User login and signup powered by Firebase and JWT.
- **Responsive Design:** Works beautifully on desktops, tablets, and mobile devices.
- **History:** Save and view previously generated stories.

---

## 🛠️ Tech Stack

- **Frontend:** React.js, Vite, Tailwind CSS
- **Backend:** Node.js, Express.js
- **Database:** MongoDB (Mongoose)
- **AI Integration:** Cohere API
- **Authentication:** Firebase Auth + Custom JWT
- **Deployment:** Netlify (Frontend) + Render (Backend)

---

## 🚀 Getting Started

### Prerequisites

- Node.js installed
- MongoDB URI
- Cohere API Key
- Firebase Project Credentials

### Installation

1.  **Clone the repository:**

    ```bash
    git clone https://github.com/yourusername/StorySprout.git
    cd StorySprout
    ```

2.  **Setup Backend:**

    ```bash
    cd backend
    npm install
    # Create .env file with PORT, MONGODB_URI, COHERE_API_KEY, etc.
    npm start
    ```

3.  **Setup Frontend:**
    ```bash
    cd ..
    npm install
    npm run dev
    ```

---

# 🎓 Viva Preparation Guide

_This section is designed to help you answer questions about the project during your viva/presentation._

## 🧠 Key Challenges Faced

1.  **AI Model Deprecation:**
    - _Issue:_ The `generate` API endpoint was deprecated.
    - _Fix:_ Migrated to the `chat` endpoint and updated error handling.
2.  **Async Latency:**
    - _Issue:_ AI takes time to generate text.
    - _Fix:_ Added loading states and timeout handling.
3.  **CORS Errors:**
    - _Issue:_ Frontend and Backend on different domains.
    - _Fix:_ Configured `cors` middleware to allow specific origins.
4.  **Security:**
    - _Issue:_ Protecting API routes.
    - _Fix:_ Implemented JWT verification middleware.

## 📚 Top Viva Questions

### General

- **Architecture:** MERN Stack (Client-Server).
- **MVC:** Used Models (Mongoose), Views (React), Controllers (Express).
- **Env Vars:** Used for security (API keys).

### Frontend

- **Why Vite?** Faster build/HMR than CRA.
- **Hooks Used:** `useState`, `useEffect`, `useContext`.
- **State Management:** Context API for auth state.

### Backend

- **Node.js:** JS Runtime.
- **Express:** Framework for routing/middleware.
- **Middleware:** Functions like `cors`, `express.json` that run before the final handler.

### Database

- **MongoDB:** NoSQL, flexible schema.
- **Mongoose:** ODM for modeling data.
- **CRUD:** Create (POST), Read (GET), Update (PUT), Delete (DELETE).

### AI & Security

- **Model:** Cohere Command-R.
- **Prompt Engineering:** Custom templates to ensure age-appropriate content.
- **JWT:** Stateless authentication token.

_(For the full list of 100+ questions, please refer to the `viva_preparation.md` file included in the documentation)_
