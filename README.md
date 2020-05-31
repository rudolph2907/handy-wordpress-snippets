# A list of hand WordPress Snippets

A list of handy WordPress snippets you can add to your theme or plugin, without having to install extra plugins.

## Contact 7
- Enable loading contact form 7  assets only for pages that need them:

```php
add_action( 'wp_print_scripts', 'deregister_cf7_javascript', 100 );
    function deregister_cf7_javascript() {
		//Add page slugs or ids you want to allow to array
        if ( !is_page(array(8,10)) ) {
            wp_deregister_script( 'contact-form-7' );
        }
    }
```   
```
    add_action( 'wp_print_styles', 'deregister_cf7_styles', 100 );
    function deregister_cf7_styles() {
		//Add page slugs or ids you want to allow to array
        if ( !is_page(array(8,10)) ) {
            wp_deregister_style( 'contact-form-7' );
        }
    }
```

- Completely disable Contact Form 7 stylesheet:
```php
add_action( 'wp_print_styles', 'nd_cf7_deregister_styles', 100 );
function nd_cf7_deregister_styles() {
    wp_deregister_style( 'contact-form-7' );
}
```

- Disable recaptcha on pages that does not have a form
```php
add_action('wp_print_scripts', 'nd_cf7_disable_recaptcha_for_pages);
function nd_cf7_disable_recaptcha_for_pages() {
	//Add page slugs or ids you want to allow to array
	if ( !is_page( array( 'contact','some-other-page-with-form' ) ) ){
		wp_dequeue_script( 'google-recaptcha' );
	}
}
```

## Google Analytics
- Add Google Analytics script

```php
add_action( 'wp_head', 'nd_ga_add_google_analytics', 10 );
function nd_ga_add_google_analytics() { ?>
  <script>
  (function(i,s,o,g,r,a,m){i['GoogleAnalyticsObject']=r;i[r]=i[r]||function(){
  (i[r].q=i[r].q||[]).push(arguments)},i[r].l=1*new Date();a=s.createElement(o),
  m=s.getElementsByTagName(o)[0];a.async=1;a.src=g;m.parentNode.insertBefore(a,m)
  })(window,document,'script','https://www.google-analytics.com/analytics.js','ga');

  // Add you Google Analytics Tracking Code
  ga('create', 'UA-xxxxxxxx-x', 'auto');
  ga('send', 'pageview');

    </script>
  <?php } ?>
```  

## Facebook Pixel
- Add Facebook Tracking Pixel

```php
add_action( 'wp_head', 'nd_fb_add_facebook_pixel', 10 );
function nd_fb_add_facebook_pixel() { ?>
<!-- Facebook Pixel Code -->
<script>
  !function(f,b,e,v,n,t,s)
  {if(f.fbq)return;n=f.fbq=function(){n.callMethod?
  n.callMethod.apply(n,arguments):n.queue.push(arguments)};
  if(!f._fbq)f._fbq=n;n.push=n;n.loaded=!0;n.version='2.0';
  n.queue=[];t=b.createElement(e);t.async=!0;
  t.src=v;s=b.getElementsByTagName(e)[0];
  s.parentNode.insertBefore(t,s)}(window, document,'script',
  'https://connect.facebook.net/en_US/fbevents.js');
  
  // Add your Facebook Tracking ID here
  fbq('init', 'xxx');
  fbq('track', 'PageView');
</script>

// Add your Facebook Tracking ID here
<noscript><img height="1" width="1" style="display:none"
  src="https://www.facebook.com/tr?id=xxx&ev=PageView&noscript=1"
/></noscript>
<!-- End Facebook Pixel Code -->
  <?php } ?>
```  

If you have any handy snippets you'd like to share please feel free to submit a pull request.
