---
layout: post
title: "Yippie Yah Yei, Schweinebacke!"
description: "I finally created my first Github Page."
date: 2018-07-09
---

Well. I finally created my first Github Page.

It was quite easy so that there is not much to write about it. The only thing to note
is how to test the page on a local machine before pushing it to Github.

Because I do not want to install Jekyll on my OS I chose to use the Jekyll Docker
image to build the site locally:

{% highlight bash %}
docker run --rm --name jekyll-serve \
    -v $PWD:/srv/jekyll \
    -p 4000:4000 jekyll/jekyll jekyll serve\
    --force_polling # --force_polling only needed on Windows
{% endhighlight %}

As long as the Docker container is running you can see all changes on your page in no
time at http://localhost:4000/.

After work you can stop the Jekyll container with:

{% highlight bash %}
docker stop jekyll-serve
{% endhighlight %}
