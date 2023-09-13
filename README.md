# Sveltekit Navigation Progress Indicator

Utility for showing loading progress to a user in SvelteKit. 

### Why

SvelteKit include an awesome feature called [preloading](https://kit.svelte.dev/docs/link-options). It fetches the code and data for the next page before you even click the link, often leading to instantaneous rendering for the user. 

However there is one big downside: if there is a delay, the user has no visual indication the content is loading. Had we initiated a full page load, the browser itself would shows a loading indicator; since SvelteKit is just requesting the content via Javascript without reloading the page, the browser doesn't know to show it and the user is left waiting.

For short delays there's an uncanny valley where the page seems unresponsive (even though it likely renders the next page faster than a traditional page load). Long delays leave the user wondering if the system registered their click at all.

### Solution

The included `+layout.svelte` can be included in your `src/routes/` directory to add a visual indicator while the page is navigating. It's similar to the the the loading indicator used on YouTube. 

It animates a single small progress div while a navigation is happening. It is rendered in a fixed position at the top of your page so it should have minimal chance of clashing with existing styles/design (but obviously please check that). As soon at the navigation finishes it disappears.

### Design Notes

 - 100ms delay is helpful so it doesn't render for instant page loads, and only when there is a real user perceptible delay
 - The exponential easing is quite helpful. Short loads still see meaningful bar progress, while long page loads still see motion until the end
