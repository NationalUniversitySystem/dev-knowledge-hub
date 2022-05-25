# Cloudflare

> ### Notes from Todd (TBF)

**How You Are Using It Now**

From our review Cloudflare is currently set up and running on the following sites:
- india.nu.edu
- www.india.nu.edu
- www.nu.edu
- info.nu.edu
- nusaweb.dev (we don't know what this is)

Cloudflare is used on these sites for caching JS, CSS, fonts, and Images. The HTML is not cached.  WPVIP is currently caching the HTML.

All those sites are hosted by WPVIP.  WPVIP is a premium provider that provides enterprise-level security and caching (CDN).  All the basic work Cloudflare is doing is replicated by WPVIP.  If we discontinued Cloudlare, WPVIP would be able to cache JS, CSS, fonts, and images.

The benefit of Cloudflare is that it provides more insights and tools to improve security and cache than WPVIP.  While WPVIP handles all the basics, it doesn't provide a lot of insights into what is happening on the security front.  So we do find Cloudflare to be useful.

**Your Plan**

As you know, you are currently on an enterprise plan that costs $54,000 per year.  It looks like the plan allows you to use Cloudflare for up to 32 domains.  You are currently using this on only three domains (nusaweb.dev, nu.edu, and nupolytech.org which was never set up and redirects to a page on the NU website) since most of the sites are subdomains off of www.nu.edu.  

Cloudflare offers a Business plan that costs $200 per month per domain.  The main benefits of the Enterprise plan over the Business plan are (a) it offers white glove customer support and (b) it would save you money if you actually had the service set up on the 32 domains allowed in your plan.  If you actually set up Cloudflare on 32 domains, the Business plan would cost $76,800 compared to the $54,000 per year you are paying.  If we downgraded to the Business plan and kept the three domains we have currently set up, we would be looking at a cost of $7,200 per year.

**Recommendation**

To state the obvious, you are currently paying for a bunch of services you aren't using.  You have way more domains than you need and as far as we are aware no one is using the enhanced customer service they offer.  Assuming you don't intend to expand how you use Cloudflare, we recommend the following:
- Keep using Cloudflare on www.nu.edu but downgrade to the $200 per month Business Plan.  This way we will have access to the enhanced tools but will save a lot of money.
- Stop using Cloudflare altogether on the other two domains (nusaweb.dev and nupolytech.org).  So make this change we would need to transition the DNS for these two sites to be served by WP VIP instead of Cloudflare.

Note I suspect you could also keep the Enterprise plan and greatly reduce costs if you told them you just wanted to use it on  www.nu.edu instead of the 30+ sites you are contracted for.
