# Introduction
In order to have a better experience and learning. Do not binge all parts of the courses. Instead do some parts, then take a break before continuing. 

These should not be idle breaks. Instead, work on projects utilizing all that you have learned from completed parts.

The following section shows an example plan for enrolling the course that you can follow.

# Course Plan
### Milestone 1: The Core Foundation
**Complete:** Parts 0 – 3 
**Concepts Acquired:** React fundamentals, Node.js, Express REST APIs, MongoDB. 
**Action:** Build a monolithic CRUD application.
- **Project Idea:** A web-based configuration or snippet manager. Users can create, read, update, and delete configuration files or code snippets. Focus purely on data flow between the React frontend and the Express backend.

### Milestone 2: Security and Quality Assurance
**Complete:** Parts 4 – 5 
**Concepts Acquired:** Backend/Frontend testing (Jest, Cypress/Playwright), JWT Authentication, React Router. 
**Action:** Build a multi-user, tested application.
- **Project Idea:** An issue tracker or a secure task management board. Implement user registration, login, and secure routes. Write unit tests for your API endpoints and end-to-end tests to verify the login and task creation workflows.

### Milestone 3: Complex Client Architecture
**Complete:** Parts 6 – 7 
**Concepts Acquired:** Redux, React Query, Context API, Custom Hooks. 
**Action:** Build a state-heavy frontend application.
- **Project Idea:** A system dashboard or resource monitor interface. The UI should require complex state synchronization (e.g., filtering, sorting, and updating multiple data widgets simultaneously) without passing props down deeply nested component trees. Utilize custom hooks to abstract the logic.

### Milestone 4: Paradigm Shifts in Data and Typing
**Complete:** Parts 8 – 9 
**Concepts Acquired:** GraphQL, TypeScript. 
**Action:** Build a strongly typed, graph-based service.
- **Project Idea:** A comprehensive inventory or hardware tracking system. Use TypeScript across the entire stack for end-to-end type safety. Replace the standard REST API with a GraphQL endpoint to allow the frontend to request specifically tailored data payloads, optimizing network payload size.

### Milestone 5: Infrastructure and Automation
**Complete:** Parts 11 – 12 
**Concepts Acquired:** CI/CD pipelines (GitHub Actions), Docker, Containerization. _(Note: Part 10, React Native, can be treated as an optional side quest if you specifically want to explore mobile development)._ 
**Action:** Implement professional deployment workflows for an existing project.
- **Project Idea:** Take the application you built in Milestone 4. Write `Dockerfile` and `docker-compose.yml` configurations to containerize the frontend, backend, and database. Set up a GitHub Actions pipeline that automatically runs your tests, builds the containers, and pushes the images upon every commit.
    

### Milestone 6: Relational Systems and SSR
**Complete:** Parts 13 – 14 
**Concepts Acquired:** PostgreSQL, Sequelize (ORM), Next.js (Server-Side Rendering / App Router). 
**Action:** Build a modern, SEO-friendly, relational web application.
- **Project Idea:** A technical documentation hub or a developer blog platform. Design a normalized relational database schema in PostgreSQL (e.g., Users, Posts, Tags, Comments with proper foreign key constraints). Build the frontend using Next.js to leverage server-side rendering for optimal load times and route protection.