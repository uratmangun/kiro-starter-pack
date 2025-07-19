---
description: Creates a new React + Vite + shadcn + Supabase project with optional custom project_id
---

This workflow creates a complete React project with Vite, shadcn-ui, and Supabase integration.

**Prerequisites**: Ensure you have Node.js, pnpm, and Supabase CLI installed.

// turbo-all

1. **Create Vite React project**: Initialize a new React project with Vite and TypeScript
```fish
pnpm create vite . --template react-ts
```

2. **Install dependencies**: Install the base project dependencies
```fish
pnpm install
```

3. **Install additional dependencies**: Add required packages for shadcn-ui and Supabase
```fish
pnpm add @supabase/supabase-js lucide-react class-variance-authority clsx tailwind-merge
```

4. **Install dev dependencies**: Add development dependencies
```fish
pnpm add -D @types/node autoprefixer postcss tailwindcss
```

5. **Initialize Tailwind CSS**: Set up Tailwind CSS configuration
```fish
pnpm dlx tailwindcss init -p
```

6. **Initialize shadcn-ui**: Set up shadcn-ui with default configuration
```fish
bunx shadcn@latest init
```

7. **Configure Tailwind**: Update tailwind.config.js for shadcn-ui compatibility
```fish
echo 'import type { Config } from "tailwindcss"

const config: Config = {
  darkMode: ["class"],
  content: [
    "./pages/**/*.{ts,tsx}",
    "./components/**/*.{ts,tsx}",
    "./app/**/*.{ts,tsx}",
    "./src/**/*.{ts,tsx}",
  ],
  prefix: "",
  theme: {
    container: {
      center: true,
      padding: "2rem",
      screens: {
        "2xl": "1400px",
      },
    },
    extend: {
      colors: {
        border: "hsl(var(--border))",
        input: "hsl(var(--input))",
        ring: "hsl(var(--ring))",
        background: "hsl(var(--background))",
        foreground: "hsl(var(--foreground))",
        primary: {
          DEFAULT: "hsl(var(--primary))",
          foreground: "hsl(var(--primary-foreground))",
        },
        secondary: {
          DEFAULT: "hsl(var(--secondary))",
          foreground: "hsl(var(--secondary-foreground))",
        },
        destructive: {
          DEFAULT: "hsl(var(--destructive))",
          foreground: "hsl(var(--destructive-foreground))",
        },
        muted: {
          DEFAULT: "hsl(var(--muted))",
          foreground: "hsl(var(--muted-foreground))",
        },
        accent: {
          DEFAULT: "hsl(var(--accent))",
          foreground: "hsl(var(--accent-foreground))",
        },
        popover: {
          DEFAULT: "hsl(var(--popover))",
          foreground: "hsl(var(--popover-foreground))",
        },
        card: {
          DEFAULT: "hsl(var(--card))",
          foreground: "hsl(var(--card-foreground))",
        },
      },
      borderRadius: {
        lg: "var(--radius)",
        md: "calc(var(--radius) - 2px)",
        sm: "calc(var(--radius) - 4px)",
      },
      keyframes: {
        "accordion-down": {
          from: { height: "0" },
          to: { height: "var(--radix-accordion-content-height)" },
        },
        "accordion-up": {
          from: { height: "var(--radix-accordion-content-height)" },
          to: { height: "0" },
        },
      },
      animation: {
        "accordion-down": "accordion-down 0.2s ease-out",
        "accordion-up": "accordion-up 0.2s ease-out",
      },
    },
  },
  plugins: [require("tailwindcss-animate")],
} satisfies Config

export default config' > tailwind.config.ts
```

8. **Update global CSS**: Replace src/index.css with shadcn-ui styles
```fish
echo '@tailwind base;
@tailwind components;
@tailwind utilities;

@layer base {
  :root {
    --background: 0 0% 100%;
    --foreground: 222.2 84% 4.9%;
    --card: 0 0% 100%;
    --card-foreground: 222.2 84% 4.9%;
    --popover: 0 0% 100%;
    --popover-foreground: 222.2 84% 4.9%;
    --primary: 222.2 47.4% 11.2%;
    --primary-foreground: 210 40% 98%;
    --secondary: 210 40% 96%;
    --secondary-foreground: 222.2 47.4% 11.2%;
    --muted: 210 40% 96%;
    --muted-foreground: 215.4 16.3% 46.9%;
    --accent: 210 40% 96%;
    --accent-foreground: 222.2 47.4% 11.2%;
    --destructive: 0 84.2% 60.2%;
    --destructive-foreground: 210 40% 98%;
    --border: 214.3 31.8% 91.4%;
    --input: 214.3 31.8% 91.4%;
    --ring: 222.2 84% 4.9%;
    --radius: 0.5rem;
  }

  .dark {
    --background: 222.2 84% 4.9%;
    --foreground: 210 40% 98%;
    --card: 222.2 84% 4.9%;
    --card-foreground: 210 40% 98%;
    --popover: 222.2 84% 4.9%;
    --popover-foreground: 210 40% 98%;
    --primary: 210 40% 98%;
    --primary-foreground: 222.2 47.4% 11.2%;
    --secondary: 217.2 32.6% 17.5%;
    --secondary-foreground: 210 40% 98%;
    --muted: 217.2 32.6% 17.5%;
    --muted-foreground: 215 20.2% 65.1%;
    --accent: 217.2 32.6% 17.5%;
    --accent-foreground: 210 40% 98%;
    --destructive: 0 62.8% 30.6%;
    --destructive-foreground: 210 40% 98%;
    --border: 217.2 32.6% 17.5%;
    --input: 217.2 32.6% 17.5%;
    --ring: 212.7 26.8% 83.9%;
  }
}

@layer base {
  * {
    @apply border-border;
  }
  body {
    @apply bg-background text-foreground;
  }
}' > src/index.css
```

