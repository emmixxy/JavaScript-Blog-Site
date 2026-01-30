# Signal Blog

A modern, block-based blog template built with Next.js, Prisma, and Tailwind CSS.

## Features
- Block-based editor for headings, paragraphs, lists, and images
- Admin dashboard for creating, editing, and deleting posts
- Category pages with descriptions
- Image uploads stored in `/public/uploads`
- Optional references/sources per post
- Seed data from `data/posts.json`

## Tech Stack
- Next.js (App Router)
- React
- TypeScript
- Tailwind CSS
- Prisma + PostgreSQL

## How It Runs
- Next.js App Router handles pages, layouts, and API routes.
- Prisma reads/writes posts, categories, and references in PostgreSQL.
- The admin editor writes content blocks (no markdown parsing).
- Image uploads go to `/public/uploads` via `POST /api/uploads`.
- Seed data loads from `data/posts.json` using `npm run seed`.

## Getting Started

1) Install dependencies
```bash
npm install
```

2) Create your environment file
```bash
copy .env.example .env
```
Update:
- `DATABASE_URL` for your Postgres instance
- `ADMIN_PASSWORD` for admin login

3) Run migrations and seed data
```bash
npx prisma migrate dev
npm run seed
```

4) Start the dev server
```bash
npm run dev
```

Open http://localhost:3000.

## Admin Support

- Login: `/admin/login`
- Default admin password: `ADMIN_PASSWORD` from `.env` (fallback is `changeme`)
- Admin features:
  - Create, edit, and delete posts
  - Upload hero images and inline images
  - Add references/sources
  - Mark posts as featured

## Environment Variables

```
DATABASE_URL="postgresql://USER:PASSWORD@localhost:5432/blog_template?schema=public"
ADMIN_PASSWORD="changeme"
```

## Content Model

Posts are stored in the database with JSON `content` blocks. Each post contains:
- `title`, `slug`, `excerpt`
- `author`, `category`, `date`
- `featured` (boolean)
- `image` (hero image URL)
- `blocks`:
  - `heading` (level 1-3)
  - `paragraph`
  - `list`
  - `image` (src, alt, caption)

Seed data lives in `data/posts.json`.

## Project Structure

- `src/app` - pages and API routes
- `src/components` - UI and admin editor
- `src/lib` - auth and data access (Prisma)
- `src/constants` - site config and categories
- `prisma` - schema and seed script
- `data` - seed data for posts
- `public/uploads` - uploaded images

## Scripts

- `npm run dev` - start local development
- `npm run build` - production build
- `npm run start` - start production server
- `npm run lint` - lint the codebase
- `npm run prisma` - Prisma CLI passthrough
- `npm run seed` - seed the database from `data/posts.json`

## Deployment Notes

- The upload API writes files to `public/uploads`. For serverless hosts, swap this
  with object storage (S3, Cloudinary, etc).
- Set `DATABASE_URL` and `ADMIN_PASSWORD` as environment variables in your host.

## Customization Checklist

- Update `src/constants/index.ts` (site name, tagline, categories)
- Replace the mock posts in `data/posts.json`
- Update the contact email in `src/app/contact/page.tsx`
- Add your own privacy/terms copy if required

## Contributing

Issues and pull requests are welcome. If you plan a larger change, open an issue first.

## Support

If this template helps you, you can support its development:

- ETH: `0xB6339673185B9e9D87D1fa09F759c34Eb9a993ac`

## License

MIT
