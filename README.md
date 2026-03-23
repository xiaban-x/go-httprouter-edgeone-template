# Go Cloud Functions on EdgeOne Pages - HttpRouter Framework

A full-stack demo application built with Next.js + Tailwind CSS frontend and Go HttpRouter backend, showcasing how to deploy Go Cloud Functions using the HttpRouter package on EdgeOne Pages with RESTful API routing.

## 🚀 Features

- **HttpRouter Integration**: Blazing fast, zero-allocation HTTP router with named parameters and catch-all routes
- **Modern UI Design**: Dark theme with #1c66e5 accent color, responsive layout with interactive elements
- **Interactive API Testing**: Built-in API endpoint panel — click "Call" to test each REST endpoint in real-time
- **RESTful API Design**: Complete Todo CRUD operations with clean route definitions (`/api/todos`)
- **TypeScript Support**: Complete type definitions and type safety on the frontend

## 🛠️ Tech Stack

### Frontend
- **Next.js 15** - React full-stack framework (with Turbopack)
- **React 19** - User interface library
- **TypeScript** - Type-safe JavaScript
- **Tailwind CSS 4** - Utility-first CSS framework

### UI Components
- **shadcn/ui** - High-quality React components
- **Lucide React** - Beautiful icon library
- **class-variance-authority** - Component style variant management
- **clsx & tailwind-merge** - CSS class name merging utilities

### Backend
- **Go 1.21** - Cloud Functions runtime
- **HttpRouter v1.3** - High-performance, zero-allocation HTTP router for Go

## 📁 Project Structure

```
go-httprouter/
├── cloud-functions/                # Go Cloud Functions source
│   ├── api.go                     # HttpRouter app with all REST API routes
│   ├── go.mod                     # Go module definition
│   └── go.sum                     # Go dependency checksums
├── src/
│   ├── app/                       # Next.js App Router
│   │   ├── globals.css           # Global styles (dark theme)
│   │   ├── layout.tsx            # Root layout
│   │   └── page.tsx              # Main page (API testing UI)
│   ├── components/               # React components
│   │   └── ui/                   # UI base components
│   │       ├── button.tsx        # Button component
│   │       └── card.tsx          # Card component
│   └── lib/                      # Utility functions
│       └── utils.ts              # Common utilities (cn helper)
├── public/                        # Static assets
│   ├── eo-logo-blue.svg          # EdgeOne logo (blue)
│   └── eo-logo-white.svg         # EdgeOne logo (white)
├── package.json                   # Project configuration
└── README.md                     # Project documentation
```

## 🚀 Quick Start

### Requirements

- Node.js 18+
- pnpm (recommended) or npm
- Go 1.21+ (for local development)

### Install Dependencies

```bash
pnpm install
# or
npm install
```

### Development Mode

```bash
edgeone pages dev
```

Visit [http://localhost:8088](http://localhost:8088) to view the application.

### Build Production Version

```bash
edgeone pages build
```

## 🎯 Core Features

### 1. HttpRouter REST API Routes

All API endpoints are defined in a single `cloud-functions/api.go` file using HttpRouter's explicit method routing:

| Method | Route | Description |
|--------|-------|-------------|
| GET | `/` | Welcome message with route list |
| GET | `/health` | Health check |
| GET | `/api/todos` | List all todos |
| POST | `/api/todos` | Create a new todo |
| GET | `/api/todos/:id` | Get todo by ID |
| PATCH | `/api/todos/:id/toggle` | Toggle todo completion |
| DELETE | `/api/todos/:id` | Delete a todo |

### 2. Interactive API Testing Panel

- 7 pre-configured API endpoint cards with "Call" buttons
- Real-time JSON response display with syntax highlighting
- POST request support with pre-filled JSON body
- Loading states and error handling

### 3. HttpRouter Framework Convention

The Go backend uses HttpRouter's standard patterns — explicit method routing and named parameters:

```go
package main

import (
    "github.com/julienschmidt/httprouter"
    "net/http"
    "encoding/json"
)

func main() {
    router := httprouter.New()

    router.GET("/health", func(w http.ResponseWriter, r *http.Request, _ httprouter.Params) {
        w.Header().Set("Content-Type", "application/json")
        json.NewEncoder(w).Encode(map[string]string{
            "status":    "ok",
            "framework": "httprouter",
        })
    })

    router.GET("/api/todos", listTodos)
    router.POST("/api/todos", createTodo)
    router.GET("/api/todos/:id", getTodo)
    router.PATCH("/api/todos/:id/toggle", toggleTodo)
    router.DELETE("/api/todos/:id", deleteTodo)

    http.ListenAndServe(":9000", router)
}
```

### 4. Data Model

```go
type Todo struct {
    ID        int       `json:"id"`
    Title     string    `json:"title"`
    Completed bool      `json:"completed"`
    CreatedAt time.Time `json:"createdAt"`
}
```

## 🔧 Configuration

### Tailwind CSS Configuration
The project uses Tailwind CSS 4 with custom color variables:

```css
:root {
  --primary: #1c66e5;        /* Primary color */
  --background: #000000;     /* Background color */
  --foreground: #ffffff;     /* Foreground color */
}
```

### Component Styling
Uses `class-variance-authority` to manage component style variants with multiple preset styles.

## 📚 Documentation

- **EdgeOne Pages Official Docs**: [https://edgeone.ai/document/go-functions](https://edgeone.ai/document/go-functions)
- **HttpRouter**: [https://github.com/julienschmidt/httprouter](https://github.com/julienschmidt/httprouter)
- **Next.js Documentation**: [https://nextjs.org/docs](https://nextjs.org/docs)
- **Tailwind CSS Documentation**: [https://tailwindcss.com/docs](https://tailwindcss.com/docs)

## 🚀 Deployment Guide

### EdgeOne Pages Deployment

1. Push code to GitHub repository
2. Create new project in EdgeOne Pages console
3. Select GitHub repository as source
4. Configure build command: `edgeone pages build`
5. Deploy project

### Go HttpRouter Cloud Function

Create `cloud-functions/api.go` in project root with your HttpRouter application:

```go
package main

import (
    "github.com/julienschmidt/httprouter"
    "encoding/json"
    "net/http"
)

func main() {
    router := httprouter.New()

    router.GET("/hello", func(w http.ResponseWriter, r *http.Request, _ httprouter.Params) {
        w.Header().Set("Content-Type", "application/json")
        json.NewEncoder(w).Encode(map[string]string{
            "message": "Hello from HttpRouter on EdgeOne Pages!",
        })
    })

    http.ListenAndServe(":9000", router)
}
```

## Deploy

[![Deploy with EdgeOne Pages](https://cdnstatic.tencentcs.com/edgeone/pages/deploy.svg)](https://edgeone.ai/pages/new?from=github&template=go-httprouter)

## 📄 License

This project is licensed under the MIT License - see the [LICENSE](https://github.com/github/choosealicense.com/blob/gh-pages/_licenses/mit.txt) file for details.
