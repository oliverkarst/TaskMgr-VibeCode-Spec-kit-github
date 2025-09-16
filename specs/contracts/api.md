# API Contracts

Base URL: /api (Backend)

Endpoints

GET /api/tasks
- Response 200
- Body: [{ id, title, description, completed, createdAt, updatedAt }]

POST /api/tasks
- Request Body: { title: string, description?: string }
- Response 201
- Body: { id, title, description, completed, createdAt, updatedAt }

GET /api/tasks/:id
- Response 200 or 404

PUT /api/tasks/:id
- Request Body: { title?: string, description?: string, completed?: boolean }
- Response 200 or 404

DELETE /api/tasks/:id
- Response 204 or 404

Errors: JSON error object { error: string, details?: any }
