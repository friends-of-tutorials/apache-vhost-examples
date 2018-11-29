# Apache vhost examples

## 1. Variables

Some Basics:

```
# default
RewriteRule .* - [ENV=url:%{HTTP_HOST}]

# overwrite if the conditions are met (RewriteCond). 
RewriteCond ...
RewriteCond ...
RewriteRule .* - [ENV=url:test.domain.de]

...
```

### 1.1 Example: User-agent dependent redirects

Always redirect to current http_host. If a special user-agent is given, rewrite the current http_host.

```
# url = save current http_host (directly requested "-origin" url should keep the "-origin" url)
RewriteRule .* - [ENV=url:%{HTTP_HOST}]

# url = redirect url without "-origin" if http_user_agent is "Amazon CloudFront"
RewriteCond %{HTTP_USER_AGENT} "Amazon CloudFront"
RewriteCond %{HTTP_HOST}       "^test-origin.domain.de$"
RewriteRule .* - [ENV=url:test.domain.de]

# url = redirect url without "-origin" if http_user_agent is "Amazon CloudFront"
RewriteCond %{HTTP_USER_AGENT} "Amazon CloudFront"
RewriteCond %{HTTP_HOST}       "^www-origin.domain.de$"
RewriteRule .* - [ENV=url:www.domain.de]

# Redirect to non-html if *.html is given
RewriteCond %{THE_REQUEST} /([^.]+)\.html [NC]
RewriteRule ^ https://%{ENV:url}/%1 [NC,L,R]
```

## A. Authors

* Björn Hempel <bjoern@hempel.li> - _Initial work_ - [https://github.com/bjoern-hempel](https://github.com/bjoern-hempel)

## B. Licence

This tutorial is licensed under the MIT License - see the [LICENSE.md](/LICENSE.md) file for details

## C. Closing words

Have fun! :)
