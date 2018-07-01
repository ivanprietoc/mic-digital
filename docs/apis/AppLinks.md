FORMAT: 1A

# AppLinks
App links API is a bridge to create [applinks](http://applinks.org/) pages created on the fly on apigee, with  [open graph](http://ogp.me/) meta tags added.
This allows our apps to share links which look good on social networks and allow linking between apps and to the platforms "app store" with a clear standard.
# Group Applinks
App links requires previous configuration on the proxy to 'onboard' an APP and enable it to use the service.
The onboarding requires getting information on the app that will be linking:

    {
    app_key_name:{name:"app name as will be shown",
                  ios_url:"ios_app_url_scheme://",
                  android_url:"android_app_url_scheme://",
                  web_url:"app_web_url_fallback",
                  ios_id:'app_store_id_if_it_exists',
                  android_package:"android.package.name",
                  twitter_acct:"@twitter_origin_account",
                  add_path_to_web:0, 
                  add_qs_to_web:0,
                  app_img:"app_image_url"
                 },
       
    };
With these configs in place, the app can then use the GET endpoint below when sharing.

The `add_path_to_web` flag will determine if the proxy will concatenate the `path` in the call will be added to the `web_url` meta tags.

The `add_qs_to_web flag` will determine if the proxy will add the `querystring` sent in the call to the `web_url` meta tag.

`path` and `querystring` if present, are added to the android and ios url scheme.

Existance of the `ios_id` will determine if the twitter IOS links are created.

Twitter links have to first be validated in the [twitter cards validator](https://cards-dev.twitter.com/validator), they must have 0 errors before validating. They will not show if not valid.

## applinks Collection [/applinks/{app_key_name}/{article_name}/{path}?{querystring}]
### Get Applinks [GET]
+ Response 200 (text/htm)

        <html>
           <head>
              <title>article_name</title>
              <meta property="al:ios:url" content="ios_app_url_scheme://path?querystring" />
              <meta property="al:ios:app_name" content="app name as will be shown" />
              <meta property="al:android:url" content="android_app_url_scheme://path?querystring" />
              <meta property="al:android:package" content="android.package.name" />
              <meta property="al:android:app_name" content="app name as will be shown" />
              <meta property="al:web:url" content="app_web_url_fallback" />
              <meta property="al:web:should_fallback" content="false" />
              <meta property="twitter:image:src" content="img_url"/>
              <meta name="twitter:app:name:googleplay" content="app name as will be shown">
              <meta name="twitter:app:id:googleplay" content="android.package.name">
              <meta name="twitter:app:url:googleplay" content="android_app_url_scheme://path?querystring">
              <meta http-equiv="refresh" content="0;url=app_web_url_fallback" />
              <!-- equivalent twitter IOS meta tags if ios app ID exists in config !-->
              <meta property="og:image" content="app_image_url"/>
           </head>
           <body>Redirecting...</body>
         </html>


