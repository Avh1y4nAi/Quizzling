Overview & Core Requirements

This project is a quiz platform with three user roles: Students, Professors, and an Admin. The system supports quizzes with multiple-correct answers and provides feedback only after a full attempt is submitted. Profiles will be customizable with fields for a bio and social links.

    Frontend: A React application built with Vite and TypeScript. A component library like Material UI is recommended to accelerate development.

    Backend: A Node.js and Express server using a MongoDB database. It is currently in JavaScript, but migrating to TypeScript is a future consideration.

    Authentication: The system will use a standard email/password flow, issuing JSON Web Tokens (JWTs) for session management.

Project Objectives

1. Pages & Dashboards

    Public Access: Create a "Home" and "About" page accessible to everyone.

    Authentication: Implement "Login" and "Register" pages.

    Role-Based Dashboards: Design unique dashboard experiences for Students, Professors, and Admins, showing relevant information and actions for each role.

2. User & Profile Management

    Profile Editing: All users must be able to view and update their own profiles.

    Admin User Control: Admins have full authority to create, view, update, and delete any user account and assign roles.

3. Question Sets & Quizzes

    Admin Privileges: Admins can create, read, update, and delete any question set on the platform.

    Professor Privileges: Professors can create, update, and delete only their own question sets. They can also view the results of any student who has attempted their quizzes.

    Student Experience: Students can attempt quizzes and review their own past results.

4. Quiz Mechanics

    Multiple-Correct Answers: Quizzes must support questions where more than one option can be correct.

    Post-Submission Feedback: Results, including total marks and correct/incorrect counts, are shown only after the entire quiz is submitted. The review should clearly indicate which answers were correct and which were incorrectly selected.

    Simplified Scope: For now, do not implement timers, pagination (one question per page), negative marking, or the ability to resume an incomplete quiz.

Data Models (Database Schema)

Structure your MongoDB collections as follows:

    User:

        Fields: name, email (must be unique), passwordHash, role (one of 'admin', 'professor', 'student'), bio, github_link, twitter_link.

        Include timestamps for creation and updates.

    QuestionSet:

        Fields: title, description, createdBy (a reference to the User who created it), isPublic, and an array of questions.

        Include timestamps.

    Question:

        This will be a sub-document within a QuestionSet.

        Fields: prompt (the question text), an array of options (each with a unique key and text), and an array of correctKeys to support multiple answers.

    Attempt:

        Fields: userId, questionSetId, an array of responses (linking a questionId to the selectedKeys), score, correctCount, and incorrectCount.

        Include a timestamp for when the attempt was made.

Backend Implementation (Node.js)

1. Project Structure

Organize your backend with distinct folders for config, models, middleware, routes, controllers, validators, utils, and seed scripts to maintain a clean architecture.

2. Security & Middleware

    Authentication: Use JWTs passed as Bearer tokens in the Authorization header.

    Password Hashing: Hash all user passwords with bcrypt.

    General Security: Implement helmet for header security and cors to manage cross-origin requests.

    Input Validation: Use a library like Joi or Zod to validate all incoming request bodies to prevent invalid data.

    Role-Based Access Control (RBAC): Create middleware that checks a user's role (admin, professor) before allowing access to protected endpoints. Professors should only be able to modify resources they own (where createdBy matches their user ID).

3. API Endpoints

Design your REST API with clear and logical routes:

    /api/auth/: For user registration and login.

    /api/users/: For admin-only user management (CRUD operations).

    /api/me/: For users to manage their own profiles.

    /api/question-sets/: For all operations related to quizzes. Ensure GET requests are filtered based on the user's role.

    /api/attempts/: For submitting quiz attempts and retrieving results, with access controls based on the user's role.

4. Seeding

Create a script to seed the database with initial data, including one user for each role (admin, professor, student) and a sample quiz to facilitate testing.

Frontend Implementation (React)

1. Project Structure

Organize your React src folder with subdirectories for api, context, routes, pages, components, hooks, styles, and types.

2. State Management

    Use React's Context API to manage global authentication state (user object, token). This will make user data accessible throughout the application.

    For forms, use a library like React Hook Form with Zod for validation to handle complex form states efficiently.

3. UI & Components

    UI Library: Use a component library like Material UI to build the user interface quickly and consistently.

    Routing Guards:

        Create a ProtectedRoute component that redirects unauthenticated users to the login page.

        Create a RoleGuard component to protect routes based on user roles (e.g., ensuring only an 'admin' can access the user management page).

4. Key Components & Logic

    API Client: Set up a centralized axios client that automatically attaches the JWT Bearer token to all outgoing requests.

    Quiz Attempt Page: This component will fetch the quiz questions, manage the state of selected answers (using checkboxes), and handle the submission. After submission, it should display the results, highlighting correct answers in green and incorrectly selected answers in red.

Setup and Deployment

1. Local Setup

    Backend: Initialize a Node.js project, install dependencies (express, mongoose, bcrypt, etc.), set up your .env file with database and JWT secrets, and run the development server with nodemon.

    Frontend: Create a new React project using Vite with the TypeScript template. Install dependencies (axios, react-router-dom, react-hook-form, a UI library), and run the development server.

2. Deployment

    Frontend: Deploy to a static hosting service like Vercel or Netlify.

    Backend: Deploy to a platform-as-a-service like Render or Heroku.

    Database: Use a managed database service like MongoDB Atlas.