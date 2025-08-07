# AI Resume Analyzer

An intelligent resume analysis platform that provides AI-powered feedback to help you optimize your resume for job applications. Get detailed insights on ATS compatibility, content quality, structure, and more.

## Features

- 🤖 **AI-Powered Analysis** - Comprehensive resume feedback using Claude Sonnet 4
- 📄 **PDF Processing** - Upload PDF resumes and get visual analysis
- 🎯 **ATS Optimization** - Check how well your resume passes Applicant Tracking Systems
- 📊 **Detailed Scoring** - Get scored feedback across 5 key categories
- ☁️ **Cloud Integration** - Secure storage and processing via Puter.js
- 🔒 **Authentication** - Secure user accounts and data management
- 🚀 **Modern Stack** - React Router v7, TypeScript, TailwindCSS

## How It Works

1. **Upload Your Resume** - Drop in your PDF resume for analysis
2. **AI Analysis** - Our AI examines your resume across multiple dimensions
3. **Get Feedback** - Receive detailed scores and improvement suggestions
4. **Track Progress** - View all your resume submissions and track improvements

## Getting Started

### Prerequisites

- Node.js 18+ 
- A Puter.js account for cloud services

### Installation

Install the dependencies:

```bash
npm install
```

### Development

Start the development server:

```bash
npm run dev
```

The application will be available at `http://localhost:5173`.

## Available Commands

- `npm run dev` - Start development server
- `npm run build` - Build for production  
- `npm run start` - Start production server
- `npm run typecheck` - Run TypeScript checks

## Analysis Categories

The AI provides feedback across five key areas:

- **ATS Compatibility** - How well your resume works with tracking systems
- **Content Quality** - Relevance and impact of your experience
- **Structure & Format** - Organization and visual hierarchy  
- **Tone & Style** - Professional language and communication
- **Skills Alignment** - Technical and soft skills presentation

## Technology Stack

- **Frontend**: React Router v7 with TypeScript
- **Styling**: TailwindCSS v4
- **State Management**: Zustand
- **PDF Processing**: PDF.js
- **Cloud Services**: Puter.js (storage, auth, AI)
- **AI Model**: Claude Sonnet 4

## Deployment

### Docker Deployment

```bash
docker build -t ai-resume-analyzer .
docker run -p 3000:3000 ai-resume-analyzer
```

### Production Build

```bash
npm run build
npm run start
```

The app includes server-side rendering and is production-ready out of the box.
