# React
## Useful Snippets
Some of these snippets are included in `ts_ls` while some of them are custom made. If you want to use the custom made snippets, you can get them at:
## Server vs Client Components

# Next.js
## Tidbits
- Files:
	- `error.tsx` or `global-error.tsx` - custom error pages  
	- `loading.tsx` - custom loading states
	- `not-found.tsx` - custom 404
	- `template.tsx` - not sure what this does to be honest.
-  `NEXT_PUBLIC*` environment variables (for server + client)

## Routing
Routing is done using folders within the `app` directories. Each folder should have a `page.tsx` file. Nested folders mean nested routes.

### Dynamic Routing
You can create dynamic routes (e.g. user ids) using folders named: `[id]`.
The name of the folder inside brackets will be the params used in the page. Example:
```typescript
const Id = async ({params}: {params: Promise<{id: string}>}) => {
    const { id } = await params;
```

### Routing Groups
Routes can be grouped without impacting the url path. This is done by wrapping the group's folder's name with parentheses `()`.
Example:
```bash
.
└── (about)
    └── users
        └── [id]
```
To access `users` you only need to write `/users`, but you can apply route configs (e.g. layouts, errors) to the `about` groups which will affect other routes inside the folder.

### API Routes
To create API routes, you can use `route.ts` under a folder. This folder cannot contain a `page.tsx` as the route defined for the folder now handles json responses and will not handle html responses.
## Layout
Each routes can have their own layout. For example inside the `users` directory, you can add a `layout.tsx` to define the layout that every `/users` routes will have (but not other routes).

## Data Fetching
Server and client components uses different ways to fetch data (Learn more).

## Auth
If using Auth.js, the `auth()` function returns a `session` object.