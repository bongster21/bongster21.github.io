![Shopping mall dashboard]({{ site.url }}/images/shoppingmall_dashboard.jpg)

We implemented a simple shopping mall dashboard to show some useful analytics. The map is zoomed in very much so you can't see the overall plan, because the data has remain anonymous.

Analytics that will be useful to shopping malls include: 
- Hot and Cold Zone
- Customer Behavior
- Dwell time (footfall, busyness) by shop by zone by floor
- Path Building
- Stay Spots Analysis
- Time of day Profile Analysis
- TOD + Dwell Time
etc.

![Shopping mall dashboard]({{ site.url }}/images/shopping_mall_dwell_time.PNG)

CSS is file is missing on heroku! But it is loading fine on local. :/

First, we set heroku config NODE_ENV to production. But that doesn't seem to solve the problem.

  heroku config:set NODE_ENV=production
  
It looks like the website is not using the build but dev, because the source file does not look like this:
![Shopping mall dashboard]({{ site.url }}/images/shoppingmall_source_code.PNG)


Instead, it complains of a missing .tmp/styles.css file, which should not exist in build.

Things seem properly defined in package.json
![packagejson]({{ site.url }}/images/package_json.PNG)

We finally solved the problem by adding the 'production' environment in app.js so that the code will be run by heroku.
![app_js_smd]({{ site.url }}/images/app_js_smd.PNG)

The strange thing is this didn't give us a problem before...


A view of our another dashboard, which monitors piling progress in a site:
![Shopping mall dashboard]({{ site.url }}/images/pile_dashboard.PNG)
