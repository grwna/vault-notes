## CSS Properties
### `order` property
The order property changes the visual sequence of elements. An example use for it is for a sidebar that appears at the top of the screen in mobile but as a true sidebar on desktop.
```html
<div class="flex flex-col md:flex-row"> <div class="order-2 md:order-1">Main Content (Top on Desktop)</div>
  
  <div class="order-1 md:order-2">Sidebar (Top on Mobile)</div>
</div>
```
Notice the `md` part.

## Tidbits to Remember (CSS)
- `align-items` vs `align-self`
- `flex-flow`: a combination of `flex-wrap` and `flex-direction`
- `align-content`:  aligning multiple lines (for wrapped contents)

## Grid vs Flex
Things to remember:
Flex:
- `justify-content`
- `align-content`
- `align-items`

Grid:
- `place-items` 
- `place-content` 
- `grid-column` & `grid-row`
	- `column-start` vs `column-end` (and how using`span` with these works)
	- `grid-column` (start / end) shorthand for both
	- `grid-area`
- 

# Tailwind
## Themes
**Prefixes**
- `--color`: defines colors
- `--font`: defines font variables
- `--radius`
- `--spacing`
- `--width`
- `--text`
- `--font`
- `--font-weight`
- `--leading`
- `--shadow`
- `--blur`
- `--animate`
## Specifity
These offer a solution to the specificity problem of tailwind while also allowing for better reusability. In order from lowest priority to highest:
- `base`
- `components`
- `utility`
Example code:
```css
@layer components {
	.card {
		padding: 1.5rem;
		padding: var(--spacing-6);	
		@apply p-6;
	}
}
```
Note: the properties inside the `.card` components are all equal
## Tidbits to Remember (Tailwind)
- Numbers (i.e `mt-1`) is a unit which equals to 0.25rem. 