---
description: Creates a new React + Vite + shadcn + Supabase project with optional custom project_id
---
This workflow creates a complete React project with Vite, shadcn-ui, and Supabase integration.

**Prerequisites**: Ensure you have Node.js, pnpm, and Supabase CLI installed.

Execute the following steps to create the project:

1. **Create Vite React project**: Initialize a new React project with Vite and TypeScript using `pnpm create vite . --template react-ts`

2. **Install dependencies**: Install the base project dependencies with `pnpm install`

3. **Install additional dependencies**: Add required packages for shadcn-ui and Supabase: `pnpm add @supabase/supabase-js lucide-react class-variance-authority clsx tailwind-merge`

4. **Install dev dependencies**: Add development dependencies: `pnpm add -D @types/node autoprefixer postcss tailwindcss`

5. **Initialize Tailwind CSS**: Set up Tailwind CSS configuration with `pnpm dlx tailwindcss init -p`

6. **Initialize shadcn-ui**: Set up shadcn-ui with default configuration using `bunx shadcn@latest init`

7. **Configure Tailwind**: Update tailwind.config.js for shadcn-ui compatibility with proper theme configuration including colors, border radius, keyframes, and animations.

8. **Update global CSS**: Replace src/index.css with shadcn-ui styles including CSS variables for light and dark themes.

9. **Initialize Supabase**: Ask the user if they want to use an existing Supabase project. If yes, request project_id and use `supabase link --project-ref PROJECT_ID`. If no, use `supabase init` to create new project.

10. **Create Supabase client**: Create src/lib/supabase.ts with Supabase client configuration using environment variables.

11. **Create environment file**: Set up .env.local with placeholder Supabase URL and anon key.

12. **Update .gitignore**: Add environment files (.env.local, .env) to gitignore.

13. **Create utils file**: Add src/lib/utils.ts with cn utility function for className merging.

14. **Update vite.config.ts**: Add path alias configuration for better imports (@/ alias).

15. **Update tsconfig.json**: Add path mapping for TypeScript to support @/* imports.

16. **Install tailwindcss-animate**: Add required animation plugin with `pnpm add tailwindcss-animate`

17. **Create components.json**: Ensure shadcn-ui configuration is properly set with correct paths and aliases.

18. **Final verification**: Test the setup by running `pnpm run dev`

## Post-Setup Instructions:

1. **Configure Supabase**: Update .env.local with actual Supabase URL and anon key from project dashboard

2. **Add shadcn-ui components**: Install components as needed using `bunx shadcn@latest add [component-name]`

3. **Start developing**: The project includes:
   - ⚡ Vite for fast development
   - ⚛️ React 18 with TypeScript
   - 🎨 Tailwind CSS + shadcn-ui components
   - 🗄️ Supabase integration
   - 📁 Proper path aliases (@/components, @/lib)

The development server will run on http://localhost:5173 and the project will be ready for modern React development with a complete design system and backend integration.