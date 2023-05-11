# Next.js 13 Supabase Tailwind Starter

This is a starter template by Tino Ambrecht for using all Next.js 13 features in
combination with a Supabase backend and Tailwind as styling

## Description

With the introduction of Next.js 13, the concept of "client components" and
"server components" was introduced. Here is the difference between the two:

    Client components:
        Client components are components that run directly in the browser.
        They can use React components or other JavaScript frameworks.
        They can retrieve data from the server using APIs or GraphQL.
        They can respond to events in the browser, such as user interactions or changes in the state of the browser.
        Client components are transmitted over the network to the browser, where they are rendered.

    Server components:
        Server components are executed on the server.
        You can use React components or other JavaScript frameworks.
        They can retrieve data from the server using APIs or GraphQL.
        Server components can access databases, external APIs, and other server-side resources.
        They are rendered during build time in static HTML pages or during request in serverless mode.
        Server components can handle sensitive data because they run on the server and are not accessible in the browser.

### Supabase

Go to https://supabase.com and start a New Project.

Retrieve your project URL and anon key in your project's API settings in the
Dashboard to set up the following environment variables. For local development
you can set them in an .env.local file. See an example.

NEXT_PUBLIC_SUPABASE_URL=YOUR_SUPABASE_URL

NEXT_PUBLIC_SUPABASE_ANON_KEY=YOUR_SUPABASE_ANON_KEY

To use Supabase for both client components and server components, there are two
helper functions in the utils folder## supabase-browser.ts

## supabase-browser.ts

This file exports the function `createBrowserClient` which creates an instance
of the Supabase client for the browser. It uses the module
`@supabase/auth-helpers-nextjs` module to provide client-side authentication and
access to the Supabase client. This file is used in a client component.

## supabase-server.ts

This file exports the `createServerClient` function, which creates an instance
of the Supabase client for the server. The function uses modules like
`next/headers` and `@supabase/auth-helpers-nextjs` to perform server-side
authentication and access to the Supabase client. This file is used in a server
component.

## supabase-provider.tsx

This file defines the Supabase provider that provides the Supabase client and
the authentication session. It uses the module `@supabase/auth-helpers-nextjs`
and `react` for the context and the state management. The Supabase provider is
used to provide the Supabase client and session information about the context,
and to use the `useSupabase` hook in components to access it. This file can be
used in both client and server components.

## supabase-listener.tsx

This file defines a component which responds to changes in the authentication
session. It uses the Supabase client and the `useSupabase` hook from
`supabase-provider.tsx` to access the current user status. user state. In
addition, the `next/navigation` module is used module is used to reload the page
if the server and the client are not in are in sync. This file is used in a
client component.

                       +----------------------+
                       | supabase-server.ts   |
                       +----------------------+
                       | createServerClient() |
                       +----------------------+
                                      |
                                      |
                                      v
                       +----------------------+
                       | supabase-browser.ts  |
                       +----------------------+
                       | createBrowserClient()|
                       +----------------------+
                                      |
                                      |
                                      v
                       +----------------------+
                       | supabase-provider.tsx|
                       +----------------------+
                       | SupabaseProvider     |
                       | useSupabase()        |
                       +----------------------+
                                      |
                                      |
                                      v
                       +----------------------+
                       | supabase-listener.tsx|
                       +----------------------+
                       | SupabaseListener     |
                       +----------------------+

    supabase-server.ts:
    This file exports a function called createServerClient that creates a Supabase client to be used on the server-side. The client is configured with headers and cookies and allows access to a Supabase database.

    supabase-browser.ts:
    This file exports a function called createBrowserClient that creates a Supabase client to be used on the client-side (browser). It allows access to the Supabase database from the client-side of the application.

    supabase-provider.tsx:
    This file creates a Supabase provider component that uses React's context API. It exports a context called SupabaseContext and a custom hook called useSupabase. The provider component wraps its children components and provides the Supabase client and session information through the context. The Supabase client is created using the createBrowserClient function from the supabase-browser.ts file.

    supabase-listener.tsx:
    This file exports a component called SupabaseListener that handles the refreshing of server data when the user logs in or out. It imports the useSupabase hook from the supabase-provider.tsx file to access the Supabase client. Inside the useEffect hook, it subscribes to changes in the authentication state of the Supabase client. If the session's access token doesn't match the provided server access token, it refreshes the page to fetch fresh server data. This component relies on the Supabase provider to provide the necessary context.

In a modern Next.js 13 app, these files work together to integrate Supabase functionality into the application. The supabase-server.ts and supabase-browser.ts files provide the client configuration for the server-side and client-side respectively. The supabase-provider.tsx file creates a context provider that makes the Supabase client and session available to the rest of the application. The supabase-listener.tsx file listens for changes in the authentication state and triggers a page refresh when needed. By combining these files, Next.js can leverage Supabase for data storage and authentication in a seamless manner.
