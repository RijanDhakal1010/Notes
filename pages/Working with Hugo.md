- [[Short codes inside of hugo]]
- # shared material
- A sample `config.yaml` file
  id:: 637fe4b1-3dfc-48ee-9ba3-8647e27409b6
  collapsed:: true
	- ```yaml
	  baseURL: http://example.org/ 
	  languageCode: en-us 
	  title: Acme Corporation 
	  theme: Eclectic 
	  author: 
	    facebook: "https://facebook.com/example" 
	    twitter: "https://twitter.com/example" 
	    email: "contact@example.org" 
	    name: "Acme Corporation" 
	    location: New York 
	    phone: (999) 999-9999 
	    hours: "**Mon-Fri:** 9:00AM - 6:00PM, ET" 
	  
	  menu:
	    main: 
	      - identifier: about 
	        name: About 
	        url: /about 
	        weight: 100 
	      - identifier: contact 
	        name: Contact 
	        url: /contact 
	        weight: 200 
	  params: 
	    color: "#4f46e5"
	    copyright: "Copyright &copy; 2022 Acme Corporation.
	      All Rights Reserved."
	    footer:
	    - title: About
	      content: >
	        Acme Corporation is the world's leading
	        manufacturer of digital shapes. From squares and
	        circles to triangles and hexagons, we have it
	        all. Browse through our collection of various
	        forms with different thicknesses and line styles.
	        We shape the world. You live in it.
	  
	  
	    - title: Recent Blog Posts
	      recents: blog
	      recentCount: 7
	    - title: Contact Us
	      contact: true
	  
	  ```
- The background image and the favicon do not sit inside the theme folder, rather they sit inside the resources folder and are accessed from there. This does not always need to be the case as some themes choose to keep their files in different places but the `resouces` folder is `Hugo`'s preferred location.
  id:: 638025f8-f2c5-4b4f-8767-b4d9f1e1a055
- Hugo  makes a different between the general template and the `index page` template. Most website have a landing or index page that is specialized to welcome users while the rest of the website can be simple content that can follow a different template (i.e. general template.)
  id:: 638026d1-fc8b-4b4d-a3a9-7c1e8a7e9777
- The global config can be a folder of metadata files instead of just one large metadata file.
  id:: 63862bfa-b06f-453c-ab3b-57e3dab5664f
  collapsed:: true
	-
	- Within the config folder, make a sub-directory `_default`. `_default` is a privileged folder inside of `hugo`, `hugo` uses it to set its defaults.
	- Moving the `config.toml` file to `_default` changes nothing about the website. But now we can have separate configs for separate parts of the website.
		- For example, now *author* can be configured with `config/_default/author.yaml`
		- The file names within `_default` are mapped to keys automatically.
		- The `_default` folder also support sub-directories `production` and `development` (the names `production` and `development` are hard-coded in hugo.)
			- Hugo's live server is hard-coded to default to the `_default/development` folder.
- # Quick commands
	- The command to build a live server
	  collapsed:: true
		- `hugo server -D`
		- `hugo serve` (Not sure what is different about this one yet)
		- `hugo server` (Not sure what is different about this one yet)
	- The easiest way to make a new website.
	  collapsed:: true
		- `hugo new site acme-corporation --format yaml`
	- Hugo supports `jekyll` imports
	  collapsed:: true
		- `hugo import jekyll <jekyll source folder> <target hugo folder>`
	- Use `-- port <number>` flag to specify the port number you want the server to run on.
	- How to disable live render:
	  collapsed:: true
		- `--disableFastRender`
		- `--disableLiveReload`
	- Changing the theme can clash with the browser's caching mechanism, to deal with this use the following one-liner
	  collapsed:: true
		- `hugo server --noHTTPCache --disableFastRender`
	- The command to use Wrangler CLI
	  collapsed:: true
		- `npx wrangler pages publish public`
	- To enable emojis
	  collapsed:: true
		- ```yaml
		  theme: <theme name>
		  enableEmoji: true
		  ```
	- Using Cloudflare Wrangler CLI to deploy
	  collapsed:: true
		- `wrangler pages publish .`
	- Using a specific `env` with the live server `hugo --environment <env name>`
