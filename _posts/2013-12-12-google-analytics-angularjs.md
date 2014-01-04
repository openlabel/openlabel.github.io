---
layout: post
title: Google Analytics with AngularJS
cover: cover.png
date:   2013-12-12 12:00:00
categories: posts
tags: engineering
---

## AngularJS and Google Analytics

Since AngularJS is a single page application framework, navigating from page to page on an AngularJS site doesn't result in full page reloads. All of the page resources are typically downloaded at first load of the page or as fragments on the fly.

This trips up Google Analytics, which typically tracks page views with a script element like the one below embedded in each page that is expected to run when the page loads:

{% highlight html %}
    <script>
      (function(i,s,o,g,r,a,m){i['GoogleAnalyticsObject']=r;i[r]=i[r]||function(){
      (i[r].q=i[r].q||[]).push(arguments)},i[r].l=1*new Date();a=s.createElement(o),
      m=s.getElementsByTagName(o)[0];a.async=1;a.src=g;m.parentNode.insertBefore(a,m)
      })(window,document,'script','//www.google-analytics.com/analytics.js','ga');
      
      ga('create', 'UA-XXXXXX-Y', 'mysite.com');
      ga('send', 'pageview')
    </script>
{% endhighlight %}


But in a single page appplication, this script only gets executed once when the page downloads.  No good.

Fortunately we can fix this by hooking up some code to the AngularJS $routeChangeSuccess event and fire the ga() tracking code from there. The code can be wrapped up neatly in a directive:

{% highlight javascript %}
app.directive('analytics', ['$rootScope', '$location',
	function ($rootScope, $location) {
	return {
		link: function (scope, elem, attrs, ctrl) {
			$rootScope.$on('$routeChangeSuccess', function(event, currRoute, prevRoute) {
			    ga('set', 'page', $location.path());
				ga('send', 'pageview');
			});
		}
	}
}]);
{% endhighlight %}

and attached to the page like so:

{% highlight html %}
<body ng-app="myApp" analytics>
{% endhighlight %}


Wallah! Your visitors will now be tracked throughout your single page application.


## Prevent double counting index views

It is also a good idea to remove the ga('send', 'pageview') line from the original script block to prevent double counting index views, since the $routeChangeSuccess event will get fired on the first page load.
