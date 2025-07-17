# Portfolio Website

Personal portfolio website for Arif (@masarif.id) - A visual storyteller from Central Java, Indonesia. Features photography gallery, blog posts, Spotify integration, and product showcase. Built with Next.js 15.

## Features

- **Dynamic Grid Layout** - Interactive and responsive grid system using React Grid Layout
- **Spotify Integration** - Real-time display of currently playing or recently played tracks
- **Blog System** - MDX-powered blog with syntax highlighting and custom components
- **Project Gallery** - Showcase photography work with optimized image loading
- **Product Pages** - Dedicated pages for Lightroom presets and video LUTs
- **Interactive Map** - Location display using Mapbox GL
- **Theme Support** - Light and dark mode with smooth transitions
- **Real-time Analytics** - Track visitors, page views, UTM campaigns, and user behavior
- **Secure Analytics Dashboard** - Protected admin panel with authentication
- **SEO Optimized** - Complete meta tags, sitemap, and structured data
- **Performance Focused** - Optimized images, fonts, and loading states

## 🛠️ Tech Stack

- **Framework:** Next.js 15 (App Router)
- **Language:** TypeScript
- **Styling:** Tailwind CSS v4
- **Content:** MDX (next-mdx-remote)
- **Grid System:** React Grid Layout
- **Maps:** Mapbox GL + React Map GL
- **Icons:** React Icons
- **Data Fetching:** SWR
- **Theme:** next-themes
- **Analytics:** Vercel Analytics

## Analytics Features

The portfolio includes a comprehensive analytics system:

### Real-time Tracking
- Page views and unique visitors
- UTM campaign tracking
- Device and country detection
- Session tracking
- External link clicks
- Scroll depth tracking
- Time on page

### Analytics Dashboard (`/analitik`)
- Secure login system
- Real-time visitor statistics
- Traffic source analysis
- UTM campaign performance
- Device and country breakdown
- Top pages and content performance
- Hourly and daily traffic patterns

### Privacy & Security
- IP addresses are hashed for privacy
- Rate limiting on API endpoints
- JWT-based authentication
- Secure password hashing with bcrypt
- Database-level security with Supabase RLS

## Prerequisites

Before you begin, ensure you have the following installed:

- **Node.js** (version 18.0 or higher)
- **npm**, **yarn**, or **pnpm** package manager
- **Git** for version control

## Installation

### 1. Clone the Repository

```bash
git clone https://github.com/homearif6/tes-porto.git
cd tes-porto
```

### 2. Install Dependencies

Using npm:
```bash
npm install
```

Using yarn:
```bash
yarn install
```

Using pnpm:
```bash
pnpm install
```

### 3. Environment Variables

Create a `.env.local` file in the root directory and add the following environment variables:

```env
# Spotify API Configuration
SPOTIFY_CLIENT_ID=your_spotify_client_id
SPOTIFY_CLIENT_SECRET=your_spotify_client_secret
SPOTIFY_REFRESH_TOKEN=your_spotify_refresh_token

# Mapbox Configuration
NEXT_PUBLIC_MAPBOX_ACCESS_TOKEN=your_mapbox_access_token

# Supabase Configuration (untuk analytics database)
NEXT_PUBLIC_SUPABASE_URL=your_supabase_url
NEXT_PUBLIC_SUPABASE_ANON_KEY=your_supabase_anon_key
SUPABASE_SERVICE_ROLE_KEY=your_supabase_service_role_key

# Analytics Authentication
ANALYTICS_JWT_SECRET=your_very_secure_jwt_secret_key_here
ANALYTICS_ADMIN_EMAIL=admin@masarif.id
ANALYTICS_ADMIN_PASSWORD_HASH=your_bcrypt_hashed_password
```

#### Getting Spotify API Credentials:

