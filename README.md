# TaskSocial API Documentation

Official API documentation for **TaskSocial**, a social accountability application.

The documentation is built with **OpenAPI, Redocly, and Mintlify** and includes an interactive API reference connected to the deployed TaskSocial backend.

## Documentation

**Live Documentation:** https://task-social.mintlify.app

The documentation includes:

- Getting Started guide
- Authentication guide
- Creating Your First Task guide
- API Testing guide
- Interactive API Reference
- Request and response examples
- Authentication and task ownership details

## API

TaskSocial provides a REST API for:

- User registration
- User authentication
- Task creation
- Viewing personal tasks
- Viewing the shared task feed
- Updating tasks
- Deleting tasks
- User logout

### Production API

```text
https://tasksocial-production.up.railway.app
```

API endpoints use the `/api/v1` path.

For example:

```http
POST /api/v1/auth/login
```

## Authentication

TaskSocial uses JWT-based authentication.

After a successful login, the backend creates a JWT and stores it in an HttpOnly `tokenName` cookie.

Protected requests use this cookie for authentication.

```text
Login
   ↓
JWT created
   ↓
HttpOnly tokenName cookie
   ↓
Authenticated request
   ↓
JWT verification
   ↓
Controller
```

The API also checks task ownership when users update or delete tasks.

## Documentation Stack

### OpenAPI

The API is described using an OpenAPI 3.1 specification.

The OpenAPI definition is organized into separate files for better maintainability:

```text
openapi/
├── openapi.yaml
├── components/
│   └── schemas.yaml
└── paths/
    ├── auth.yaml
    └── tasks.yaml
```

The specification is bundled into a single file before being consumed by Mintlify.

### Redocly

Redocly is used to:

- Validate the OpenAPI specification
- Bundle the multi-file specification
- Catch documentation and schema issues

Bundle the specification with:

```bash
npx @redocly/cli bundle openapi.yaml -o openapi-bundled.yaml
```

Validate it with:

```bash
npx @redocly/cli lint openapi-bundled.yaml
```

A successful validation should report that the API description is valid.

### Mintlify

Mintlify is used to build and deploy the developer documentation.

The documentation project contains:

```text
mintlify/
├── docs.json
├── index.mdx
├── openapi-bundled.yaml
└── guides/
    ├── getting-started.mdx
    ├── authentication.mdx
    ├── creating-your-first-task.mdx
    └── api-testing.mdx
```

## Running the Documentation Locally

Clone the repository:

```bash
git clone https://github.com/Shahzebdev/tasksocial-docs.git
cd tasksocial-docs
```

Install the Mintlify CLI if you don't already have it:

```bash
npm install -g mint
```

Check the installed version:

```bash
mint --version
```

### Validate the documentation

From the `mintlify` directory:

```bash
cd mintlify
mint validate
```

### Preview locally

```bash
mint dev
```

The documentation will be available at:

```text
http://localhost:3000
```

## API Playground

The API Reference includes an interactive playground.

The playground is configured to use the deployed TaskSocial API:

```text
https://tasksocial-production.up.railway.app
```

It supports the TaskSocial authentication flow using the `tokenName` HttpOnly cookie.

The main workflow can be tested directly from the documentation:

```text
Register
   ↓
Login
   ↓
Authentication cookie
   ↓
Create task
   ↓
Get tasks
   ↓
Update task
   ↓
Delete task
   ↓
Logout
```

## Guides

### Getting Started

Introduces the API, base URL, available capabilities, and the typical TaskSocial API flow.

### Authentication

Explains registration, login, JWT authentication, HttpOnly cookies, protected endpoints, and task ownership.

### Creating Your First Task

Walks through creating, retrieving, updating, and deleting tasks.

### API Testing

Shows how to test the TaskSocial API using Postman.

## Deployment

The documentation is connected to GitHub and deployed through Mintlify.

The deployment workflow is:

```text
Local documentation changes
        ↓
mint validate
        ↓
Git commit
        ↓
git push
        ↓
GitHub
        ↓
Mintlify
        ↓
Live documentation
```

The live documentation is available at:

```text
https://task-social.mintlify.app
```

## Project Structure

```text
tasksocial-docs/
│
├── mintlify/
│   ├── docs.json
│   ├── index.mdx
│   ├── openapi-bundled.yaml
│   └── guides/
│       ├── getting-started.mdx
│       ├── authentication.mdx
│       ├── creating-your-first-task.mdx
│       └── api-testing.mdx
│
└── openapi/
    ├── openapi.yaml
    ├── redocly.yaml
    ├── openapi-bundled.yaml
    ├── components/
    └── paths/
```

## Development Workflow

When making changes to the API documentation:

```text
Edit OpenAPI / MDX
        ↓
Validate OpenAPI with Redocly
        ↓
Bundle OpenAPI specification
        ↓
Copy updated bundle to Mintlify
        ↓
Run mint validate
        ↓
Preview with mint dev
        ↓
Test the API Playground
        ↓
Commit changes
        ↓
Push to GitHub
```

## What This Project Demonstrates

This documentation project demonstrates practical experience with:

- API documentation
- OpenAPI 3.1
- REST API documentation
- Redocly
- Mintlify
- MDX documentation
- Interactive API references
- JWT authentication documentation
- Cookie-based authentication
- API testing with Postman
- Git and GitHub workflows
- Documentation deployment
- Developer experience

## License

This project is currently licensed under the terms defined in the repository.
