# Custom React Stack

React has a very rich ecosystem. For anything you want to do, there is probably
a library or a framework available for it. That's great, but having too many
options can also be very confusing. Do you want to start out simple or go for
the ultimate because your app demands it? What's the right set of options for
your specific use case?

This guide will help you build your own custom React stack, explaining key
options and tradeoffs at each step.

Another advantage of this approach is that you will know exactly what's in your
stack. When that new shiny technology comes along, you will be in a better
position to slot it in.

## Our Sample App: Movie Magic

For the purpose of this discussion, imagine that you want to write a movie
streaming app - _Movie Magic_. The app should present the available movie titles
and help users make a choice. It should also allow them to manage their
subscriptions.

Here's a very humble beginning, just two pages:

1. A Home page showing the list of top 10 movies:

![Home Page](assets/home-page.png)

2. A Settings page for users to manage their subscription:

![Settings Page](assets/settings-page.png)

Click [here](https://custom-react-stack.vercel.app/) to test drive the final
application. As you can see, it doesn't do much yet. However, this is good
enough for the purpose of our discussion. Let's start by discussing our
architecture choices.

## Architecture Choices

### Client-Side Rendering (CSR)

![Client-Side Rendering](assets/csr.png)

For simple applications (say with 10-20 pages) you can probably get away with a
Single Page App (SPA) where all the JavaScript is loaded in one shot and
thereafter all rendering takes place client-side. The client makes HTTP requests
to an API server to get any data it needs to render pages. This is called
Client-Side Rendering (CSR). This is also how classic React works.

CSR is simple to develop and simple to deploy (only a static bundle needs to be
deployed to your web server). It's perfect for simple applications. However, the
downside is that the initial render is slow because the entire JavaScript has to
be downloaded before rendering can happen. In technical terms, we have a slow
First Contentful Paint (FCP) and a slow Time to Interactive (TTI). If you are
building a marketing or eCommerce site your users may not have the patience to
wait for the app to load. If that's the case, you should consider SSR.

### Server-Side Rendering (SSR)

![Server-Side Rendering](assets/ssr.png)

In Server-Side Rendering, as the user navigates through the site, the browser
makes requests to the web server to render individual pages. The web server must
connect to the API server and get the data it needs to render pages. It needs to
be smart to compose pages really fast and send them to the browser (unlike CSR,
where the server simply sends a pre-built static bundle to the browser). This
puts a lot more load on the web server. However, the advantage is that the
browser sees its First Contentful Paint (FCP) really fast. The Time to
Interactive (TTI) is still slow because interactions cannot start until the
JavaScript is also sent to the browser (a process called hydration). That's the
tradeoff.

Next.js and Remix are a two of the most popular Server-Side Rendering frameworks
in the React ecosystem.

## Development Build

```bash
npm install
npm run dev
```

Open browser windows at each of the following URLs to see the respective demo
apps:

1. http://localhost:3000/: Movie Magic | React
2. http://localhost:3001/: Movie Magic | Next.js
3. http://localhost:3002/: Movie Magic | Remix

Note that the React app fetches mock data from MSW, whereas the other two apps
fetch real data from the movie-magic-api.

> Note: Do not run `npm install` in any of the subdirectories. It will break the
> build. There should be only one `package-lock.json` file in the entire repo
> (at the root).

## Production Build

To build all apps and packages, run the following command:

```bash
npm install
npm run build
```

## Clean Build

Removes all build artifacts and performs a clean build.

```bash
npm run clean
npm install
npm run dev
```

For an "aggressive" clean build, add one more step as shown below. This wil
build the lock file from scratch.

```bash
npm run clean
rm package-lock.json
npm install
npm run dev
```

## Running Storybook

```bash
cd storybook
npm install
npm run storybook  # you can also run it from the root directory
```

## Running Unit Tests

```bash
npm run test
```

## Running End-to-End Tests

```sh
npm run dev # starts a local server hosting the react app

# run cypress in a different shell
npm run cypress
```

## Code Formatting

```sh
npm run format
```