- # Community resources
- The extensions that `Hugo` can apply to markdown are listed [on this website](https://gohugo.io/getting-started/configuration-markup/).
-
- # To-do
	- SEO support?
	  collapsed:: true
		- On page 54, section 1.9.1 they mention SEO support. I need to know what that means.
	- Hugo pipes
	- Shortcodes to extend markdown.
	- use a `_default/testing` folder to test themes.
	- Come back to the menus, around page 130s.
- # Setting the global config
- Enable line numbers in code blocks
  collapsed:: true
	- ```yaml
	  markup:
	  	highlight:
	      	lineNos: true
	  ```
- # Content management
- Try not to have one single massive config file. A single large config file can become a bottleneck.
- It is healthier to maintain two distinct and stable environments, one for production and one for development.
- {{embed ((63862bfa-b06f-453c-ab3b-57e3dab5664f))}}
- `summary` and `description` are two different types of metadata fields in `hugo`. `Description` is what is sent to the search engines.
- There are many ways to manage images.
	- They primarily go inside two folders:
	  collapsed:: true
		- Assets folder
		  collapsed:: true
			- These are optimized
		- Static folder
		  collapsed:: true
			- Not optimized and used as is.
- ## Page bundles
- These are collections of assets (pages, images, PDFs) that together make an individual bundle. These bundles are then used for content management. You can drop a bundle into a site and have the bundle not affect the rest of the site.
- There are three types of package bundles.
	- Leaf
		- Leaf bundles are a collection of elements that make the core contents of one page. The elements range from markup, metadata, images to CSS and JS.
		- The way to convert one page into a bundle is to make a folder with the pages name and have an `index.md` page for the markup and other assets such as metadata and images.
	- Branch
		- These form a section instead of just a page. To really fit the definition all assets that make up the section should be in the same folder.
	- Headless
- Page bundles are a compromise between speed and re-usability.
  collapsed:: true
	- Isolation makes things reusable thanks to isolation but increases bandwidth and storage cost but on the other hand sharing things makes it difficult to optimize things across the board.
- ## `Index.md` vs `_index.md`
- The `index.md` is the primary markup for a *leaf bundle* while the `_index.md` indexes the folder.
- ## How to use sections and menus to organize content
	- Individual sections can be given their own `_index.md` files that organize the landing page for the folder/section.
	- Every folder need an `_index.md` file, except `content`.
		- The `_index.md` for the content folder's root is optional because it is overridden by the `index.html` file in layouts.
	- ### Menus
	- There are two ways to add menus:
		- 1. Add menu items for the page in the config file. this helps localize and tightly monitor the menu.
		  2.Specify the page menus in the front matter. This makes the menus content driven and easier to manage.
- ## Taxonomies
- `Taxonomies` in `hugo` are a way to define relationships between web-pages without using the file system.
- The goal of `taxonomies` is to emulate the abilities of the relational database.
  collapsed:: true
	- To do this we provide information that connects one page to another in the `frontmatter`.
	- The user's job is to provide identifying information only and anything past that is taken care of by `Hugo`.
- `Taxonomies` use tags to build many-to-many relationships and expand upon the functionality of tags.
- # General Information
- Hugo tries to prioritize its command line interface.
  collapsed:: true
	- Hugo's CLI takes in commands in a hierarchical fashion. (Hugo in action, page 27)
	  collapsed:: true
		- A plain `hugo` call runs the default command to build the site.
		- `Hugo new` call creates new things.
		- `Hugo new site` creates a skeleton site.
		- `hugo new theme` generates a new theme
	- Commands and flags are different things, flags modify the commands' configurations. For example we can use `--format yaml` to change the format of the metadata from `TOML` to `YAML`
	- An example of how to nest commands and flags:
		- `hugo help` shows the whole document.
		- `hugo new --help` brings the help section for the `new` command specifically.
	-
- Hugo's file structure makes a difference.
  collapsed:: true
	- The various essential folders inside of a hugo webstie (Chapter 2.1.3)
	  collapsed:: true
		- |Folder name|Folder function|
		  |--|--|
		  |Achetypes|This contains the templates for the content files. This minimizes the copy and paste work for the website.|
		  |Content|This contains the files that will go into the database.  In hugo content is generally organized according to the file sturcture but it is possible to give each file a different postion on the file tree using `front matter`|
		  |Data|Data that belongs outside of the content folder can sit here and can be used by Hugo globally.|
		  |layouts|Here we configure the overriding of the theme.|
		  |Themes|This customizes the content folder's data for presentation.|
		  |Config |This is the global config across the website. Either this is a single yaml file or a folder of various yaml files.|
		  |Static|This is where the binary files sit.|
	- Other folders that can be placed inside of hugo
	  collapsed:: true
		- |Folder name|Function|
		  |--|--|
		  |Assets folder|This is where images, javascript and CSS files sit.|
		  |Public folder|This is where the output is dumped, this is where the html is generated and placed. This is what is pushed to the CDN.|
		  |Resouces folder|this is where hugo caches intermediate files for reuse across builds. For example, to save time and energy Hugo reuses images until they are changed and this is where they are kept.|
		  |go.mod and go.sum files|Used to sync project dependencies|
		  |vendor folder|Stores 3rd-party dependencies that we can include via hugo modules.|
		  |Node_modules, package.json, package-lock.json and package.hugo.json files|Folder that integrates hugo with the JS ecosystem|
		  |.github folder and netlify.toml files|Attaches hugo with CI/CD services|
		  |API folder|Folder that houses custom APIs|
- Hugo themes
  collapsed:: true
	- In `hugo` themes are the templates of logic that convert content from markup format into presentable web pages.
	- What makes up a theme?
	  collapsed:: true
		- Template code
		- JavaScript
		- CSS assets
		- Images for icons and backgrounds
- {{embed ((63862bfa-b06f-453c-ab3b-57e3dab5664f))}}
- The popular name for `Hugo`'s server mode is *live reload*
- Hugo has a standard way to define `menus`, which are rather common elements on all websites.
- The config file has some default hooks that are theme agnostic
  id:: 637fc291-ec1c-4bdd-802f-fea8db3985d4
- {{embed ((638025f8-f2c5-4b4f-8767-b4d9f1e1a055))}}
- {{embed ((638026d1-fc8b-4b4d-a3a9-7c1e8a7e9777))}}
- Markdown is specially easy to convert into formatted documents but plain old HTML and CSS are even more powerful.
- Hugo Shortcodes make it possible to makes themes without using inline HTML.
- To add metadata to each content page use `YAML` inside the metadata section. The metadata section is defined by a pair of three dashes with the metadata in-between.
  collapsed:: true
	- ```YAML
	  ---
	  #metadata goes here
	  ---
	  Markdown content here.
	  ```
- One of the greatest pros of using markdown based approach to a static blog is that textual data is easier to work with and has many robust tools available for use (such as git).
- `Hugo` has `shortcodes` which are equivalent to functions in programming. They are used to extend the functionality of markdown and summoned with `{{<>}}`
-
- # Working with Examples
- Use the following command to make a new website
  collapsed:: true
	- `hugo new site acme-corporation --format yaml`
- Adding content to a skeleton page that has a theme setup.
  collapsed:: true
	- Things to do:
		- supply settings
		- Supply metadata
		- add pages like privacy policy
		- terms of use
		- override the theme's landing page with a custom version
- Hugo's configuration file has two different levels
  id:: 637fe1dd-5b45-4bb5-9d7e-141cd5f56b67
  collapsed:: true
	- The top level configuration, common across themes
		- Such as the URL of the website, its name and language
		- Options for Hugo features such as `menus`
		- {{embed ((637fc291-ec1c-4bdd-802f-fea8db3985d4))}}
	- Theme specific `params` section, different between themes.
	  collapsed:: true
		- Such as theme-specific params (This is not much of an example but I will try to get back to this.)
- To override parts of a theme place a custom layout file in the layouts folder.
- # Themes in Hugo
- Making a hugo theme is a time consuming task and as such if possible simply use good themes that are already available.
- It is always possible to change the UI of the theme but to just get an website up and running it is better to use a pre-built theme.
- There are a few ways to setup themes in Hugo:
  collapsed:: true
	- Using Hugo modules
		- Hugo modules are the built-in package management system in Hugo. It is possible to make themes with dependencies using Hugo modules
	- Using Git sub-modules
		- Git sub-modules are git repos inside other git repos. It is possible to insert git repos that are pre-configured themes inside the `themes` folder to come up with a theme.
		- Git handles sub-modules not not `Hugo`.
		- Hugo prefers the use of `hugo` modules over git `submodules`
	- Good old copy and paste
		- It is possible to just download the files that pre-configure a theme and drop them in the theme folder. This is the simplest way to set up a theme
- How to load themes?
  collapsed:: true
	- Step 1: Go to `config.yaml`
	- Step 2: Write on a new line `theme: {Theme name}` in this case `theme:Eclectic`
	- start the live server to see if your theme worked.
- Metadata between themes is not portable.
- {{embed ((637fe1dd-5b45-4bb5-9d7e-141cd5f56b67))}}
- {{embed ((637fe4b1-3dfc-48ee-9ba3-8647e27409b6))}}
- The theme inside `hugo` can be written in `YAML` or `TOML`. Do not mix the two
- {{embed ((638025f8-f2c5-4b4f-8767-b4d9f1e1a055))}}
- {{embed ((638026d1-fc8b-4b4d-a3a9-7c1e8a7e9777))}}
- The `index.html` file holds a special place inside of `hugo`. It is specifically meant to help with configuration of the landing page.
- Hugo's template language is go templates. When not using other go templates, the configs need to be hard  coded.
- Custom HTML is static, whereas Hugo's templating language is dynamic. Whereas HTML is easy to get started with, unlike Go templates, HTML pages do not change automatically when overall things change.
- # [[Mar 17th, 2023]]
- The way to add module is `git submodule add {git theme} themes/{theme name}`. Do not clone the theme.
-