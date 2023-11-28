# Vue/Nuxt Weather App

A very simple app to get the weather using openmeteo's API built with Vue 3 and Nuxt 3, deployed using Vercel.

[Check out the live app here](https://nuxt-weather-app-zeta.vercel.app/)

## Other implementations

- [React (Remix)](https://github.com/dominikjessen/remix-weather-app)
- [Sveltekit](https://github.com/dominikjessen/svelte-weather-app)

## About this app

This small weather app is part of a series of apps I've built to explore Remix, Nuxt, and Svelte. I mainly build projects using NextJS normally, so out of curiosity I wanted to see how these other frameworks handle things. The remaining parts of the app like weather data API and designs are the same across all of them. This one specifically is built using Vue 3 and Nuxt 3.

## Things I like about Vue/Nuxt at first glance

One thing that I like about Vue/Nuxt is the way it handles component setup (I'm using the script setup syntax because I find that a lot nicer than the verbose setup() function). It creates relatively clear encapsulation and makes it easy to compose apps.

I'm relatively neutral on Vue's reactivity system. It's not quite as cool as Svelte, but marking a variable as a ref is simple enough. What makes me neutral on it is the fact that you have to make sure to change the ref's value, not the value itself due to Vue's proxy nature. With TS this is pretty much a non-issue, but I still don't really like having .value everywhere in my code (which is also why I rarely use useRef in React). Seems like a matter of personal taste though.

I personally think Vue's custom directives (v-if, v-for etc.) make for a very pretty HTML template for components. However, my personal taste is that I enjoy what Svelte and React do a lot more because it makes it very clear where I'm 'stepping out of basic HTML'.

I think one of Nuxt's biggest pros - maybe different in a larger app - is that there don't seem to be too many setup files and folders. The file structure of this app is a lot neater than both the Svelte and Remix one.

## Things I dislike about Vue/Nuxt at first glance

I think the main downside for Vue/Nuxt for me is that there's a lot of "framework-y" stuff versus more JavaScript-y stuff in React and Svelte. Things like watchers, emits and defineProps mean you'll have to know Vue. For React and Svelte it feels a lot more like you simply have to know JS (well).

As I mentioned already, having .value everywhere and not having the visual distinction between HTML and framework/JS stuff is a personal distaste. It reminded me a bit of the old AngularJS ways, which is fine but I prefer React/Svelte here.
