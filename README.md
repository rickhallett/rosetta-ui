# Therapy Practice Management Platform

A comprehensive platform for therapists to manage clients, sessions, notes, and analytics with AI-powered insights.

## 🚀 Quick Start

```bash
# Clone the repository
git clone https://github.com/rickhallett/rosetta-ui.git
cd rosetta-ui

# Install dependencies
npm install

# Set up environment variables
cp .env.example .env.local

# Start development server
npm run dev
```

Visit [http://localhost:3000](http://localhost:3000) to view the application.

## 🏗️ Tech Stack

- **Framework**: Next.js with TypeScript
- **Database**: Supabase (PostgreSQL)
- **Authentication**: Supabase Auth
- **UI Components**: shadcn/ui
- **State Management**: TanStack Query
- **ORM**: Prisma
- **AI Integration**: OpenAI
- **File Storage**: Supabase Storage

## 📅 Development Timeline

### Week 1: Foundation & Authentication
- [x] Project structure setup
- [ ] Authentication system
- [ ] User management
- [ ] Dashboard layout
- [ ] Protected routes

### Week 2: Core Features
- [ ] Client management
- [ ] Session scheduling
- [ ] Notes system
- [ ] File management
- [ ] Storage integration

### Week 3: Advanced Features
- [ ] Analytics dashboard
- [ ] Full-text search
- [ ] Advanced filtering
- [ ] Performance optimization
- [ ] Error handling

### Week 4: AI Integration & Polish
- [ ] AI-powered features
- [ ] UI/UX refinements
- [ ] Documentation
- [ ] Production deployment

## 🗄️ Project Structure

```
src/
├── app/
│   ├── (auth)/
│   │   ├── login/
│   │   └── register/
│   ├── (dashboard)/
│   │   ├── clients/
│   │   ├── sessions/
│   │   └── settings/
│   ├── api/
│   └── layout.tsx
├── components/
│   ├── ui/
│   ├── forms/
│   └── shared/
├── lib/
│   ├── supabase/
│   ├── utils/
│   └── types/
└── styles/
```

## 📊 Database Schema

### Profiles
```sql
create type user_role as enum ('therapist', 'admin');

create table profiles (
  id uuid references auth.users on delete cascade,
  role user_role default 'therapist',
  full_name text,
  email text unique,
  created_at timestamptz default now(),
  updated_at timestamptz default now()
);
```

### Clients
```sql
create table clients (
  id uuid default uuid_generate_v4(),
  therapist_id uuid references profiles(id),
  first_name text,
  last_name text,
  email text,
  phone text,
  status client_status default 'active',
  created_at timestamptz default now(),
  updated_at timestamptz default now(),
  primary key (id)
);
```

### Sessions & Notes
```sql
create table sessions (
  id uuid default uuid_generate_v4(),
  client_id uuid references clients(id),
  date timestamptz,
  duration integer,
  status session_status default 'scheduled',
  notes text,
  created_at timestamptz default now(),
  updated_at timestamptz default now(),
  primary key (id)
);

create table notes (
  id uuid default uuid_generate_v4(),
  session_id uuid references sessions(id),
  content text,
  tags text[],
  created_at timestamptz default now(),
  updated_at timestamptz default now(),
  primary key (id)
);
```

## 🔒 Security Features

- Row Level Security (RLS) policies
- Authentication middleware
- Role-based access control
- Secure file storage policies
- Data encryption

## 🧪 Testing

```bash
# Run tests
npm test

# Run tests with coverage
npm test -- --coverage
```

## 📚 Documentation

- [Setup Guide](docs/setup.md)
- [API Documentation](docs/api.md)
- [Component Library](docs/components.md)
- [Deployment Guide](docs/deployment.md)

## 🚀 Deployment Checklist

- [ ] Configure environment variables
- [ ] Set up SSL certificates
- [ ] Configure database backups
- [ ] Set up monitoring tools
- [ ] Configure error tracking
- [ ] Set up analytics
- [ ] Deploy to production

## 📝 License

[Your chosen license]

## 🤝 Contributing

1. Fork the repository
2. Create your feature branch (`git checkout -b feature/amazing-feature`)
3. Commit your changes (`git commit -m 'Add some amazing feature'`)
4. Push to the branch (`git push origin feature/amazing-feature`)
5. Open a Pull Request

## 📫 Support

For support, email [your-email] or create an issue in the repository.

---

This is a [Next.js](https://nextjs.org) project bootstrapped with [`create-next-app`](https://nextjs.org/docs/app/api-reference/cli/create-next-app).

## Getting Started

First, run the development server:

```bash
npm run dev
# or
yarn dev
# or
pnpm dev
# or
bun dev
```

Open [http://localhost:3000](http://localhost:3000) with your browser to see the result.

You can start editing the page by modifying `app/page.tsx`. The page auto-updates as you edit the file.

This project uses [`next/font`](https://nextjs.org/docs/app/building-your-application/optimizing/fonts) to automatically optimize and load [Geist](https://vercel.com/font), a new font family for Vercel.

## Learn More

To learn more about Next.js, take a look at the following resources:

- [Next.js Documentation](https://nextjs.org/docs) - learn about Next.js features and API.
- [Learn Next.js](https://nextjs.org/learn) - an interactive Next.js tutorial.

You can check out [the Next.js GitHub repository](https://github.com/vercel/next.js) - your feedback and contributions are welcome!

## Deploy on Vercel

The easiest way to deploy your Next.js app is to use the [Vercel Platform](https://vercel.com/new?utm_medium=default-template&filter=next.js&utm_source=create-next-app&utm_campaign=create-next-app-readme) from the creators of Next.js.

Check out our [Next.js deployment documentation](https://nextjs.org/docs/app/building-your-application/deploying) for more details.
