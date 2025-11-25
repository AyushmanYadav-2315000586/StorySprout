# StorySprout Viva Preparation Guide

## 🚀 Project Overview

**Project Name:** StorySprout
**Tagline:** Personalized AI Story Generator for Kids
**Core Functionality:** Generates unique, age-appropriate stories based on user inputs (characters, setting, theme) using AI, and allows users to download them as PDFs.

---

## 🧠 Challenges Faced (The "Convincing" Ones)

_These are real-world problems that show you didn't just copy-paste code._

1.  **AI Model Deprecation & API Integration:**

    - _Challenge:_ The initial implementation used Cohere's `generate` endpoint, which was deprecated and started returning 404 errors.
    - _Solution:_ Migrated to the newer `chat` endpoint (`v1/chat`) and updated the payload structure to match the new API requirements. Implemented robust error handling to log specific API status codes instead of generic 500 errors.

2.  **Handling Asynchronous AI Responses:**

    - _Challenge:_ The AI generation process takes time (latency), leading to potential timeouts or a "hanging" UI.
    - _Solution:_ Implemented a loading state in the frontend to give user feedback. On the backend, ensured the timeout settings were sufficient and handled potential API failures gracefully with try-catch blocks.

3.  **CORS (Cross-Origin Resource Sharing) Issues:**

    - _Challenge:_ Since the frontend (Netlify) and backend (Render) are hosted on different domains, browsers blocked requests by default.
    - _Solution:_ Configured the `cors` middleware in Express to explicitly allow the frontend domain (`https://storysproutofficial.netlify.app`) and `localhost` for development.

4.  **Secure Authentication Flow:**

    - _Challenge:_ Integrating Firebase Auth on the frontend while securing backend routes.
    - _Solution:_ Used Firebase for the initial login/signup (handling Google Auth easily) but generated a custom JWT (JSON Web Token) on the backend to manage session persistence and secure API endpoints.

5.  **Prompt Engineering for Consistent Output:**
    - _Challenge:_ The AI sometimes generated stories that were too short, too scary, or ignored the "age" parameter.
    - _Solution:_ Refined the prompt template in the backend to explicitly instruct the model on tone, length, and age-appropriateness (e.g., "Write an engaging story in English for a 5-year-old...").

---

## 📚 Viva Questions (100+)

### 🔹 General & System Design

1.  **What is the architecture of your application?** (Answer: Client-Server architecture using the MERN stack).
2.  **Why did you choose the MERN stack?** (Unified language - JS, JSON everywhere, huge community support).
3.  **How does the frontend communicate with the backend?** (REST API calls using `axios` or `fetch`).
4.  **What is the purpose of `package.json`?** (Manifest file for dependencies, scripts, and project metadata).
5.  **What is the difference between `dependencies` and `devDependencies`?** (Prod vs. Dev tools like nodemon/eslint).
6.  **Explain the flow of data when a user clicks "Generate Story".** (React Form -> API Request -> Node Controller -> Cohere API -> MongoDB Save -> Response -> React Display).
7.  **What is MVC architecture? Did you use it?** (Model-View-Controller. Yes: Mongoose Models, React Views, Express Controllers).
8.  **What is an Environment Variable (`.env`)? Why use it?** (To store secrets like API keys outside the codebase for security).
9.  **What is Git and why is it important?** (Version control, collaboration, history tracking).
10. **What is the difference between `npm` and `npx`?** (Package Manager vs. Package Executor).

### 🔹 Frontend (React + Vite + Tailwind)

11. **Why use Vite instead of Create React App?** (Faster build times, HMR - Hot Module Replacement, native ES modules).
12. **What are React Hooks? Name a few you used.** (`useState` for state, `useEffect` for side effects/data fetching, `useContext` for global state).
13. **What is the Virtual DOM?** (A lightweight copy of the DOM; React compares it with the real DOM to update only changed elements).
14. **How do you handle routing in React?** (`react-router-dom` library).
15. **What is the difference between `Link` and `<a>` tag?** (`Link` handles client-side routing without page refresh; `<a>` triggers a full reload).
16. **Why use Tailwind CSS over normal CSS?** (Utility-first, faster development, no class naming conflicts).
17. **How do you pass data from a parent to a child component?** (Props).
18. **How do you pass data from a child to a parent?** (Callback functions passed as props).
19. **What is State Management?** (Managing data across the app; used Context API or Redux).
20. **How did you handle the "Loading" state during story generation?** (Conditional rendering: `if (loading) showSpinner()`).

