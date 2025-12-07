# Node Express API Starter

A production-ready REST API starter built with Node.js, Express, and PostgreSQL. Features authentication, authorization, security middleware, and comprehensive development tooling.

## Features

- **Authentication & Authorization**: JWT-based authentication with role-based access control (RBAC)
- **Database**: PostgreSQL with Drizzle ORM and Neon serverless database
- **Security**: Helmet, CORS, rate limiting with Arcjet, and cookie-based token management
- **Logging**: Winston for structured logging and Morgan for HTTP request logs
- **Validation**: Zod schema validation for request payloads
- **Code Quality**: ESLint, Prettier, and Jest for testing
- **DevOps**: Docker support with separate dev/prod configurations, GitHub Actions CI/CD
- **Development**: Hot reload, database migrations, and local development with Neon Local

## Tech Stack

- **Runtime**: Node.js 20.x
- **Framework**: Express 5.x
- **Database**: PostgreSQL (Neon Serverless)
- **ORM**: Drizzle ORM
- **Authentication**: JWT (jsonwebtoken)
- **Security**: Helmet, Arcjet, bcrypt
- **Validation**: Zod
- **Testing**: Jest
- **Logging**: Winston, Morgan
- **Docker**: Multi-stage builds with Docker Compose

## Prerequisites

- Node.js 20.x or higher
- npm or yarn
- Docker and Docker Compose (for containerized development)
- PostgreSQL (or use Neon cloud database)

## Getting Started

### 1. Clone the repository

```bash
git clone https://github.com/shashank-amireddy/node-express-api-starter.git
cd node-express-api-starter
```

### 2. Install dependencies

```bash
npm install
```

### 3. Environment Setup

Create environment files based on the examples:

```bash
cp .env.example .env
cp .env.example .env.development
cp .env.example .env.production
```

Update the environment variables:

**`.env` (for local development without Docker):**
```env
NODE_ENV=development
PORT=3000
LOG_LEVEL=info

DATABASE_URL=postgresql://user:password@localhost:5432/dbname

JWT_SECRET=your_jwt_secret_key
ARCJET_KEY=your_arcjet_key
```

**`.env.development` (for Docker development):**
```env
NODE_ENV=development
DATABASE_URL=postgresql://neon:npg@neon-local:5432/neondb
# Add Neon project details if using Neon Local
```

### 4. Database Setup

Run database migrations:

```bash
npm run db:migrate
```

Generate new migrations after schema changes:

```bash
npm run db:generate
```

Open Drizzle Studio to manage your database:

```bash
npm run db:studio
```

## Development

### Local Development (without Docker)

```bash
npm run dev
```

The API will be available at `http://localhost:3000`

### Docker Development (with Neon Local)

```bash
npm run dev:docker
```

This starts:
- Neon Local proxy for ephemeral database branches
- Application with hot reload enabled

### Production Build (Docker)

```bash
npm run prod:docker
```

## API Endpoints

### Authentication

- `POST /api/auth/sign-up` - Register a new user
- `POST /api/auth/sign-in` - Login and receive JWT token
- `POST /api/auth/sign-out` - Logout

### Users

- `GET /api/users` - Get all users (authenticated)
- `GET /api/users/:id` - Get user by ID (authenticated)
- `PUT /api/users/:id` - Update user (authenticated)
- `DELETE /api/users/:id` - Delete user (admin only)

### Health & Status

- `GET /` - Root endpoint
- `GET /health` - Health check endpoint
- `GET /api` - API root endpoint

## Testing

Run tests:

```bash
npm test
```

Run tests in watch mode:

```bash
npm run test:watch
```

## Code Quality

### Linting

```bash
npm run lint          # Check for linting issues
npm run lint:fix      # Auto-fix linting issues
```

### Formatting

```bash
npm run format        # Format code with Prettier
npm run format:check  # Check if code is formatted
```

## Project Structure

```
├── .github/
│   └── workflows/           # GitHub Actions CI/CD pipelines
├── drizzle/                 # Database migrations
├── scripts/                 # Development and deployment scripts
├── src/
│   ├── config/             # Configuration files (database, logging, etc.)
│   ├── controllers/        # Request handlers
│   ├── middleware/         # Custom middleware (auth, security)
│   ├── models/             # Database models (Drizzle schemas)
│   ├── routes/             # API route definitions
│   ├── services/           # Business logic layer
│   ├── utils/              # Utility functions
│   ├── validations/        # Zod validation schemas
│   ├── app.js              # Express app configuration
│   ├── server.js           # Server entry point
│   └── index.js            # Application entry point
├── tests/                   # Test files
├── docker-compose.dev.yml   # Docker Compose for development
├── docker-compose.prod.yml  # Docker Compose for production
├── Dockerfile               # Multi-stage Docker build
├── drizzle.config.js        # Drizzle ORM configuration
└── package.json             # Project dependencies and scripts
```

## Security Features

- **Helmet**: Secure HTTP headers
- **CORS**: Cross-Origin Resource Sharing configuration
- **Rate Limiting**: Role-based rate limits with Arcjet
  - Admin: 20 requests/minute
  - User: 10 requests/minute
  - Guest: 5 requests/minute
- **JWT**: Secure token-based authentication
- **bcrypt**: Password hashing
- **Input Validation**: Zod schema validation

## Environment Variables

| Variable | Description | Required |
|----------|-------------|----------|
| `NODE_ENV` | Environment (development/production) | Yes |
| `PORT` | Server port | Yes |
| `DATABASE_URL` | PostgreSQL connection string | Yes |
| `JWT_SECRET` | Secret key for JWT signing | Yes |
| `ARCJET_KEY` | Arcjet API key for rate limiting | Yes |
| `LOG_LEVEL` | Logging level (info/debug/error) | No |

## CI/CD

The project includes GitHub Actions workflows:

- **Tests**: Runs on push and PR to main/staging
- **Lint & Format**: Code quality checks
- **Docker Build**: Builds and pushes Docker images

## Docker

### Development with Docker

Uses Neon Local for ephemeral database branches:

```bash
docker compose -f docker-compose.dev.yml up
```

### Production with Docker

```bash
docker compose -f docker-compose.prod.yml up -d
```

### Build Docker image manually

```bash
docker build -t node-express-api:latest .
```

## Contributing

1. Fork the repository
2. Create a feature branch (`git checkout -b feature/amazing-feature`)
3. Commit your changes (`git commit -m 'Add amazing feature'`)
4. Push to the branch (`git push origin feature/amazing-feature`)
5. Open a Pull Request

## License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

## Acknowledgments

- Built with [Express](https://expressjs.com/)
- Database powered by [Neon](https://neon.tech/)
- ORM by [Drizzle](https://orm.drizzle.team/)
- Security by [Arcjet](https://arcjet.com/)
