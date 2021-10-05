# Wordpress

## Code Development
### Hooks
There are two types of hooks in WordPress, filters and actions.
- "Filters" must return something. You are literally filtering an existing object, value, array, etc. It might be an empty string or array, but the filter and it's parameters will be passing something to it.

```php
/**
 * Manipulate or trigger code based on the context of the content.
 *
 * @param string $the_content The good old content of any WP object.
 */
add_filter( 'the_content', function( $the_content ) {
	// Alter the content, append something to the content, check for something via a global $post to trigger other code, etc.
	return $the_content;
}, 10, 1 );
```
- "Actions" do not return anything specific, can have returns to escape the function/method like in a return pattern.

```php
/**
 * Manipulate or trigger code based on the context of the content.
 */
add_action( 'wp_enqueue_scripts', function() {
	// Enqueue general theme styles
	wp_enqueue_style( 'national-university', get_template_directory_uri() . '/assets/css/theme.min.css', [], filemtime( get_template_directory() . '/assets/css/theme.min.css' ) );

	// Enqueue specific styles for a page.
	if ( is_page( 'campaign-name' ) ) {
		wp_enqueue_style( 'campaign-name-styles', get_template_directory_uri() . '/assets/css/campaign-name.min.css', [], filemtime( get_template_directory() . '/assets/css/campaign-name.min.css'; ) );
	}
}, 999 );
```
- Pay close attention to the priority and parameters when defining hooks (and the defaults).
	- The default priority is 10.
	- The default parameter number is 1.
	- If the defaults will be used, no need to declare them.
	- If a callback has more than 1 parameter you will need to define that in the hook declaration.
	```php
	// No deafult priority nor parameter used.
	add_filter( 'the_content', function( $the_content ) {
		return $the_content
	} );

	// Lower number in priority so it executes earlier than the standard "10" and declare the number of parameters.
	add_filter( 'wp_kses_allowed_html', function() {
		if ( 'post' === $context ) {
			$allowed['img']['data-src']  = true;
		}

		return $allowed;
	}, 5, 2 )
	```


### Enqueueing assets
- When enqueuing **JS** assets, make sure to decide whether or not those files need to be loaded/ with `defer` or `async` attribute.
- Load those with the `script_loader_tag` filter

```php
/**
 * Allows enqueued scripts to be deferred or loaded asynchronously, thus preventing the
 * page from being blocked by js calls.
 *
 * @param  string $tag    The <script> tag for the enqueued script.
 * @param  string $handle The script's registered handle.
 * @param  string $src    The script's source URL.
 *
 * @return string The formatted HTML script tag of the given enqueued script.
 */
add_action( 'script_loader_tag', function( $tag, $handle, $src ) {
		$async_scripts = [
			'script-handle-1',
		];
		if ( in_array( $handle, $async_scripts, true ) ) {
			return str_replace( ' src', ' async="async" src', $tag );
		}

		$defer_scripts = [
			'script-handle-2',
			'script-handle-3',
		];
		if ( in_array( $handle, $defer_scripts, true ) ) {
			return str_replace( ' src', ' defer="defer" src', $tag );
		}
}, 10, 3 );
```

---

## Admin side (content management)
### Images
- When uploading images, add _at least_ an `alt` value. This is for accessibility purposes and because we use the caption and/or alt values to display text on every image.
- Rename the files so they are easier to search for. Usually utilizing the image subject's name and activity.
	- Example: "louis g. in class room"
	- If you were not provided with the image subject's name, ask for it from the design team or find on [Photoshelter](https://natuniv.photoshelter.com/index).
	- Optimize the image through some of our online tools or Photoshop for web settings with 80-90 percent judging your best for un-noticeable pixelation.

### URL Slugs
WP automatically generates a slug for pages. Sometimes you may receive a copy deck that has a lengthy Title (h1) which would end up having an automatically generated slug of 5+ words. This is bad UX for several reasons. That may include trying to type, write, or say the link and SEO purposes.
You can edit the WP generated slug to the requested one, _or_ if none was requested and it's a long URL, shorten it to keyword of the title or the content.

This should be applied to any type of website, not just WP.

Although this should be common knowledge as part of dev, we are also a team with beginners into the web dev world.
There are also a lot of resources online and therefore that can be looked up online.
A few examples:
- https://yoast.com/slug/
- https://prettylinks.com/url-slugs-and-how-to-use-them/
- https://webmasters.stackexchange.com/a/68425
