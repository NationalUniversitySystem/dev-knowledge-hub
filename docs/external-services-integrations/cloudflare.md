# Cloudflare

Once a code release for NU has been deployed, it's highly recommended to purge the cache in Cloudflare. To do so, you would need to follow the steps below:

- [Log in to Cloudflare](https://dash.cloudflare.com/login) and select the `nu.edu` site:

![CloudFlare](../_images/cloudflare-01.png)

- Select `Purge Cache` from the **Quick Actions** menu

![CloudFlare](../_images/cloudflare-02.png)

- Click `Purge Everything`

![CloudFlare](../_images/cloudflare-03.png)

- And then confirm

![CloudFlare](../_images/cloudflare-04.png)

## RocketLoader

To improve site performance, we use Cloudflare's RocketLoader functionality. This can be toggled on/off via the Cloudflare dashboard (under 'Speed').

Problem: Rocketloader works in part by blocking javascript from loading until after the page has rendered. This causes one of our custom gutenberg blocks to break: horizontal-card-slider, breaking both the styling and the scroll functionality. 

Rocketloader allows you to tell it to skip certain javascript by adding a data-cfasync=true attribute to the <script> tag. This sounds simple but there are two extra layers we need to dig through:
  1) Since we're including the script via wp_enqueue_script, our <script> tag is dynamically generated, rather than a hardcoded line in the code. We can get around this by adding a script_loader_tag filter in functions.php that will add data-cfasync=true to specified javascripts. Reference  (https://techorbiter.com/how-to-exclude-any-wordpress-script-from-cloudflare-rocket-loader/4291/)
  2) WPVIP has a filter than runs on javascript includes, which concatenates/minifies/caches them to boost site performance. We need to bypass this for this javascript include, in order for the solution above to work. This is also accomplished in fuctions.php via the js_do_concat filter. Reference (https://docs.wpvip.com/technical-references/vip-platform/file-concatenation-and-minification/) 
