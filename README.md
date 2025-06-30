# MageUnconference NL 2025 notes

## Todo of converting photos into textual notes
- Jeroen - What sucks about Magento Hosting
- Fabian - AI in agencies
- Louis - DB locks
- Jeroen - Surviving Black Friday

## Random links
- https://gamma.app/docs/Unconference-Bulk-AI-Automation-for-ecommerce-7zt94txqbhl37ay
- https://www.npmjs.com/package/@elgentos/magento2-playwright
- https://github.com/elgentos/magento2-playwright
- https://github.com/rajeev-k-tomy/magento-data
- https://github.com/MageTested/mage-unconference-e2e-pipeline
- https://github.com/yireo/Yireo_LokiAdminComponents
- https://github.com/run-as-root/magento2-message-queue-retry
- https://github.com/ho-nl/magento2-ReachDigital_BetterIndexer

## Note on database changes
** By Jelle**
https://github.com/magento/magento2/commit/03892714472bd141b37bb29c7b658014beaa5233
for context: this helps with quicker deployments when you need setup:upgrade for database changes. previously it would drop all db triggers and recreate them, but this was fixed in 2.4.6

## redis, valkey and dragonfly
**Notes by Chris and Nils**

- https://experienceleague.adobe.com/en/docs/commerce-operations/installation-guide/system-requirements states that  in Magento 2.4.7-p6 Valkey 8 can be used as a drop-in replacement for redis. Starting from 2.4.8 redis is erased from the list
- reasons: redis changed to another license and it seems like it annot be used by some cloud providers without fees anxmore (Adobe Commerce Cloud)
- https://valkey.io/ (fork of redis, backed by Amazon)
- https://www.dragonflydb.io/ is a multi threaded plug-in replacement for redis too
- both redis alternatives are fully compatible with the redis API and can be used with Magento

## Checkout
**Notes by Fabian**

HTMX: https://htmx.org/ 
Magento module for HTMX: https://github.com/magehx/htmx-actions

## Low TTFB for uncached Pages
**Notes by Max**

1. n+1 problem
    1. Load a list of products with one query
    2. Then additional queries load more data
    3. Inefficient and slow
    4. Reduce to 1 query
2. At the beginning of the project
    1. Request product data from client **early**
    2. Optimize how data is stored before starting development
3. E-Commerce has a lot of data updates (eg product import)
    1. Hit rate in Cache goes down
    2. Need to optimize the speed of uncached size
4. Think about physical distance to customers
5. Prevent 404 pages!
    1. Internal redirect, so the page is never cached
    2. Move 404 logic into NGinx
6. Use APM tools like New Relic
    1. Collect large data on performance of uncached pages before deciding where to start optimizing
    2. Starting point: APM shows you symptoms, not problems
7. Next step: profiling (eg Tideways)
    1. Identify problems in timeline view
    2. Use callgraph  and callstack to find cause of issue
8. Extensions love to invalidate customer section for no reason, keep an eye on that
    1. Increases Load
    2. If your sever is overloaded, other requests also slow down
9. Utilize varnish esi for blocks
10. DataPreloader
    1. Build a custom module that loads in a single query all the data that you will need
11. Common issue: EavConfig::getAttribute
    1. Solution: set custom attributes via di.xml as needed to be preloaded in the config
12. Performance should not be an afterthought 
    1. Monitor and optimize during every stage

## Tools / Plugins / Browser extensions for Devs
**Notes by Jeroen Vermeulen**

Chrome extensions
- XDev tools
- Alpine Pro 

Magento Development

Local dev Environments
- DDev - integrated with N98MageRun
- Warden
- Docker
- Hypernode Docker
- Valet

Tooling
- N98 MageRun 2
- Magento Performance Test for N98 MageRun 2
- Vincent Pietri magento2-developer-quickdevbar
- Ampersand
- Spatie Ray

Upgrading
- Rector
- Yireo extension checker

IDE
- PHP Storm
- Skeleton models
- AI
- Commandline as much as possible
  - NeoVim = modern version of VIM
    - with plugins
    - AI integration
  - If you do something often, make it easier

Testing
- Playwright
- Multi browser testing online - quite expensive

Security
- Sansec eComScan

Hosting
- Hypernode Brancher
  - Automation on top of it based on the API

Extensions
- Max 20
- Look if extensions are actually used, how often?
- Check if possible with default Magento maybe with a small override
- How good are the vendors?
- Exensions to clean up images etc

Development
- Don't use app/code, create proper extensions
- https://www.yireo.com/blog/2019-05-10-local-composer-development-with-magento2

## BasicRUM
**Notes by Tsvetan**

Group 1:
● Annotations that can indicate when a customer released a new version of their
webshop.
● A summary widget that will show how performance compares between last week and
the week before last week.
● Show more data like DNS, redirect, connect, response time.

Group 2:
● Annotations + 2.
● Magento specific filters +3
○ Page groups: Product, Category, Home, Cart, Checkout …
● Control to change the percentile.
● Show overview/summary per domain when someone monitors multiple domains.
● Third party script impact.
● Server-Timing headers.
● Varnish hit ratio.
● Minimize even more the boomerang js monitoring library. Today we load 30 KB of js. We can go to 20-25 KB.



