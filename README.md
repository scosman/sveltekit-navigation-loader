# Sveltekit Navigation Progress Indicator

Utility for showing a navigation progress indicator in SvelteKit. 

### Before and After Demo

Before and after shown with an artificial 3s page load delay.

<img src="https://github.com/scosman/sveltekit-navigation-loader/assets/848343/10cc4b33-3c5d-4dd9-846d-718570db2cef" width="400">

<img src="https://github.com/scosman/sveltekit-navigation-loader/assets/848343/e102d331-166f-4a21-82eb-b918116e312d" width="400">

### Why is this needed in SvelteKit projects?

SvelteKit includes an awesome feature called [preloading](https://kit.svelte.dev/docs/link-options). It fetches the code and data for the next page before you even click the link, often leading to instantaneous rendering for the user. It does so by prefetching content via Javascript, then replacing the DOM content instead of doing a full page load.

There is one big downside: if there is a delay, the user has no visual indication the content is loading. Had we initiated a full page load, the browser itself would shows a loading indicator. However, since SvelteKit is just requesting the content via Javascript, the browser doesn't know to show an indicator and the user is left hanging.

For short delays there's an uncanny valley where the page seems unresponsive (even though it likely renders the next page faster than a traditional page load would have). Long delays leave the user wondering if the system registered their click at all.

### Solution

The included `+layout.svelte` can be included in your `src/routes/` directory to add a visual indicator while the page is navigating. It's similar to the loading indicator used on Github and YouTube. 

It animates a single small progress div while a navigation is happening. It is rendered in a fixed position at the top of your page so it likely won't clash with existing styles/design (but obviously please check that). As soon at the navigation finishes it disappears.

### Design Notes

 - 100ms delay is helpful so it doesn't render or flash for instant page loads. The bar only shows up when there is a real user perceptible delay.
 - The exponential easing is quite helpful. Quick loads still see meaningful bar progress even in a few hundred milliseconds, while very long page loads still see the progress bar progressing until the end.
