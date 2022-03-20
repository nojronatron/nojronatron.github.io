# Notes from Duckett HTML and JS Books

Notes taken from Duckett HTML Book:
[Chapter 16: “Images” (pp.406-427)](#chapter-16-images)  
[Chapter 19: "Practical Information" (pp.476-492)](#chapter-19-practical-information)  
MDN Article: [Video and Audio APIs](https://developer.mozilla.org/en-US/docs/Learn/JavaScript/Client-side_web_APIs/Video_and_audio_APIs)  
Skim over [Chapter 9: pp.201-206 re: Flash (as a history lesson)](#chapter-9-flash)  

## Chapter 16: Images

Keep your HTML markup clean by using CSS to control the placement, style, and orientation of images on the website.  

### Controlling Image Size using CSS

The `width` or `height` properties in CSS control image size and help the browser to load the page more efficiently.  
Use CSS classes names "small", "medium", and "large" to pre-determine 3 common image sizes for the site and apply those classes in the HTML markup.  

### Aligning Images using CSS

Two common ways to achieve image alignment, in conjunction with small, medium, and large image size classes:  

1. Apply float to the small, medium, large class.  
2. Create new descriptive classes that set `align-left` or `align-right` properties.  

An example from *[Duckett, pg.411]*:  

```css
img.align-left {
  float: left;
  margin-right: 10px;
}
img.align-right {
  float: right;
  margin-left: 10px;
}
img.medium {
  width: 250px;
  height: 250px;
}
```

Image block type are *inline* by default, so in order to center, change to `block level` instead.  

An example from *[Duckett, pg.412]*:

```css
img.align-center {
  display: block;
  margin: 0px auto;
}
img.medium {
  width: 250px;
  height: 250px;
}
```

### Background Images

To place an image *behind* another element use `background-image`.  
Images set via background-image will attempt to fill their parent container.  
Require a valid path to the file using syntax `url("")`.  

```css
section {
  background-image: url("img/my-logo.png");
}
```

Background images can be repeated several ways, not repeated, fixed in place, or scrollable by the users mouse.  
`background-repeat` accepts values of: repeat; repeat-x; repeat-y; or no-repeat.  
`background-attachment` accepts values of: fixed or scroll.  

```css
.norepeat {
  background-repeat: no-repeat;
}
.repeat-xplane {
  background-repeat: repeat-x;
}
.scroll-pic {
  background-attachment: scroll;
}
```

Shorthand can be used to lump-together the following:  

1. `background-color`
2. `background-image`
3. `background-repeat`
4. `background-attachment`
5. `background-position`

### Image Rollovers and Sprites

A Sprite is made up of several images that can be programed to create an illusion of animation.  
Set a background image on an element and set three styles to get a rollover effect *[Duckett, pgs.417-418]*:

```css
a.button {
  height: 36px;
  background-image: url("");
  text-indent:-9999px;
  display: inline-block;
}
a#add-to-basket {
  width: 174px;
  background-position: 0px 0px; /* used to move image into and out of viewport */
}
a#framing-options {
  width: 210px;
  background-position: -175px 0px;
}
a#framing-options:hover {
  background-position: 0px -40px;
}
a#add-to-basket:active {
  background-position: 0px -80px;
}
a#framing-options:active {
  background-position: -175px -80px;
}
```

### Gradients and Contrasting

A gradient is a slight transformation of color or hue, and brightness.
*Note*: Set a class or ID selector with fallback images and colors when using gradients so browsers that cannot support the implementation can instead use the "fallback" settings.

An example gradient CSS class from *[Duckett, pg.419]*:

```css
#gradient {
  background-color: #66cccc;
  background-image:url("");
  background-image: -moz-linear-gradient(#336666,#66cccc);
  background-image: -webkit-gradient(linear, 0% 0%, 0% 100%, from(#66cccc), to(#336666));
  background-image: -webkit-linear-gradient(#336666,#66cccc);
  background-image: -o-linear-gradient(#336666,#66cccc);
  height: 150px;
  width: 300px;
}
```

The properties are set in this order for these browsers and situations:

1. Fallback color
2. Fallback image
3. FIrefox 3.6+
4. Safari 4+, Chrome 1+
5. Safari 5.1+, Chrome 10+
6. Opera 11.10+

When setting a background image behind text:

- Use a low-contrast image so text does not get lost.
- Place a "screen" of color and apply `opacity: [0-1]` to fade the contrast of the image.
- Select a strong font that can stand out against the background colors and lines.

## Chapter 19: Practical Information

SEO, Analytics, and Putting Your Site on the Web.

### Search Engine Optimization

SEO is the art of increasing chances your website will appear in search engine results.  
Search Engines look at:  

- The content on your site.  
- How many sites link to your site.  

On-page Techniques are things you can do to improve your site's search ranking:  

- Images should have text in their `alt=` attribute.  
- An appropriate page `<title>`.  
- Use of keywords in filenames (URL components).  
- Include keywords in `<h1-6>` elements.  
- Repeat keywords in the content / text.  
- Link text includes keywords.  
- The meta `description` tag should include a good site description that includes keywords.  

### Keywords and Phrases

Duckett suggests six tasks to perform when developing keywords and phrases for your site:

1. Brainstorm: How would potential visitors search for your site? What words would they use? What phrases might they use to find sites they are interested in?
2. Organize: Categorize keywords and phrases into areas associated with pages or sections of your website.  
3. Research: Add suggestions of additional keywords and suggestions provided by keyword tools online (see list below).  
4. Compare: Keyword research sites can show how popular certain keywords and phrases are, and will give you an idea as to how much competition might be out there.  
5. Refine: Create a sub-list of keywords and phrases that will be the ones you focus on the most. Ensure the keywords and phrases are related enough that when put together they still associate closely with the goals and services of your website (and not some other site).
6. Map: Select a few keywords and phrases from each of the page categories created in step 2, and plan to use these on the site pages. Avoid repeating the words and phrases on the pages, although some repition is appropriate.

### Analytics

Once your site is published you will want to learn how often your home page is loaded and other related information.
Google Analytics provides tracking code for your site that reports site visits back to Google, and access to a site with reports showing site visit data and trends.  

There are several analytic properties:

- Visits: Browsers that open a page on your site are counted.  
- Unique Visits: The number of visits by unique browsers over a specified timeframe.  
- Page views: Total page views by all visitors.  
- Pages Per Visit: An averaged number.  
- Avg Time On Site: Estimated average time each 'user' spent on the site.  

#### What Are Your Visitors Looking At?

- Pages: Which pages were viewed.  
- Landing Pages: The page visitors arrive to the site on.  
- Top Exit Pages: The last page viewed before the visitor left the site.  

Reference: [Google Analytics](https://www.google.com/analytics)  

#### Where Are Your Visitors Coming From?

- Referrers: Sites that have linked to your site.  
- Direct Search Terms: Visitors that arrived to the site NOT via a referring link i.e. via search engine, address typed into URL bar, links from within documents, etc.  

### Domain Names and Hosting

- Domain Name: The web address of your site.  
- Web Hosting: Internet-connected web servers that host your website pages.

Web Hosting Services have various offerings in terms of:

- Disk Space
- Bandwidth
- Backups: Do you have to backup your own site or will the hosting service do backups and restoration for you?
- Email Accounts: It can be handy to have this provided by a hosting service.
- Server-side Languages and Databases: Some hosts require using a specific language to access back-end services like databases. Know what the service offers (or requires).

Hosted Services do a majority of the web hosting and managing services for you, and could provide a web-development interface, but might not include email:

- WordPress  
- Tumblr  
- Posterous  
- Big Cartel (e-commerce)  
- Shopify (e-commerce)  

### FTP and Third Party Tools

FTP is a file transfer tool that allows you upload your website files to the webserver.  
There are GUI versions and terminal FTP programs that will do the trick.  

Common FTP Tools:

[FileZilla](https://www.filezilla-project.org/)  
[FireFTP](https://www.fireftp.mozdev.org)  
[CuteFTP](https://www.cuteftp.com)  
[SmartFTP](https://www.smartftp.com)  
[Transmit](https://www.panic.com/transmit)  

Common Third Party Tools:  

[WordPress](https://www.wordpress.com)  
[tumblr](https://www.tumblr.com)  
[posterous.com](https://www.posterous.com)  
[Shopify](https://www.shopify.com)  
[BigCartel](https://www.bigcartel.com)  
[Go Magento](https://go.magento.com)  
[Campaign Monitor](https://www.campaignmonitor.com)  
[MailChimp](https://www.mainchimp.com)  
[AddThis.com](https://www.addthis.com)
[AddToAny.com](https://www.addtoany.com)  

#### Keyword and Phrase Tools

[Google AdWords](https://www.adwords.google.co.uk/select/KeywordToolExternal). Use the 'exact match' option.  
[Word Tracker](https://www.wordtracker.com).  
[Keyword Discovery](https://www.keyworddiscovery.com).  

## MDN Aricle: Video and Audio APIs

## Chapter 9: Flash

Althouht an older, deprecated technology, Flash had a large impact on the internet, then and now.  
Authoring Flash content usually required software licensed from Adobe - some other unlicensed tools were available.  
HTML tags `<object>` and `<embed>` were used to add Flash to websites but later JavaScript was used instead.  
Flash `.fla` files were run within a browser using the Flash Player plugin.  
Initially, Flash was used for small animations, but it grew into a tool for creating fully functional websites.  
HTML5 introduced `<audio>` and `<video>` tags, which are used now.  

### Hosting vs Plugins vs HTML5

A web server can host video files in various formats for HTML5 websites to consume.  
Generally it is easier to host video on a service like Vimeo or YouTube.  
Requiring a Plug-in to use certain features of your website could reduce the number of potential site viewers.  
Using a hosting service also simplifies transcoding...it is done for you.  

## Additional Resources

Mozilla Developer Network: [Video and Audio APIs](https://developer.mozilla.org/en-US/docs/Learn/JavaScript/Client-side_web_APIs/Video_and_audio_APIs)  

## Back to Readme.md

[Back to index in readme](./README.md)