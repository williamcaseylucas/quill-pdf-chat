# Quill

## packages

- bun add clsx tailwind-merge
- bun add tailwindcss-animate @tailwindcss/typography
- bun add lucid-react
- bun add @kinde-oss/kinde-auth-nextjs
- bun add @clerk/nextjs
- bun add react-loading-skelton
  - have to import this in layout.tsx
- bun add date-fns
- bun add react-pdf

### Shadcn

- bunx shadcn-ui@latest init
- bunx shadcn-ui@latest add button
- bunx shadcn-ui@latest add dialog

### Prisma

- bunx prisma init
- bunx prisma generate
- bunx prisma db push
- bunx prisma studio

## react PDF

## Date-fns

- format(new Date(file), 'MMM yyyy')

## Get user information passed as context in objects for TRPC calls

- logic in src/trpc
- allows us to use User context later
- good for privateProcedures

## login flow

- Dashboard redirects to auth-callback
- We check if the user is logged in with Clerk
  - If yes, we create a new user if they don't exist in the db
  - If no, we redirect them to the sign in page
- Then we send back to the dashboard
  - If the user doesn't exist in the db still, send em' right back
  - Otherwise render the page content

## data base alternatives

- cockroachlabs -> sql w/ no credit card required
- neon.tech -> postgresql alternative

## prisma

- commands
  - bunx prisma migrate dev --name init
    - locally sync changes with name of "init'
    - calls it dev.db
  - bunx prisma studio
  - bunx prisma db push
- src/db/index.ts is where PrismaClient has been created
- planetscale doesn't support 'foreign key constraints"
  - add relationMode: "prisma"
- if you have a User model and an Article model
  - author User @relation(fields:[authorId], references: [id])
  - authorId Int
    - Will make "author" reference User
    - Will make "authorId" reference User id
    - when using "connect" keyword for author, it will populate authorId
  - using "include" allows additional objects to be included
- go to json and add
  - {
    "editor.formatOnSave": true,
    "[typescript]": {
    "editor.defaultFormatter": "esbenp.prettier-vscode"
    },
    "[typescriptreact]": {
    "editor.defaultFormatter": "esbenp.prettier-vscode"
    },
    "[javascript]": {
    "editor.defaultFormatter": "esbenp.prettier-vscode"
    },
    "[prisma]": {
    "editor.defaultFormatter": "Prisma.prisma"
    },
    }

## bun

- much faster than pnpm
- bun create next-app
- bun install
- bun add \_
- bun run build

- layout alternative to React.ReactNode -> PropsWithChildren
  - { children }: { children: React.ReactNode }
  - { children }: PropsWithChildren

## trpc

- https://trpc.io/docs/client/nextjs/setup
- add index.ts and trpc.ts in /src directory
- add Providers.tsx in components that wraps TRPC instance around your entire app
  - Good to wrap QueryClientProvider as child so that we can use that seperately later
- have trpc instance within app in (trpc)
- add route handlers for /api route
  - https://trpc.io/docs/server/adapters/nextjs#route-handlers
  - create /app/api/trpc/[trpc]/routes.ts
- /src/trpc/index.ts is where you create procedures to call
- reference db from Prisma now in trpc/index.ts
- trpc.useUtils() can be used to cause react query to reftech from db and update page without completely refreshing
  - example in src/components/dashboard

## urls

- /auth-callback?origin=dashboard
  - for reauthentication with origin being back to the dashboard (where the user currently is)
- use router to push urls
- use useSearchParams() to get queries from the url

## Clerk (supposed to be Kinde) (auth)

- using clerk instead since Kinde was having 500 errors
- can't grab {user} from auth(), instead grab user from await currentUser() with async function instead

## shadcn

- ui.shadcn.com
  - go to themes
  - copy and paste over everything
- add to Link button styles
  - buttonVariants({ size: "lg", className: "mt-5" })
- asChild allows you to create custom button instead of preconfigured button
  - would be button in button otherwise

## images

- fill or width, height
- dimensions of image when it is open is on the bottom right

## tailwind

- added components to config.ts
- can add style clipPath to give gradient some direction (app/page.tsx)
- flow-root
  - good to add to parent of "float" divs
- inset-x-0 makes the child element (that has this class applied) stretch to fill its "relative" parent completely
- gradients
  - bg-gradient-to-r from-cyan-500 to-blue-500
- truncate
  - cuts content off if they are too long
- flex-1
  - tries to take up as much space as possible
- flex-[0.75]
  - if flex-1 vs flex-[0.75]
    - left will take up slightly more room than the right
