# Apache vhost examples

## 1. Variables

### 1.1 User-agent depended http_host

Keep the http_host if no special http_user_agent is given.

```
# url = save current http_host
RewriteRule .* - [ENV=url:%{HTTP_HOST}]

# url -> stage amazon cloud redirect
RewriteCond %{HTTP_USER_AGENT} "Amazon CloudFront"
RewriteCond %{HTTP_HOST}       "^test-origin.domain.de$"
RewriteRule .* - [ENV=url:test.domain.de]

# url -> live amazon cloud redirect
RewriteCond %{HTTP_USER_AGENT} "Amazon CloudFront"
RewriteCond %{HTTP_HOST}       "^www-origin.domain.de$"
RewriteRule .* - [ENV=url:www.domain.de]

# Redirect to non-html
RewriteCond %{THE_REQUEST} /([^.]+)\.html [NC]
RewriteRule ^ https://%{ENV:url}/%1 [NC,L,R]
```

## A. Authors

* Björn Hempel <bjoern@hempel.li> - _Initial work_ - [https://github.com/bjoern-hempel](https://github.com/bjoern-hempel)

## B. Licence

This tutorial is licensed under the MIT License - see the [LICENSE.md](/LICENSE.md) file for details

## C. Closing words

Have fun! :)