9. **Initialize Supabase**: Set up Supabase project (ask for project_id if needed)
Ask the user: "Would you like to use an existing Supabase project? If yes, please provide the project_id. If no, I'll create a new one."

If project_id is provided:
```fish
supabase init
supabase link --project-ref PROJECT_ID_HERE
supabase db pull
```

If no project_id provided:
```fish
supabase init
```

10. **Create Supabase client**: Create lib/supabase.ts for Supabase client configuration
```fish
mkdir -p src/lib
echo 'import { createClient } from "@supabase/supabase-js"

const supabaseUrl = import.meta.env.VITE_SUPABASE_URL
const supabaseAnonKey = import.meta.env.VITE_SUPABASE_ANON_KEY

export const supabase = createClient(supabaseUrl, supabaseAnonKey)' > src/lib/supabase.ts
```

11. **Create environment file**: Set up .env.local for Supabase configuration
```fish
echo '# Supabase Configuration
VITE_SUPABASE_URL=your_supabase_url_here
VITE_SUPABASE_ANON_KEY=your_supabase_anon_key_here' > .env.local
```

12. **Update .gitignore**: Add environment files to gitignore
```fish
echo '
# Environment files
.env.local
.env' >> .gitignore
```

13. **Create utils file**: Add utility functions for shadcn-ui
```fish
echo 'import { type ClassValue, clsx } from "clsx"
import { twMerge } from "tailwind-merge"

export function cn(...inputs: ClassValue[]) {
  return twMerge(clsx(inputs))
}' > src/lib/utils.ts
```

14. **Update vite.config.ts**: Add path alias for better imports
```fish
echo 'import path from "path"
import { defineConfig } from "vite"
import react from "@vitejs/plugin-react"

// https://vitejs.dev/config/
export default defineConfig({
  plugins: [react()],
  resolve: {
    alias: {
      "@": path.resolve(__dirname, "./src"),
    },
  },
})' > vite.config.ts
```

15. **Update tsconfig.json**: Add path mapping for TypeScript
```fish
echo '{
  "files": [],
  "references": [
    {
      "path": "./tsconfig.app.json"
    },
    {
      "path": "./tsconfig.node.json"
    }
  ],
  "compilerOptions": {
    "baseUrl": ".",
    "paths": {
      "@/*": ["./src/*"]
    }
  }
}' > tsconfig.json
```

16. **Install tailwindcss-animate**: Add required animation plugin
```fish
pnpm add tailwindcss-animate
```

17. **Create components.json**: Ensure shadcn-ui configuration is properly set
```fish
echo '{
  "$schema": "https://ui.shadcn.com/schema.json",
  "style": "default",
  "rsc": false,
  "tsx": true,
  "tailwind": {
    "config": "tailwind.config.ts",
    "css": "src/index.css",
    "baseColor": "slate",
    "cssVariables": true,
    "prefix": ""
  },
  "aliases": {
    "components": "@/components",
    "utils": "@/lib/utils"
  }
}' > components.json
```

18. **Final verification**: Test the setup
```fish
pnpm run dev
```

## Post-Setup Instructions

1. **Configure Supabase**: 
   - Update `.env.local` with your actual Supabase URL and anon key
   - Find these in your Supabase project dashboard under Settings > API

2. **Add shadcn-ui components**: Install components as needed:
   ```fish
   bunx shadcn@latest add button
   bunx shadcn@latest add card
   bunx shadcn@latest add input
   ```

3. **Start developing**: Your project is ready with:
   - ⚡ Vite for fast development
   - ⚛️ React 18 with TypeScript
   - 🎨 Tailwind CSS + shadcn-ui components
   - 🗄️ Supabase integration
   - 📁 Proper path aliases (@/components, @/lib)

The project structure includes:
- Modern React with TypeScript
- Tailwind CSS with shadcn-ui design system
- Supabase client ready for authentication and database operations
- Development server running on http://localhost:5173
