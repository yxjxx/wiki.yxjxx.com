Wiki
===========

[My personal wiki, powered by simiki.](http://wiki.yxjxx.com)

1. [Quick Start](http://simiki.org/docs/)
2. [Deploy it to Github Pages](http://simiki.org/docs/deploy.html)
3. My Best Practice

~~~
cd mywiki
simiki new -t "your wiki's title" -c "your wiki's category"
//Write something useful.
git add "related files"
git commit -m "commit message"
git push -u origin master
simike generate
//push /output to gh-pages brance
cd /output
git add .
git commit -m "commit message"
git push -u origin gh-pages
//go to your website, your content will be there.(maybe several minutes later)
~~~
