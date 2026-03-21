
# LinkVault

A smart bookmark manager that saves links with tags, notes, and status tracking — with a full activity log of every action you take.

Built with **Next.js 14**, **TypeScript**, **PostgreSQL**, **Drizzle ORM**, and **Tailwind CSS**.

---

## Features

- Save links with a title, notes, tags, and status (unread / read / archived)
- Activity log — every action is recorded (saved, visited, status changed, tagged, deleted, notes updated)
- Filter links by status or tag, search by title, URL, or notes
- Link detail view with per-link activity history
- Clean dashboard with stats and recent activity feed

## Tech Stack

| Layer | Tech |
|---|---|
| Framework | Next.js 14 (App Router) |
| Language | TypeScript |
| Database | PostgreSQL |
| ORM | Drizzle ORM |
| Styling | Tailwind CSS |
| Deployment | Vercel |

## Getting Started

### Prerequisites

- Node.js 18+
- PostgreSQL database (local or [Neon](https://neon.tech))

### Installation

```bash
# Clone the repo
git clone https://github.com/your-username/linkvault.git
cd linkvault

# Install dependencies
npm install

# Set up environment variables
cp .env.example .env.local
```

Add your database URL to `.env.local`:

```env
DATABASE_URL=postgresql://user:password@localhost:5432/linkvault
```

### Database Setup

```bash
# Push schema to database
npx drizzle-kit push

# (Optional) Seed with sample data
npm run db:seed
```

### Run Locally

```bash
npm run dev
```

Open [http://localhost:3000](http://localhost:3000).

## Project Structure

```
src/
├── app/
│   ├── (dashboard)/
│   │   ├── page.tsx          # Dashboard
│   │   ├── links/
│   │   │   ├── page.tsx      # All links
│   │   │   └── [id]/page.tsx # Link detail
│   │   └── activity/page.tsx # Activity log
├── components/
│   ├── links/
│   └── activity/
├── lib/
│   ├── db/
│   │   ├── schema.ts         # Drizzle schema
│   │   └── index.ts
│   └── actions/
│       ├── links.ts          # Server actions
│       └── activity.ts
└── types/index.ts
```

## Database Schema

```
users ──< links ──< link_tags >── tags
                └──< activity_logs
```

Every mutation to a link (create, edit, delete, status change, tag, visit) writes a row to `activity_logs` with an `action` string and a `metadata` JSONB field for context.

## Prototype

A fully functional single-file HTML prototype is included at `prototype/linkvault.html`. Open it directly in any browser — no build step needed. Use it as a reference for UI and data flow before wiring up the backend.

## Roadmap

- [ ] Auth (NextAuth or Clerk)
- [ ] Browser extension for one-click saving
- [ ] Favicon auto-fetch
- [ ] Export links as JSON / CSV
- [ ] Public sharing for individual links

## License

MIT
