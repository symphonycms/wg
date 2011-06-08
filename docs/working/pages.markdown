##META
* Doc Version: 1
* Author: Giel Berkers
* Applies to: 2.x
* Based on: 2.x
* [Production URL]()

# A view on static pages #

First of all: let me say that _'all roads lead to Rome'_, meaning that this article is a single view of a single person
on how to combine static and dynamic content in Symphony. It summarizes the things I've learned about this from when I
started with Symphony until today.

## First timers, beware! ##

Most of you have experience with a bunch of different CMS-es. Most of these CMS-es have one thing in common: They allow
you to have a tree-like structure of your website. This allows you to create pages with a parent-child index, as well as
providing them with some basic content such as a title, a content-field and some other fields.

Most first-time-users of Symphony try to mimic this with their first created websites (I know I did!). For example: You
create a section called 'Pages' and add some fields like 'title', 'content' and 'parent' (dynamic selectbox with which
you can select other entries of the Pages-section to use as parent). Next, you create a single page (called 'content' for
example), with a parameter 'handle' or 'id' to get the right entry out of your pages-section. This might work, but it
has some serious drawbacks. For example:

- The URL's of your static pages will always end up like:
  - www.your-website.com/content/12/
  - www.your-website.com/content/my-handle/
- You would have to do some extra logic to create a navigation. Especialy when you have some static and some dynamic pages!
- If you want to hide a page from the navigation you would have to add an extra field to you pages-section.
- If you have multiple navigations (such as a top-navigation, a utilities-navigation and a footer-navigation) this also brings some extra fields to your pages-section.
- It's particularly hard to make exceptions; for example:
  - If your client wants a different picture on each page you would have to add a extra field to the pages-section.
  - If you want to change to order of the pages you would have to depend on an [extension](https://github.com/nickdunn/order_entries).
  - ... and you would ofcourse have to deal with all this logic in your XSL-template

## Forget pages, think content! ##

The first thing you need to understand is that Symphony works in no way like these other CMS-es. A 'page' in Symphony
is nothing more than a container for encapsulating content (datasources) and occasionally handling some logic (events).

If you structure your site, make sure to make the structure in 'Blueprints � Pages'. This is ofcourse pretty obvious
for dynamic pages. For example: you _would_ create a unique page for a news-section, and provide that with a parameter
and the right datasource to show the latest news items for example.

But: **All** pages should be added here, also static pages! So if you would have a site structure like:

- home
- about us
- our vision
- our products
- news
  - detail
- contact

You would have tot create 7 pages which result in 7 XSL-documents:

- home.xsl
- about-us.xsl
- our-vision.xsl
- our-products.xsl
- news.xsl
- news-detail.xsl
- contact.xsl

## Ok, but that would mean I would end up with a lot of XSL-documents which are mostly identical! ##

That's true. But that isn't a problem now is it? Even better: it's ideal! Think about all the features that come straight out of the box:

- You would have nice URL's.
- You can make use of Symphony's built-in page logic:
  - Use types to create smart navigation datasources.
  - Have correct parent-child relationships.
  - Set the order of the pages
- Exceptions are no longer hard to do, after all you have a seperate XSL-file for each page!

## And what about the content? ##

If you think 'content' and not 'pages' the most obvious thing to do is to create a datasource called 'Page content'.
This could for example have some fields like 'Title', 'Content', and one field provided by an extension: a [pages field](https://github.com/symphonycms/pagesfield).
This allows you to link your entry to a page. Now when you create your datasource, filter the pages-field by `{$current-page}`
to get the correct entry.

The XSL-code of the page now could look something like this:

    <xsl:template match="data">
        <h1>
            <xsl:value-of select="page-content/entry/title" />
        </h1>
        <xsl:copy-of select="page-content/entry/content/*" />
    </xsl:template>

Now if something ever changes about the way about how you display static content and you don't want to have to edit a
bunch of pages, you could simplify this by using a utility for static content. You can re-use this on the static content pages:

Utility:

    <xsl:template match="page-content" mode="static">
        <h1>
            <xsl:value-of select="entry/title" />
        </h1>
        <xsl:copy-of select="entry/content/*" />
    </xsl:template>

Page:

    <xsl:import href="../utilities/static-content.xsl" />
    <xsl:template match="data">
        <xsl:apply-templates select="page-content" mode="static" />
    </xsl:template>

You see that this makes it really easy to manage your static content. Now you no longer have to make exceptions for things like:

- The client want a banner on static page A, but not on static page B
- Every page should have a different image on top
- All pages have a picture, except page C, which has a Flash element.

Since each page has it's own XSL-document to deal with this logic.

## Hold the phone! All of this means my client will not be able to add new pages by himself! ##

That's also true. But is adding pages _really_ what your client wants? Sometimes the answer is correct but the question is
wrong. In my experience as a webdeveloper, I found that 99% of the clients I meet don't add new pages to their website on a
weekly base. What they **do** add however are:

- News items
- Projects
- Publications
- Downloads
- Links
- FAQ items
- Pictures
- etc...

All these items should have their own section and their own page so you would end up with URL's like:

- www.your-website.com/news/handle/
- www.your-website.com/projects/handle/
- www.your-website.com/publications/handle/
- www.your-website.com/downloads/category/
- etc...

Now if you look at 'projects' or 'publications' in this example. It _would_ look like each project and publication would
have it's own web-page. But in reality you only have one XSL-page which deals with the logic. A more clear approach would
be to add a detail-subpage so you keep your XSL clean and don't waste CPU-loops on loading datasources which will not be
used. In the above example, the URL's would then be:

- www.your-website.com/news/ _= news homepage, showing the latest 2 items for example._
- www.your-website.com/news/detail/handle/ _= the complete news item which is chosen by the visitor._
- www.your-website.com/projects/ _= projects homepage, showing all the projects with a picture and a short summary._
- www.your-website.com/projects/detail/handle/ _= the project-detail page, showing the complete project._

And if the client _really_ wants a new page (which is an average of 1-2 times a year) they give you a call and you add
it for them. In my experience with previous CMS-es where it w�s possible for the client to add their own pages they
would still call us when they wanted a new page, so nothing much changes there really...

So you see, it's more a way of thinking. As I said before, all roads lead to Rome and this is just one
of many ways on how you could approach pages in Symphony. I hope this article have given you some insight on how to do
this.

Now, let's build some static pages shall we?