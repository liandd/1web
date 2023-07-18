---
title: "About"
permalink: /about/
date: 2023-07-13
---

# theme                  : "minimal-mistakes-jekyll"
remote_theme             : "mmistakes/minimal-mistakes@4.15.1"
minimal_mistakes_skin    : "haxor" # "air", "aqua", "contrast", "dark", "dirt", "neon", "mint", "plum", "sunrise"

# Site Settings
locale                   : "en-US"
title                    : "Juan Garcia | Mi Blog"
title_separator          : "-"
name                     : "Juan David Garcia Acevedo"
description              : "Publicaciones sobre seguridad, CTFs y redes"
url                      : "https://liandd.github.io" # the base hostname & protocol for your site e.g. "https://mmistakes.github.io"
baseurl                  : # the subpath of your site, e.g. "/blog"
repository               : "liandd/liandd.github.io" # GitHub username/repo-name e.g. "mmistakes/minimal-mistakes"
logo                     : "/assets/images/masthead.png"
teaser                   : # path of fallback teaser image, e.g. "/assets/images/500x300.png"
breadcrumbs              : true # true, false (default)
words_per_minute         : 200
comments:
  provider               : false # false (default), "disqus", "discourse", "facebook", "google-plus", "staticman", "staticman_v2" "custom"
  disqus:
    shortname            : # https://help.disqus.com/customer/portal/articles/466208-what-s-a-shortname-
  discourse:
    server               : # https://meta.discourse.org/t/embedding-discourse-comments-via-javascript/31963 , e.g.: meta.discourse.org
  facebook:
    # https://developers.facebook.com/docs/plugins/comments
    appid                :
    num_posts            : # 5 (default)
    colorscheme          : # "light" (default), "dark"
staticman:
  allowedFields          : # ['name', 'email', 'url', 'message']
  branch                 : # "master"
  commitMessage          : # "New comment."
  filename               : # comment-{@timestamp}
  format                 : # "yml"
  moderation             : # true
  path                   : # "/_data/comments/{options.slug}" (default)
  requiredFields         : # ['name', 'email', 'message']
  transforms:
    email                : # "md5"
  generatedFields:
    date:
      type               : # "date"
      options:
        format           : # "iso8601" (default), "timestamp-seconds", "timestamp-milliseconds"
reCaptcha:
  siteKey                :
  secret                 :
atom_feed:
  path                   : # blank (default) uses feed.xml
search                   : # true, false (default)
search_full_content      : # true, false (default)
search_provider          : # lunr (default), algolia, google
algolia:
  application_id         : # YOUR_APPLICATION_ID
  index_name             : # YOUR_INDEX_NAME
  search_only_api_key    : # YOUR_SEARCH_ONLY_API_KEY
  powered_by             : # true (default), false
google:
  search_engine_id       : # YOUR_SEARCH_ENGINE_ID
  instant_search         : # false (default), true
# SEO Related
google_site_verification :
bing_site_verification   :
yandex_site_verification :
naver_site_verification  :

# Social Sharing
twitter:
  username               :
facebook:
  username               :
  app_id                 :
  publisher              :
og_image                 : # Open Graph/Twitter default site image
# For specifying social profiles
# - https://developers.google.com/structured-data/customize/social-profiles
social:
  type                   : # Person or Organization (defaults to Person)
  name                   : # If the user or organization name differs from the site's name
  links: # An array of links to social media profiles

# Analytics
analytics:
  provider               : "google" # false (default), "google", "google-universal", "custom"
  google:
    tracking_id          : "UA-145129883-1"
    anonymize_ip         : false # (default)


# Site Author
author:
  name             : "Juan Garcia"
  avatar           : "/assets/images/avatar.png"
  bio              : "Ingeniería en Sistemas y Telecomunicaciones CTFs player<br>Entusiasta en CiberSeguridad"
  location         : "Colombia"
  email            : "tdetde20@gmail.com"
  uri              :
  home             : # null (default), "absolute or relative url to link to author home"
  bitbucket        :
  codepen          :
  dribbble         :
  flickr           :
  facebook         :
  foursquare       :
  github           : "liandd"
  gitlab           :
  google_plus      :
  keybase          : #""
  instagram        :
  lastfm           :
  linkedin         : "juan-garcia-b1437a262/" # "john-doe-12345678" (the last part of your profile url, e.g. https://www.linkedin.com/in/john-doe-12345678)
  pinterest        :
  soundcloud       :
  stackoverflow    : # "123456/username" (the last part of your profile url, e.g. https://stackoverflow.com/users/123456/username)
  steam            : # "steamId" (the last part of your profile url, e.g. https://steamcommunity.com/id/steamId/)
  tumblr           :
  twitter          : #""
  vine             :
  weibo            :
  xing             :
  youtube          : "https://www.youtube.com/@liandd"

