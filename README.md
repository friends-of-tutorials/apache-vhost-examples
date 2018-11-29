# Apache vhost examples

## 1. Variables

### 1.1 HTTP_HOST Redirects "User-agent depended"

Keep the http_host if no special http_user_agent is given. Otherwise rewrite the http_host.

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