### 🔹 Backend (Node.js + Express)

21. **What is Node.js?** (JavaScript runtime built on Chrome's V8 engine).
22. **What is Express.js?** (Web framework for Node.js to simplify routing and middleware).
23. **What is Middleware in Express?** (Functions that execute during the request-response cycle, e.g., `cors`, `express.json`).
24. **Why do we use `express.json()`?** (To parse incoming JSON payloads in request bodies).
25. **What is the difference between `require` and `import`?** (CommonJS vs. ES Modules).
26. **What are the HTTP methods you used?** (GET for fetching, POST for creating/sending data).
27. **What is a Status Code? Give examples.** (200 OK, 201 Created, 400 Bad Request, 401 Unauthorized, 500 Server Error).
28. **How did you handle errors in the backend?** (Try-catch blocks and sending appropriate error responses).
29. **What is `nodemon`?** (Tool that restarts the server automatically on file changes).
30. **How do you secure your API keys?** (Using `dotenv` package and `.gitignore`).

### 🔹 Database (MongoDB + Mongoose)

31. **What is MongoDB?** (NoSQL document-oriented database).
32. **Why NoSQL over SQL for this project?** (Flexible schema, JSON-like documents map well to JS objects).
33. **What is Mongoose?** (ODM - Object Data Modeling library for MongoDB and Node).
34. **What is a Schema?** (Structure definition for the data, e.g., StorySchema).
35. **What is the difference between `find()` and `findOne()`?** (Returns array of docs vs. single doc).
36. **How do you connect Node to MongoDB?** (`mongoose.connect(URI)`).
37. **What is a Primary Key in MongoDB?** (`_id` field, automatically generated).
38. **Did you use any relationships between collections?** (e.g., User has many Stories - referencing User ID in Story model).
39. **What is CRUD?** (Create, Read, Update, Delete).
40. **How does `async/await` help in database operations?** (Handles promises cleanly, avoids callback hell).

### 🔹 AI Integration (Cohere)

41. **Which AI model did you use?** (Cohere Command-R).
42. **What is an API Endpoint?** (A specific URL where an API accepts requests).
43. **What parameters did you send to the AI?** (Prompt, Model, Temperature, Max Tokens).
44. **What is "Temperature" in AI models?** (Controls randomness/creativity; higher = more creative, lower = more deterministic).
45. **How did you construct the prompt?** (String interpolation combining user inputs: "Write a story about [Character] in [Setting]...").
46. **What happens if the AI API is down?** (Backend catches the error and sends a 502/500 response to the frontend).
47. **Why not generate the story on the frontend directly?** (Security - to hide the API key).
48. **What is a Token in LLMs?** (Roughly 3/4 of a word; the unit of text processing).
49. **How do you handle the cost/limits of the API?** (Using a free trial key, handling rate limits if they occur).
50. **Can this project be extended to use OpenAI/Gemini?** (Yes, just change the API call logic in the controller).

### 🔹 Authentication & Deployment

51. **How does Firebase Auth work?** (Handles identity providers like Google, returns a token).
52. **What is a JWT?** (JSON Web Token - used for stateless authentication).
53. **Why did you deploy Frontend and Backend separately?** (Decoupling; Netlify is optimized for static assets, Render for Node processes).
54. **What is "Continuous Deployment"?** (Auto-deploying when code is pushed to GitHub).
55. **How do you verify a user is logged in before saving a story?** (Middleware checks for a valid token in the request headers).

### 🔹 Advanced React & Frontend

56. **What is Prop Drilling and how did you avoid it?** (Passing data through many layers; avoided using Context API or keeping state close to where it's needed).
57. **What is the `useEffect` dependency array?** (Controls when the effect runs; empty array = run once on mount).
58. **Explain the difference between `controlled` and `uncontrolled` components.** (Controlled: React handles state via value/onChange; Uncontrolled: DOM handles state via refs).
59. **What is `localStorage`? Did you use it?** (Browser storage for persisting data like tokens across refreshes).
60. **How would you optimize the performance of your React app?** (Code splitting, lazy loading images, using `useMemo`/`useCallback`).
61. **What is the difference between `export default` and named `export`?** (Default: one per file, can be named anything on import; Named: multiple per file, must use specific name).
62. **What are "Fragments" in React?** (`<>...</>` or `<React.Fragment>`, used to group elements without adding an extra DOM node).
63. **How do you handle 404 Not Found pages?** (A catch-all route `*` in React Router).
64. **What is "Responsive Design"?** (Making the site look good on mobile/tablet/desktop using Media Queries or Tailwind classes like `md:`, `lg:`).
65. **What is the purpose of `key` prop in lists?** (Helps React identify which items have changed/added/removed for efficient updates).

### 🔹 Advanced Backend & Security

66. **What is the Event Loop in Node.js?** (Mechanism that handles asynchronous callbacks, allowing Node to be non-blocking).
67. **What is "Callback Hell" and how did you avoid it?** (Nested callbacks making code unreadable; avoided using Promises and `async/await`).
68. **What is SQL Injection? Is MongoDB vulnerable?** (Malicious SQL code execution. MongoDB is vulnerable to NoSQL Injection if inputs aren't sanitized).
69. **What is XSS (Cross-Site Scripting)?** (Injecting malicious scripts into web pages viewed by others; React escapes content by default to prevent this).
70. **What is CSRF (Cross-Site Request Forgery)?** (Tricking a user into performing actions they didn't intend; prevented using tokens/SameSite cookies).
71. **How would you handle file uploads in this project?** (Using `multer` middleware to handle `multipart/form-data`).
72. **What is Rate Limiting?** (Restricting the number of requests a user can make to prevent abuse/DDoS).
73. **What is the difference between Authentication and Authorization?** (AuthN: Who are you? AuthZ: What are you allowed to do?).
74. **Why is it bad to store passwords in plain text?** (Security risk; if DB is leaked, passwords are exposed. Use hashing like bcrypt).
75. **What is a "RESTful" API?** (API adhering to REST constraints: Stateless, Client-Server, Cacheable, Uniform Interface).

### 🔹 Database & Scalability

76. **What is Indexing in MongoDB?** (Data structure that improves search speed; e.g., indexing `email` field).
77. **What is the difference between SQL and NoSQL scaling?** (SQL: Vertical scaling (bigger server); NoSQL: Horizontal scaling (more servers/sharding)).
78. **What is "Normalization" vs "Denormalization"?** (Normalization: Reducing redundancy; Denormalization: Duplicating data for faster reads).
79. **How would you back up your MongoDB database?** (`mongodump` utility or Atlas automated backups).
80. **What are ACID properties? Does MongoDB support them?** (Atomicity, Consistency, Isolation, Durability. Yes, MongoDB supports multi-document ACID transactions).
81. **What is a "Connection Pool"?** (Cache of database connections maintained so that connections can be reused).
82. **How would you handle a situation where the database is down?** (Implement retry logic and circuit breaker pattern).
83. **What is "Soft Delete"?** (Marking a record as `deleted: true` instead of actually removing it).
84. **Why did you use `mongoose.model()`?** (To create a wrapper around the schema that provides an interface to the database).
85. **What is the difference between `PUT` and `PATCH`?** (PUT: Replace entire resource; PATCH: Update partial resource).

### 🔹 Soft Skills & Project Management

86. **What was the most difficult bug you encountered?** (Explain the API deprecation or CORS issue in detail).
87. **How did you manage your time during this project?** (Prioritized core features (MVP) first, then UI polish).
88. **If you had 2 more weeks, what would you add?** (User profiles, "Save to Library", Social sharing, Voice narration).
89. **How did you test your application?** (Manual testing, Postman for API, Console logs for debugging).
90. **What did you learn from this project?** (Full stack integration, AI prompts, Deployment complexities).
91. **How would you explain this project to a non-technical person?** ("It's like a magic book that writes itself based on what you tell it.").
92. **How do you keep up with new technologies?** (Docs, YouTube, Tech Twitter, building projects).
93. **Why is clean code important?** (Readability, maintainability, easier for others to understand).
94. **What tools did you use for design?** (Figma, or just mental models/sketching).
95. **How did you handle version control conflicts?** (Pull, resolve conflicts manually in VS Code, commit).

### 🔹 Edge Cases & "What Ifs"

96. **What if the user enters offensive words in the prompt?** (Need to implement a content filter/moderation layer before sending to AI).
97. **What if two users generate a story at the exact same time?** (Node.js handles concurrent requests via the Event Loop; they are processed independently).
98. **What if the generated story is too long for the PDF?** (Need to implement pagination or dynamic font sizing in the PDF generator).
99. **How do you handle a slow internet connection on the client side?** (Retry mechanisms, optimistic UI updates).
100.  **What if the API key leaks?** (Revoke it immediately in the dashboard and generate a new one).
