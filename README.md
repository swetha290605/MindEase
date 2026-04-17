# 🧠 MindEase

> AI-powered mental wellness journaling and mood tracking platform

MindEase helps users track their emotional wellbeing through daily mood check-ins, guided journaling, and AI-generated insights — available on mobile (React Native) and web.

---

## 📁 Project Structure

```
mindease/
├── frontend-mobile/        React Native + Expo mobile app
├── frontend-web/           React.js web dashboard
├── backend/                Node.js REST API (Express + Prisma)
├── infra/                  AWS CDK Infrastructure-as-Code
├── docs/                   Architecture diagrams & OpenAPI spec
├── Dockerfile              Backend API Docker image
├── docker-compose.yml      Local development orchestration
└── .github/workflows/      GitHub Actions CI/CD
```

---

## 🚀 Quick Start (Local Dev)

### Prerequisites
- Node.js 20+
- Docker & Docker Compose
- Expo CLI (`npm install -g expo-cli`)
- AWS CLI (for infra work)

### 1. Clone & install dependencies

```bash
git clone https://github.com/your-org/mindease.git
cd mindease

# Backend
cd backend && npm install && cd ..

# Frontend Web
cd frontend-web && npm install && cd ..

# Frontend Mobile
cd frontend-mobile && npm install && cd ..
```

### 2. Configure environment variables

```bash
cp backend/.env.example backend/.env
# Edit backend/.env with your values
```

### 3. Start local services

```bash
docker-compose up -d
```

This starts:
- PostgreSQL on `localhost:5432`
- Redis on `localhost:6379`
- Backend API on `localhost:3001`
- Frontend Web on `localhost:3000`

### 4. Run database migrations

```bash
cd backend
npx prisma migrate dev
npx prisma db seed
```

### 5. Start mobile app

```bash
cd frontend-mobile
npx expo start
```

---

## 🧪 Testing

```bash
# Backend unit + functional tests
cd backend && npm test

# Backend with coverage
cd backend && npm run test:coverage

# Frontend web
cd frontend-web && npm test
```

---

## 🏗️ Infrastructure (AWS CDK)

```bash
cd infra
npm install
cdk bootstrap
cdk deploy --all
```

Deploys:
- ECS Fargate cluster + task definitions
- RDS PostgreSQL (Multi-AZ)
- CodePipeline CI/CD pipeline
- VPC, ALB, Route53, ACM

---

## 📖 API Documentation

See [`docs/openapi.yaml`](docs/openapi.yaml) for the full OpenAPI 3.0 spec.

Run locally with Swagger UI:

```bash
docker run -p 8080:8080 -e SWAGGER_JSON=/api/openapi.yaml \
  -v $(pwd)/docs:/api swaggerapi/swagger-ui
```

Then open http://localhost:8080

---

## 🔐 Environment Variables

| Variable | Description | Required |
|---|---|---|
| `DATABASE_URL` | PostgreSQL connection string | ✅ |
| `REDIS_URL` | Redis connection string | ✅ |
| `JWT_SECRET` | Secret for JWT signing | ✅ |
| `OPENAI_API_KEY` | OpenAI API for AI insights | ✅ |
| `AWS_REGION` | AWS region for deployments | ✅ |
| `PORT` | API server port (default: 3001) | ❌ |

---

## 📄 License

MIT © MindEase Team
