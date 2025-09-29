# [- VT HACKS 13 WINNER [CoStar Group] -](https://vthacks-13.devpost.com/submissions/search?utf8=%E2%9C%93&prize_filter%5Bprizes%5D%5B%5D=90730)

# SuiteSync - Collaborative Apartment Hunting Platform

> **The Tinder for apartment hunting** - Turn apartment hunting with roommates into a fun, collaborative experience using AI-powered curation and real-time voting.

## What is SuiteSync?

SuiteSync is a collaborative apartment hunting platform that solves the nightmare of finding an apartment with roommates. Instead of endless debates and compromised decisions, friends can now swipe through apartment comparisons together in real-time sessions.

### Key Features

- **AI-Powered Curation**: Uses Google Gemini AI to intelligently filter apartments based on combined user preferences
- **Real-Time Collaboration**: Socket.io enables instant voting and updates across all participants
- **Tournament-Style Voting**: Sophisticated ranking algorithm ensures optimal group decisions
- **Comprehensive Preferences**: Handles budget, location, accessibility, amenities, and lifestyle factors
- **Real-Time Updates**: Live synchronization of votes and apartment rankings
- **Smart Filtering**: Automatically filters apartments by bedroom count and user requirements

## Quick Start

### Prerequisites

- **Node.js** 18+ and npm
- **Supabase** account and project
- **Google Gemini API** key
- **Python** 3.11+ (for data analysis features)

### 1. Clone and Install

```bash
git clone https://github.com/Stunned1/SuiteSync.git
cd SuiteSync
npm install
```

### 2. Environment Setup

Create a `.env.local` file in the root directory with the following variables:

```env
### Required Variables

| Variable | Description | Example |
|----------|-------------|---------|
| `NEXT_PUBLIC_SUPABASE_URL` | Your Supabase project URL |
| `NEXT_PUBLIC_SUPABASE_ANON_KEY` | Supabase anonymous key (public) | 
| `SUPABASE_SERVICE_ROLE_KEY` | Supabase service role key (private) | 
| `GEMINI_API_KEY` | Google Gemini AI API key |

### Optional Variables

| Variable | Description | Default | Example |
|----------|-------------|---------|---------|
| `NEXT_PUBLIC_APP_URL` | Application URL for API calls | `http://localhost:3000` | `https://yourdomain.com` |
| `NODE_ENV` | Environment mode | `development` | `production` |
| `PORT` | Server port | `3000` | `8080` |
```

### 3. Database Setup

#### Option A: Local Development with Supabase CLI

```bash
# Install Supabase CLI
npm install -g supabase

# Start local Supabase
supabase start

# Run database migrations
supabase db reset
```

#### Option B: Remote Supabase Project

1. Create a new Supabase project at [supabase.com](https://supabase.com)
2. Run the SQL scripts in your Supabase SQL editor:

```sql
-- Run these in order:
\i supabase/sql/setup_user_profiles_with_preferences.sql
\i supabase/sql/setup_rooms_table.sql
\i supabase/sql/setup_complex_public_id.sql
\i supabase/sql/setup_comparisons_table.sql
```

### 4. Start Development Server

```bash
npm run dev
```

Visit [http://localhost:3000](http://localhost:3000) to see the application.


### Getting API Keys

#### Supabase Keys
1. Go to your [Supabase Dashboard](https://supabase.com/dashboard)
2. Select your project
3. Go to Settings → API
4. Copy the Project URL and API keys

#### Google Gemini API Key
1. Visit [Google AI Studio](https://makersuite.google.com/app/apikey)
2. Create a new API key
3. Copy the key to your `.env.local`

## Project Structure

```
SuiteSync/
├── src/
│   ├── app/                    # Next.js App Router
│   │   ├── api/               # API routes
│   │   ├── page.tsx           # Home page
│   │   ├── profile/           # User profile pages
│   │   └── room/[code]/       # Room session pages
│   ├── components/            # React components
│   │   ├── ui/               # Reusable UI components
│   │   ├── apartment-comparison.tsx
│   │   ├── hunt-session.tsx
│   │   └── ...
│   ├── lib/                  # Utility libraries
│   │   ├── supabase.ts       # Supabase client
│   │   ├── socket-server.js  # Socket.IO server
│   │   ├── gemini-apartment-agent.ts
│   │   └── ...
│   ├── hooks/                # Custom React hooks
│   ├── types/                # TypeScript type definitions
│   └── data/                 # Static data
├── supabase/                 # Supabase configuration
│   ├── sql/                 # Database migrations
│   ├── functions/           # Edge functions
│   └── config.toml          # Local development config
├── analysis/                # Data analysis scripts
├── public/                  # Static assets
└── server.js               # Custom server with Socket.IO
```

## How It Works

### 1. Account Setup
- Users create an account and set their individual preferences
- Preferences include: budget, location, amenities, accessibility needs, commute preferences
- Users can save favorite apartments and ideal apartment descriptions

### 2. Room Creation
- Host creates a room with a 6-character code
- Configures session parameters (rounds, anonymous mode)
- Room is ready for friends to join

### 3. User Joining
- Friends join using the room code
- System automatically uses their saved preferences
- System validates all requirements are met

### 4. AI Curation
- Google Gemini AI analyzes all user preferences
- Filters apartments by minimum bedroom count
- Includes user favorite apartments
- Generates optimized apartment list

### 5. Tournament Voting
- Users swipe through apartment comparisons
- Real-time vote synchronization
- Sophisticated ranking algorithm determines winners
- Live updates show current standings

### 6. Results & Analytics
- Final apartment rankings
- Midpoint insights and analytics
- Export results for further discussion

## Development

### Available Scripts

```bash
# Development
npm run dev          
```

### Tech Stack

- **Frontend**: Next.js 15, React 19, TypeScript
- **Styling**: Tailwind CSS, Radix UI
- **Backend**: Next.js API Routes, Socket.IO
- **Database**: Supabase (PostgreSQL)
- **AI**: Google Gemini 2.0 Flash
- **Real-time**: Socket.IO
- **Deployment**: Vercel (recommended)


### Environment Variables for Production

```env
NEXT_PUBLIC_SUPABASE_URL=your_production_supabase_url
NEXT_PUBLIC_SUPABASE_ANON_KEY=your_production_anon_key
SUPABASE_SERVICE_ROLE_KEY=your_production_service_key
GEMINI_API_KEY=your_gemini_api_key
NEXT_PUBLIC_APP_URL=https://yourdomain.com
NODE_ENV=production
```

## Data Analysis Features

The project includes Python-based data analysis tools:

```bash
# Set up Python environment
cd analysis
python -m venv venv
source venv/bin/activate  # On Windows: venv\Scripts\activate
pip install -r requirements.txt

# Run clustering analysis
python clustering.py
```

## Troubleshooting

### Common Issues

#### "No users found in room"
- Verify room code exists in database
- Check that `players` column has data
- Ensure room was created successfully

#### "AI selection failed"
- Verify `GEMINI_API_KEY` is valid
- Check API quotas and limits
- Ensure internet connectivity

#### Socket.IO connection issues
- Verify `NEXT_PUBLIC_APP_URL` is correct
- Check firewall settings
- Ensure port 3000 is available

#### Database connection errors
- Verify Supabase credentials
- Check database is running (if local)
- Ensure tables exist and are properly set up

### Getting Help
- Review the [GEMINI_AI_AGENT_README.md](GEMINI_AI_AGENT_README.md) for AI-specific issues
- Check Supabase logs in the dashboard

---

**Built for better apartment hunting experiences**