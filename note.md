

Type of file:
+ ./tap-content/manifest.json
+ ./tap-content/public/assets/**/*.css
+ ./tap-content/src/server/**/**.js
+ ./tap-content/src/server/**/**.json
+ ./tap-content/src/app/**/*.(scss|js)

+ ./tap-iso/manifest-*.json
+ ./tap-iso/public/assets/**/*.(js|css)
+ ./tap-iso/src/**/*.js
+ ./tap-iso/src/app/styles/*j*/*.scss
+ ./jtap-iso/src/app/containers/ContributorPage/contributorPageTemplate.html

+ ./tap-iso-product-affiliate/public/assets/commonJson/loginLandingPageData/my-en.json

+ ./community-web/src/other/localization/locales/ph/common.json


Actual usage: 
+ (MobileDrawer/Hsa/index.js): "url(https://s3.theasianparent.com/tap-assets-prod/wp-content/uploads/sites/12/2015/12/parenting.jpg)"
+ html: href="https://s3.theasianparent.com/tap-assets-prod/wp-content/uploads/sites/12/2015/12/parenting.jpg"
+ json: "https://s3.theasianparent.com/tap-assets-prod/wp-content/uploads/sites/12/2015/12/parenting.jpg"
+ css: background: url("https://s3.theasianparent.com/tap-assets-prod/wp-content/uploads/sites/12/2015/12/parenting.jpg") no-repeat;
+ js: img="https://s3.theasianparent.com/tap-assets-prod/wp-content/uploads/sites/12/2015/12/parenting.jpg"

+ js:
  + object value
  + jsx tag prop
  + string content



For beyeu: 
+ manifest-beyeu.json: 's3.beyeu.com'


community-web .gitignore not contain build folder



## 'cdn-cgi' prompt
getCloudflareUrlForImage: vip_backend, tap-fluencer




































# CDN setup
General setup then per-repo setup

## General setup:
### Infrastructure stand point:
+ Others: Client -> CDN -> AWS Docker container
+ Image: Client -> CDN -> AWS S3

### Code stand point:
Current general usage of cdn link include 3 ways:
#### Static url: has many patterns across file types, see more below
These are patterns that used in listed file type:
- Json: When __ = https://s3
  + "key": "__"
- Css: When __ = https://s3
  + url(__
  + url('__
  + url("__
- Scss: When __ = https://s3
  + url(__
  + url('__
  + url("__
  + ${variable-name}: '__
  + ${variable-name}: "__
- Js:
  When __ = https://s3
  + "__
  + " __
  + '__
  + `__
  + &quot;__
  When __ = //s3
  + '__
  When __ = url(https://s3
  + "__
html ?????

#### SiteConfig/SConfig: could reside in both server or client code (src/config || src/server/config)
Ex: ${CONFIG['region']['s3Prefix']}${CONFIG['region']['logoImage']} (community-web)
    ${user.s3Base}tap-assets/glass-featured-prime-block.png (tap-basic)
    {SiteConfig(this.props.user).site.s3Base + "tap-assets/adult/18plus.png"} (tap-content)

- community-web: src/config/index.js: s3ImgPath
- tap-basic: src/server/config/country.js: s3Base
- tap-community: src/server/config/country.js: s3Base
  This repo looks like doesn't have proper setup for SiteConfig?
- tap-content: 
  + src/server/config/country.js: s3Base
  Using s3Base from userObj: tap-content/src/app/helpers/setUserObj.js
  src/app/components/Layout/Community/Footer/index.js: s3Prefix though cant be found in SiteConfig?
- tap-iso: 
    + src/server/config/country.js: s3Base
    + src/app/helpers/setUserObj.js: s3Base
    + src/server/controllers/ampArticleHtml.js: userObjs3Base could be wrongly used
- tap-iso-product-affiliate: 
    + src/server/config/country.js: s3Base
    + src/app/helpers/setUserObj.js: s3Base
- tapfluencer: src/config/index.js: cloudflare.baseUrl
- vip_backend: 
  + src/config/index.js: cloudflare.baseUrl 
  + vip_backend/src/helpers/getS3CDNPath.js: getS3CDNPath 
- vip_cc_admin:
  + vip_cc_admin/src/server/config/country.js: s3Base
  src/app/components/Layout/Community/Footer/index.js: s3Prefix though cant be found in SiteConfig?
- vip_cc_web: seems no usage
- vip_content_creator_backend: seems no usage

Further per-repo inspection would needed for more detail.

#### URL builder Function: may use SiteConfig internaly
Ex: getS3CDNPath("insufficient_balance_warning.png") (vip_backend)
    getCloudflareUrlForImage(data.productImage, 400) (tapfluencer)


# Proposed
For old:
- Static: 
  + non-js: search/replace old-static to new-static, using regex
  + js: import getImgCdn helper function, then search and replace old usage to in-place funtion call
- SiteConfig/SConfig: use getImgCdn funtion without param
- URL buildder Function: convert it to general version and put to tap-component helper

For new:
Create a tap-component helper function:
function getImgCdn(imgName, width, height, options){
  const cdnDomain = 'cdn.link';
  if (width || height) { /*  */ }
  if (options) { /*  */ }
  return ``
}









#### Some Other Basic Analysis



<!-- s3Base -->
html.replace(/<!-- s3Base -->/g, siteConfigCountry.site.s3Base);
uploadToS3


loop around 1 more time and find src/server/extend/index.js, src/config/index.js




# URL structure
Simply explain url part according to doc

# Image optimizer functions.
Simply explain url structure for img optimizer








