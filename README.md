# eleventy-base-blog

A starter repository showing how to build a blog with the [Eleventy](https://github.com/11ty/eleventy) static site generator.

[![Build Status](https://travis-ci.org/11ty/eleventy-base-blog.svg?branch=master)](https://travis-ci.org/11ty/eleventy-base-blog)

## Demos

* [On Glitch](https://11ty-eleventy-base-blog.glitch.me/)

## Getting Started

### 1. Remix this project.

Then have a look at `.eleventy.js` to see if you want to configure any Eleventy options differently.

This project's config differs from 11ty/eleventy-base-blog git repository by the following config section, which enables 404 pages to work in your remix and when hosting your site using `eleventy --serve`. 
```
  eleventyConfig.setBrowserSyncConfig({
    callbacks: {
     ready: function(err, bs) {
       const content_404 = fs.readFileSync('_site/404.html');
       bs.addMiddleware("*", (req, res) => {
        // Provides the 404 content without redirect.
        res.write(content_404);
        res.end();
      });
     }
    }
  });
```

### 2. Installing dependencies happens automatically - thanks, Glitch!

### 3. Edit _data/metadata.json

### 4. Press 'Show' to view your new site

The site will reload automatically when something changes. In a normal Glitch project, you would be able to turn this off by unchecking 'Refresh App on Changes', but `eleventy --serve` is what we're using to serve files, and it always `--watch`es.  

### Implementation Notes

#### Glitch-specific
* On Glitch, image files should be stored in `assets`. After uploading a new image, you can use the CDN link the assets drawer provides in your pages.
  * This means you can remove `png` from `templateFormats`, because Glitch won't allow you to store a `png` outside of `assets`. 
* `watch.json` controls when Glitch refreshes the server, but since Eleventy is watching for us, we can safely tell it to ignore most of our files. Instead, Eleventy will rebuild and restart BrowserSync when you make changes. 
* Run BrowserSync in Ghost mode, so things like scroll position and form inputs are not synced across users. [See pull request in original repo](https://github.com/11ty/eleventy-base-blog/pull/34/files). We're using `eleventy --serve` to serve the static files, so this is necessary for a project on Glitch where it wouldn't be necessary if you were just running a build and then uploading the static file to a server that handled serving static files for you. 
  * Close readers might remember that Glitch _does_ serve static files for you in some projects! But, if you have a `package.json` file, Glitch assumes you're running a Node server yourself. (Typical usage would be `node server.js` in the `start` field of `package.json`.) We could create a server.js file that serves the static files, but for simplicity's sake, we're just using `eleventy --serve` as the `start` command. `eleventy --serve` isn't intended for production use, so you may hit other interesting snags that require modifications to the BrowserSync config.

#### Opinionated Choices in this Project

* Filter out all elements in the filtered tags list (notably including both tag `post` and `posts`) from the pagination display. [See pull request in original repo](https://github.com/11ty/eleventy-base-blog/pull/32). 


#### General Eleventy Help
* `about/index.md` shows how to add a content page.
* `posts/` has the blog posts but really they can live in any directory. They need only the `post` tag to be added to this collection.
* Add the `nav` tag to add a template to the top level site navigation. For example, this is in use on `index.njk` and `about/index.md`.
* Content can be any template format (blog posts needn’t be markdown, for example). Configure your supported templates in `.eleventy.js` -> `templateFormats`.
	* Because `css` and `png` are listed in `templateFormats` but are not supported template types, any files with these extensions will be copied without modification to the output (while keeping the same directory structure).
* The blog post feed template is in `feed/feed.njk`. This is also a good example of using a global data files in that it uses `_data/metadata.json`.
* This example uses three layouts:
  * `_includes/layouts/base.njk`: the top level HTML structure
  * `_includes/layouts/home.njk`: the home page template (wrapped into `base.njk`)
  * `_includes/layouts/post.njk`: the blog post template (wrapped into `base.njk`)
* `_includes/postlist.njk` is a Nunjucks include and is a reusable component used to display a list of all the posts. `index.njk` has an example of how to use it.