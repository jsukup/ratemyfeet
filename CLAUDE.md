# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

RateMyFeet is a Next.js application being transformed from an AI-powered facial attractiveness analyzer to a user-driven rating platform for foot images. The application features:

- **Frontend**: Next.js with TypeScript, Tailwind CSS, and Radix UI components
- **Backend**: Next.js API routes for user rating system
- **Storage**: Supabase for database, user data, and image storage
- **Rating System**: User-generated ratings with median score calculations
- **Deployment**: Vercel for full-stack hosting

## Common Commands

### Frontend Development
```bash
npm run dev          # Start development server
npm run build        # Build for production
npm run start        # Start production server
npm run lint         # Run ESLint
npm run clean        # Clean node_modules cache
```

### Testing (Legacy - will be updated)
```bash
npm run test:replicate          # Test Replicate API integration (deprecated)
node scripts/test-ensemble-api.js  # Test ensemble API (deprecated)
```

## Architecture Overview

### Current State (Deprecated)
The codebase currently contains AI/ML components that are being removed, including:
- Replicate API integration
- TensorFlow.js models and inference
- Face detection and analysis
- AI scoring systems
- Python FastAPI backend

### Target Architecture (TaskMaster Plan)
The application is being transformed to include:

#### Database Schema
- **ratings table**: Stores user ratings (0-10 scale) with session tracking
- **images table**: Updated to store median scores and rating counts
- **users table**: Username management and validation

#### Core Components
- **RatingSlider**: Interactive 0-10 rating component with decimal precision
- **ImageCapture**: Simplified webcam capture without face detection
- **Leaderboard**: User-generated rating display with categories
- **UsernameInput**: Real-time username validation

#### API Endpoints
- `/api/ratings/submit`: Handle rating submissions with validation
- Rating aggregation and median calculation utilities
- Session management and duplicate prevention

### Key Features Being Implemented

1. **User Rating System**: 0-10 scale ratings with 0.01 precision
2. **Session Management**: Prevent duplicate ratings per session
3. **Rate Limiting**: IP-based daily limits (50 ratings/day)
4. **Leaderboard Categories**: Ranked tiers ("Smoke Shows", "Monets", "Mehs", "Plebs", "Dregs")
5. **Performance Optimization**: Lazy loading and image caching
6. **Branding Update**: Complete rebrand from "looxmaxx" to "RateMyFeet"

### Data Flow (New System)
1. User captures foot image via webcam
2. Username validation and image upload to Supabase
3. Other users rate images on 0-10 scale
4. Median scores calculated and leaderboard updated
5. Images categorized into ranking tiers

### Environment Variables
- `NEXT_PUBLIC_SUPABASE_URL`: Supabase project URL
- `NEXT_PUBLIC_SUPABASE_ANON_KEY`: Supabase anonymous key
- Database connection variables for rating system

### Important Files
- `vercel.json`: Vercel deployment configuration
- `package.json`: Frontend dependencies (AI packages being removed)
- `components.json`: Shadcn/ui component configuration
- `tailwind.config.ts`: Tailwind CSS configuration with new branding colors

## Development Notes

### Concurrent Development Workflow

When working on tasks across multiple worktrees, follow this workflow:

#### Task Completion Protocol
1. **Complete the assigned task** according to task specifications
2. **Test thoroughly** - ensure build passes and functionality works
3. **Stage all changes**: `git add .`
4. **Commit with detailed message** following this format:
   ```
   Task [N] Complete: [Brief description]
   
   - [Key change 1]
   - [Key change 2]
   - [Key change 3]
   
   🤖 Generated with [Claude Code](https://claude.ai/code)
   
   Co-Authored-By: Claude <noreply@anthropic.com>
   ```
5. **Push to GitHub**: `git push -u origin [branch-name]`
6. **Create Pull Request** (optional for review)
7. **Update task status** in TodoWrite
8. **Move to next priority task**

#### Worktree Status
- ✅ **ratemyfeet-cleanup** (Task 1) - **COMPLETED & PUSHED**
- ✅ **ratemyfeet-database** (Task 2) - **COMPLETED & PUSHED** 
- ⬜ **ratemyfeet-rating** (Tasks 3-6) - Ready to start (depends on Task 2)
- ⬜ **ratemyfeet-users** (Tasks 7-10) - Depends on Tasks 3-6
- ⬜ **ratemyfeet-branding** (Task 11) - Can run in parallel
- ⬜ **ratemyfeet-errors** (Task 12) - Final integration work

### TaskMaster Implementation Plan
The codebase is being updated through Claude TaskMaster with 12 main tasks:
1. Remove AI/ML dependencies and components
2. Update database schema for user ratings
3. Implement rating slider component
4. Create rating submission APIs
5. Implement median score calculations
6. Update leaderboard for user ratings
7. Add username validation system
8. Update image capture workflow
9. Implement session management
10. Add performance optimizations
11. Complete branding update to RateMyFeet
12. Add comprehensive error handling

### Current Development Status
- **State**: Deprecated codebase with AI components
- **Target**: User-driven rating platform
- **Migration**: In progress via TaskMaster automation

### Important Notes for Development
- All AI/ML related code should be considered deprecated
- Focus on user rating system implementation
- Maintain existing Supabase integration patterns
- Ad integration patterns should be preserved
- Performance optimizations are critical for leaderboard scalability