1. Go to [Spotify Developer Dashboard](https://developer.spotify.com/dashboard)
2. Create a new app
3. Get your `Client ID` and `Client Secret`
4. Set redirect URI to `http://localhost:3000/api/auth/callback/spotify`
5. Use [Spotify Web API Authorization Guide](https://developer.spotify.com/documentation/web-api/tutorials/code-flow) to get refresh token

#### Setting Up Analytics (Production):

1. **Setup Supabase Database:**
   - Create a new Supabase project
   - Run the migration file `supabase/migrations/create_analytics_tables.sql`
   - Get your Supabase URL, anon key, and service role key

2. **Generate Password Hash:**
   ```bash
   node utils/setup-password.js yourSecurePassword123
   ```
   Copy the generated hash to your environment variables

3. **Set Environment Variables:**
   - Add all Supabase credentials to `.env.local`
   - Set a strong JWT secret (random string)
   - Set admin email and password hash

4. **Access Analytics:**
   - Go to `/analitik/login`
   - Login with your admin credentials
   - View real-time analytics at `/analitik`

#### Getting Mapbox Access Token:

1. Sign up at [Mapbox](https://www.mapbox.com/)
2. Go to your [Account page](https://account.mapbox.com/)
3. Create a new access token
4. Copy the token to your environment variables

### 4. Run the Development Server

```bash
npm run dev
# or
yarn dev
# or
pnpm dev
```

Open [http://localhost:3000](http://localhost:3000) in your browser to see the result.

## Project Structure

```
├── app/                          # Next.js App Router
│   ├── (content)/               # Content pages group
│   │   ├── posts/[slug]/        # Blog post pages
│   │   ├── projects/[slug]/     # Project detail pages
│   │   ├── products/            # Product pages
│   │   └── spotify/             # Spotify integration page
│   ├── api/                     # API routes
│   │   └── now-playing/         # Spotify API endpoint
│   ├── globals.css              # Global styles
│   ├── layout.tsx               # Root layout
│   └── page.tsx                 # Homepage
├── components/                   # React components
│   ├── grid/                    # Grid layout components
│   │   ├── widgets/             # Grid item widgets
│   │   ├── item.tsx             # Grid item wrapper
│   │   └── layout.tsx           # Grid layout component
│   └── ui/                      # UI components
├── config/                      # Configuration files
│   ├── grid.ts                  # Grid layout configurations
│   ├── site.ts                  # Site metadata
│   └── socials.ts               # Social media links
├── content/                     # MDX content
│   ├── posts/                   # Blog posts
│   └── projects/                # Project descriptions
├── public/                      # Static assets
│   ├── images/                  # Images
│   └── projects/                # Project images
└── utils/                       # Utility functions
    ├── fonts.ts                 # Font configurations
    ├── hooks.ts                 # Custom React hooks
    ├── lib.ts                   # Helper functions
    └── mdx.ts                   # MDX processing
```

## Content Management

### Adding Blog Posts

1. Create a new `.mdx` file in `content/posts/`
2. Add frontmatter with required fields:

```mdx
---
title: "Your Post Title"
description: "Post description for SEO and previews"
date: 2024-01-15
---

Your post content here using MDX syntax...
```

### Adding Projects

1. Create a new `.mdx` file in `content/projects/`
2. Add frontmatter with required fields:

```mdx
---
title: "Project Name"
description: "Project description"
links: [{"name": "Live Demo","url": "https://example.com"}]
images: [{"i":"image-1","url":"/projects/project-name/image-1.jpg"}]
---

Project details and description...
```

### Customizing Grid Layout

Edit `config/grid.ts` to modify the grid layout:

- Add new widgets in `components/grid/widgets/`
- Update `gridItems` array to include new components
- Modify `layouts` object for different breakpoints

## Customization

### Site Configuration

Update `config/site.ts` with your information:

```typescript
export const siteConfig = {
    title: 'Your Name',
    description: 'Your description',
    url: 'https://yourdomain.com',
    ogImage: 'https://yourdomain.com/og-image.png',
    author: 'Your Name',
};
```

### Social Media Links

Update `config/socials.ts` with your social media profiles:

```typescript
const socials: Social[] = [
    {
        name: 'Instagram',
        url: 'https://instagram.com/yourusername',
        icon: FaInstagram,
    },
    // Add more social links...
];
```

### Styling

- Global styles: `app/globals.css`
- Tailwind configuration: Uses Tailwind CSS v4 with custom color palette
- Component styles: Inline with Tailwind classes

## Deployment

### Deploy to Vercel (Recommended)

1. Push your code to GitHub
2. Connect your repository to [Vercel](https://vercel.com)
3. Add environment variables in Vercel dashboard
4. Deploy automatically on every push

### Deploy to Netlify

1. Build the project: `npm run build`
2. Upload the `out` folder to Netlify
3. Configure environment variables
4. Set up continuous deployment

### Other Platforms

The project can be deployed to any platform that supports Next.js:

- **Railway**
- **Render**
- **DigitalOcean App Platform**
- **AWS Amplify**


## Scripts

```bash
# Development
npm run dev          # Start development server

# Production
npm run build        # Build for production
npm run start        # Start production server

# Code Quality
npm run lint         # Run ESLint
```

## Troubleshooting

### Common Issues

**Spotify Integration Not Working:**
- Verify environment variables are set correctly
- Check if Spotify app is approved for production use
- Ensure refresh token is valid

**Map Not Loading:**
- Verify Mapbox access token
- Check if token has proper permissions
- Ensure domain is added to token restrictions

**Build Errors:**
- Clear `.next` folder and rebuild
- Check for TypeScript errors
- Verify all dependencies are installed

### Getting Help

If you encounter issues:

1. Check the [Next.js documentation](https://nextjs.org/docs)
2. Review [Tailwind CSS documentation](https://tailwindcss.com/docs)
3. Open an issue on GitHub

## License

This project is open source and available under the [MIT License](LICENSE).

## Credits

This project is based on the original portfolio template by [bymaul](https://github.com/bymaul/portfolio).

**Original Repository:** https://github.com/bymaul/portfolio

## Contributing

Contributions are welcome! Please feel free to submit a Pull Request.

1. Fork the project
2. Create your feature branch (`git checkout -b feature/AmazingFeature`)
3. Commit your changes (`git commit -m 'Add some AmazingFeature'`)
4. Push to the branch (`git push origin feature/AmazingFeature`)
5. Open a Pull Request

