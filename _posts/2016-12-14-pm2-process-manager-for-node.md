---
layout: post
title: 'PM2 : Process manager for Node'
tags: [node, pm2, linux, blog, ghost]
---

While looking at the docs for managing this ghost powered blog, I came across this cool piece of technology called [**PM2**](http://pm2.keymetrics.io/).

It is essentially a process manager for node (as can be gathered from the title :). But it is a sophisticated one at that. It is targeted for production systems and is currently used by tech companies like Paypal and Intuit.

Besides just managing the node processes, restart on crash, start on boot, PM2 also provides app monitoring and a nice terminal based interface.
One of the useful features is the no-downtime reload, which is especially helpful if you are changing the setting of your blog often.
Moreover, it has the ability to remotely deploy your apps as well.
Debugging needed? You have the tailed logs.
Another feature to mention is the cluster mode of operation using which an application can be run by multiple process which are load balanced. This improves the performance of the application.

All in all, if you are using node for some of your applications, a simple `nohup node index.js &`, though simplistic and helpful, might not be the entire solution.

You would need some mechanism to maintain it (keep the process running, recover from crash, monitor memory and CPU usage, etc). And in that case, PM2 would be one of the most comprehensive options out there.

So quickly, some of the helpful command of PM2. A comprehensive list can be found [here](https://github.com/Unitech/pm2#commands-overview).


* **Start a node application** : `pm2 start index.js --name 'app-name'` <br>
In the response, you would get a table, with the name of your application and an `id` attached to it. This could be used to refer to this process.

* **List the applications** : `pm2 list`<br>
Also lists the modules

* **Stop the application** : `pm2 stop id`<br>
It stops the application. But it would still remain in the pm2 grid.

* **Delete the application** : `pm2 delete id`<br>
It stops the application and remove from the grid.

* **Reload the application** : `pm2 reload id`<br>
This restarts the running applications with no downtime. The no-downtime part works only for <u>cluster mode</u> of operation.
`pm2 reload all` to reload all applications.

* **Check the logs** : `pm2 logs id/app-name`<br>
This is equivalent to doing `tail -f`. Logs are polled and printed on screen.
There are also the option of rotating logs. This is done using `pm2-logrotate` module[^3].

* **Monitor** : `pm2 monit`<br>
Monitor the memory and cpu of the running applications.

* **Kill the pm2 process** : `pm2 kill`<br>
Kill all the running applications and pm2 itself.

* **Startup** `pm2 startup`
Detects the platform, generates a startup script and configures the startup system.

* **Starting in cluster mode** `pm2 start -i 4 index.js`<br>
Run the application in a cluster of 4 processes.

* **Scale up the application** : `pm2 scale app-name 10`

###### Ghost specific settings

For normal start, we use the options `--mode=production`. For starting via pm2, this option would not work. For starting in production mode, declare a variable called `NODE_ENV` and set its value to `production`.
Something like this : `export NODE_ENV=production`
After this, run `pm2 start index.js --name=ghost` for starting the ghost via pm2.

For some reason, the cluster mode is not working for ghost. I would have to look more on this.

###### Open Source

One of my foremost metric for evaluation of a library or a product is it being open source. And yes, like all cool stuff I talk about here, PM2 is <u>open source</u>. You can look through it's code [here](https://github.com/Unitech/pm2). It has more than 3000 commits as of date.


Do try this out.

Cheers.

---
1. Code : https://github.com/Unitech/pm2
2. Website : http://pm2.keymetrics.io/
3. Install using `pm2 install pm2-logrotate`. Logs are found here : `~/.pm2/logs`.