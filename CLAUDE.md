# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Development Commands

- **Start development server**: `npm run dev` (runs on http://localhost:5173)
- **Build for production**: `npm run build`
- **Start production server**: `npm run start`
- **Type checking**: `npm run typecheck` (runs React Router typegen + tsc)

## Architecture Overview

This is an AI-powered resume analyzer built with React Router v7, designed to help users get feedback on their resumes for job applications. The application integrates with Puter.js for cloud storage, authentication, and AI services.

### Core Architecture Components

**Frontend Framework**: React Router v7 with file-based routing
- Server-side rendering enabled
- TailwindCSS v4 for styling
- TypeScript throughout

**State Management**: 
- Zustand store (`usePuterStore`) for managing Puter.js integration
- Handles authentication, file storage, AI services, and key-value storage

**Key Services**:
- **Puter.js Integration**: Cloud platform providing auth, file storage, AI chat, and key-value storage
- **PDF Processing**: Client-side PDF to image conversion using pdfjs-dist
- **Resume Analysis**: AI-powered feedback using Claude Sonnet 4 model

### Route Structure

- `/` - Home page displaying user's uploaded resumes
- `/auth` - Authentication flow with Puter
- `/upload` - Resume upload with PDF processing
- `/resume/:id` - Individual resume analysis view
- `/wipe` - Data deletion utility

### Data Flow

1. **Authentication**: Users authenticate via Puter.js OAuth
2. **File Upload**: PDFs uploaded to Puter cloud storage + converted to images locally
3. **AI Analysis**: Resume images analyzed via Puter AI service (Claude Sonnet 4)
4. **Storage**: Resume metadata and feedback stored in Puter key-value store with pattern `resume:*`
5. **Display**: Structured feedback shown across 5 categories: ATS, tone/style, content, structure, skills

### Key Files & Components

**State Management**:
- `app/lib/puter.ts` - Central Puter.js integration with Zustand store
- `types/puter.d.ts` - Puter API type definitions

**Core Utilities**:
- `app/lib/pdf2img.ts` - Client-side PDF to PNG conversion
- `constants/index.ts` - Resume data types and AI prompt templates

**UI Components**:
- `components/FileUploader.tsx` - Drag & drop PDF upload with react-dropzone
- `components/ResumeCard.tsx` - Resume list item with score display
- `components/ScoreGauge.tsx` - Circular progress indicators
- `components/Accordion.tsx` - Expandable feedback sections
- `components/ATS.tsx` - ATS-specific feedback display

### Data Structures

**Resume Object**:
```typescript
interface Resume {
  id: string;
  companyName?: string;
  jobTitle?: string;
  imagePath: string;    // Path to resume image in Puter storage
  resumePath: string;   // Path to PDF in Puter storage
  feedback: Feedback;   // AI analysis results
}
```

**Feedback Structure**: 5-category scoring system (ATS, toneAndStyle, content, structure, skills) with numerical scores and improvement tips.

### Important Implementation Notes

- **AI Model**: Uses Claude Sonnet 4 via Puter AI service (configured in `app/lib/puter.ts:353`)
- **PDF Processing**: Renders first page only at 4x scale for optimal quality
- **Storage Pattern**: Resume data stored in Puter KV with keys like `resume:{id}`
- **Authentication Flow**: Redirects unauthenticated users to `/auth` with next parameter
- **File Handling**: All resume files stored in Puter cloud, not local filesystem

### Development Notes

- React Router v7 uses file-based routing in `app/routes/`
- TailwindCSS classes are available globally
- All async operations should handle Puter.js availability checks
- Components follow TypeScript strict mode conventions
- PDF worker loaded from public directory (`/pdf.worker.min.mjs`)