# MageUnconference NL 2025 notes

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
```
