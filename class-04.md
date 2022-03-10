# Notes from Duckett HTML and JS Books

HTML Book Chapters 4 and 15  
JS Book Chapters 3  

## HTML Book Chapter 4 Notes - Links

Many reasons to link, usual suspects are:

- Bookmark an area within the same page to rapid jump-ahead or return.  
- Link to another page on the same website, like in a nev menu.  
- Link to another (external) website, like for a reference.  

### Structure

```html
<a href="">content</a>
```

- An anchor ('a') tag requires a closing tag.  
- Some content is expected between opening and closing tags.  
- 'href=' points to the URL aka the target of the link.  
  - Should be a full, absolute url for external sites.  
  - Should be relative url for internal "bookmark" links.  
- The content between opening and closing tags is rendered in the browser window.  
- Clearly displaying links to users (helps keep them around).  
- Write good link text (also helps keeps them around).  
- Anchor links 'shortcut' users around a site structure (e.g. nav links).  

URL construction will depend on whether the link is internal or external:

- External: Use the fully qualified URL to the *page* (usually the home page) of the external site.  
- Internal: Use *relative* URLs. There are some rules and tips to get these right:
  - Same-level link: enter the page filename.  
  - Parent to child: Add the hierarchy into the link like `child/page.html`.  
  - Parent to grandchild: Add the hierarchy like `child/grandchild/gcpage.html`.  
  - Child to parent: Reverse the hierarchy like: `../index.html`.  
  - Child to grandparent: Similar to P-to-GC but go UP the tree: `../../index.html`.  

### Email Links

```html
<a href='mailto:person@domain.org'>Email me!</a>
```

### Open Link In New Window

```html
<a href='https://www.google.com' target="_blank">Google Search</a>
```

### Linking to Specific Parts of a Page

Same Page:

- Use `id="bookmark_name` as the tag ID that surrounds the target content.  
- Point the anchor tag to the id like: `<a href="bookmark_name">here</a>`  
- The browser will scroll the window to put the tag in the viewport.  

Other Page:

- Use an ID in the target tag on the target page, like `<div id="SummaryLinks"><div>`  
- Point the anchor tag to the relative or fully-qualified URL and include the id like:

```html
<a href="http://my-site.com/#SummaryLinks">Summary Links on my site</a>
```



## HTML Book Chapter 15 Notes - Nnnn

## JS Book Chapter 3 Notes - Nnnn
