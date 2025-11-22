

# UI-KIT

<pre>
 ==========================
||                        ||
||   WELCOME TO UI-KIT!   ||
||                        ||
 ==========================
      vv_         _vv
      ||    ^ ^    ||
      ||   ('_')   ||
      \O===O---O===O/
           \ X /
           | X |
</pre>


UI-KIT is a small Javascript library that helps developers create single-page application (SPA) web sites.

Features:
* Organize areas of your site into components with HTML templates
* Load component content dynamically
* HTML syntax supporting conditionals and looping 
* No external dependencies
* No build step needed

In concept, UI-KIT is similar to web frameworks like Angular, React, or Vue, but with pared-down functionality and less to learn for people new to UI development.
UI-KIT makes use of a handful of custom html attributes (which have a `kit-` prefix) and a couple of simple javascript conventions.
All that is needed as a prerequisite is a basic understanding of HTML, CSS, and Javascript:

> Hello UI-KIT! HTML code example:
> ```html
> <!doctype html>
> <html>
> <head>
>   <meta charset="utf-8" />
>   <meta name="viewport" content="width=device-width, initial-scale=1">
>   <title>hello ui-kit</title>
>   <script type="module" src="/ui-kit.js"></script>
> </head>
> <body>
>   <div kit-element 
>        kit-model="{ title: 'HELLO UI-KIT', isEasy: true, howEasy: [ 'a', 'b', 'c' ] }">
>       <h1>%{#model.title}%</h1>
>       <div kit-if="#model.isEasy">
>         <p>This is as easy as:</p>
>         <ul kit-array="#model.howEasy" kit-array-item-alias="item">
>           <li>%{#item}%</li>
>         </ul>
>       </div kit-if>
>   </div>
> </body>
> </html>
> ```

> Browser view:
> <pre>
> ---------------------------
> |                         |
> | HELLO UI-KIT!           |
> | This is as easy as:     |
> | a                       |
> | b                       |
> | c                       |
> |                         |
> ---------------------------
> </pre>


The [Quick start guide](#quick-start "quick start guide") below offers a breakdown on the code concepts illustrated above as well as a step-by-step guide for building a simple single-page web application with UI-KIT. After exploring the quick start topics below you should be able to drop the ui-kit.js file into your web application and start using `kit-*` attributes to build applications.  
A full reference on the UI-KIT html attributes and Javascript framework can be found in the [Reference](#reference "reference") section at the end of this document.

# Table of contents <span id="toc" />

- [Quick start guide](#quick-start "quick start guide")
  - [The index page](#quick-start-1 "the index page")
  - [Component HTML templates](#quick-start-2 "component html templates")
  - [Component Javascript models](#quick-start-3 "component javascript models")
  - [Conditional rendering](#quick-start-4 "conditional rendering")
  - [Looping](#quick-start-5 "looping")
  - [Navigation](#quick-start-6 "navigation")
  - [State transitions](#quick-start-7 "state transitions")
- [Reference](#reference "reference")
  - [HTML reference](#reference-html "html reference")
    - [Tags](#reference-html-tags "html tags")
    - [Attributes](#reference-html-attributes "html attributes")
      - [kit-array](#reference-html-attributes-kit-array "kit-array attribute")
      - [kit-array-index](#reference-html-attributes-kit-array-index "kit-array-index attribute")
      - [kit-array-index-alias](#reference-html-attributes-kit-array-index-alias "kit-array-index-alias attribute")
      - [kit-array-item](#reference-html-attributes-kit-array-item "kit-array-item attribute")
      - [kit-array-item-alias](#reference-html-attributes-kit-array-item-alias "kit-array-item-alias attribute")
      - [kit-attr-*](#reference-html-attributes-kit-attr-* "kit-attr-* attribute")
      - [kit-component](#reference-html-attributes-kit-component "kit-component attribute")
      - [kit-element](#reference-html-attributes-kit-element "kit-element attribute")
      - [kit-element-key](#reference-html-attributes-kit-element-key "kit-element-key attribute")
      - [kit-if](#reference-html-attributes-kit-if "kit-if attribute")
      - [kit-model](#reference-html-attributes-kit-model "kit-model attribute")
      - [kit-obj-*](#reference-html-attributes-kit-obj-* "kit-obj-* attribute")
      - [kit-template-key](#reference-html-attributes-kit-template-key "kit-template-key attribute")
    - [Special characters](#reference-html-special-characters "special characters")
  - [CSS reference](#reference-css "css reference")
  - [Javascript reference](#reference-javascript "javascript reference")
    - [Working with models](#reference-javascript-working-with-models "working with models")
    - [Framework classes](#reference-javascript-framework "framework classes")
      - [UIKit](#reference-javascript-framework-ui-kit "UIKit")
      - [KitResourceManager](#reference-javascript-framework-kit-resource-manager "KitResourceManager")
      - [KitNavigator](#reference-javascript-framework-kit-navigator "KitNavigator")
      - [KitMessenger](#reference-javascript-framework-kit-messenger "KitMessenger")
      - [KitRenderer](#reference-javascript-framework-kit-renderer "KitRenderer")
&nbsp;

# Quick start guide <span id="quick-start" /><sup><span style="font-size:8pt;">[top](#toc "table of contents")</span></sup>
In this section we will build a simple single-page web application in a step-by-step fashion while introducing the basic concepts of building an app with UI-KIT.
At the end of this section you will have a functioning web-application with a heading component, a navigation panel component, and a couple of content components that are displayed conditionally depending on the current url.

&nbsp;  

---
## Step 1: The index page <span id="quick-start-1" /><sup><span style="font-size:8pt;">[top](#toc "table of contents") | [next](#quick-start-2 "component html templates")</span></sup>
---
With a single-page web application there is just one page: index.html.
Your application will dynamically modify the html content of this page based on things like user input and navigation actions.

:point_right: _Action: Create app folder_  
Let's start by creating a folder in your local file system to contain your web application.
You can name the folder anything you like.  I'll call mine "hello-ui-kit".  

:point_right: _Action: Add index.html file_  
Add an index.html file to this folder with the following initial content:

> index.html:
> ```html
> <!doctype html>
> <html>
> <head>
>   <meta charset="utf-8" />
>   <meta name="viewport" content="width=device-width, initial-scale=1">
>   <title>hello world</title>
>   <script type="module" src="/ui-kit.js"></script>
> </head>
> <body>
>   <h1>Hello UI-KIT!</h1>
> </body>
> </html>
> ```

The html above contains a reference to ui-kit.js:
>```html
>   <script type="module" src="/ui-kit.js"></script>
>```

:point_right: _Action: Add ui-kit.js file_  
To make this a valid script reference, download a copy of the ui-kit.js file and place it in the same folder.  

You should now have an application folder containing two files:

>```folder structure
> > hello-ui-kit
>   - index.html
>   - ui-kit.js
>```

Now that we have our initial content, let's serve it up to see what it looks like in a browser.  
There are many ways to serve web content locally.  How you choose to do it might depend on the OS you are using (Windows, Linux, Mac, ...) or which editor you prefer when writing code.
I have a Windows laptop and use either Visual Studio or Visual Studio Code to develop.
For me, an easy way to serve web content is with IISExpress.
IISExpress is free to use and is included with Visual Studio but can also be downloaded and installed separately (see [IISExpress install](https://www.microsoft.com/en-us/download/details.aspx?id=48264 "iis express install")).

:point_right: _Action: Open command prompt_  
If you are using IISExpress, once installed, open a command prompt by clicking the Windows Start button or the Window key, type in "cmd", and select the Command Prompt app.  

:point_right: _Action: Navigate to app folder in command prompt_  
In the command prompt window, navigate to your application folder with the cd command:

> Navigate to your app folder:
>```cmd
>C:\>cd <path-to-your-app-folder-here>
>```

:point_right: _Action: Run IISExpress_    
Then run the following command to start serving your application:

>Run IISExpress:
>```cmd
>"C:\Program Files (x86)\IIS Express\iisexpress" /path:%cd%\
>```

> <span style="color:#FFD700;font-weight:bold;">◊</span> _Note:_   
> _The IISExpress command might be slightly different depending on where IISExpress was installed on your machine._

After running the command, you should see output in the command window that looks something like this:
>```cmd
>Starting IIS Express ...
>Successfully registered URL "http://localhost:8080/" for site "Development Web Site" application "/"
>```

:point_right: _Action: Browse to app_  
However you are serving your application, open up a browser and navigate to your index page (_e.g. "http://localhost:8080/index.html"_).  

You should see a page with a heading that reads "Hello UI-KIT!".

&nbsp;  

---
## Step 2: Component HTML templates <span id="quick-start-2" /><sup><span style="font-size:8pt;">[top](#toc "table of contents") | [prev](#quick-start-1 "the index page") | [next](#quick-start-3 "component javascript models")</span></sup>
---
Now that we have our initial html content and can see it in the browser, let's start using UI-KIT to break our app into components.
We're going to add 3 components in this step: a heading component, a navigation panel component, and a content component.  
Each UI-KIT component (represented by an html element with a `kit-component` attribute) is comprised of an html fragment as a template and (optionally) a javascript model. We'll get to the javascript in later steps.  In this step, we're just focusing on the html templates.  
A component's html template can either be defined "inline" as the element's inner html, or it can be loaded from an external file path contained in the `kit-component` attribute.
We've seen an example of the inline approach in the "Hello UI-KIT! HTML" code example at the top of this document.
In this step we'll explore the second method: loading the template from an external file.

It isn't strictly necessary, but a nice way to organize an application is to create a folder for each component.

:point_right: _Action: Create component folders_  
Let's follow that convention and create some new subfolders for our components within our app directory like this:

>```folder structure
> > hello-ui-kit
>   > components
>     > heading
>       - heading.html
>     > navigation
>       - navigation.html
>     > content
>       - content.html
>   - index.html
>   - ui-kit.js
>```

heading.html, navigation.html, and content.html are the templates for our new heading, navigation, and content components.

:point_right: _Action: Add basic component template content_   
Put some basic content in each html template file to get started:

> heading.html:
> ```html
> <div id="heading">
>   <h2>Hello UI-KIT!</h2>
> </div>
> ```

> navigation.html:
> ```html
> <div id="navigation">
>   <h2>Navigation</h2>
> </div>
> ```

> content.html:
> ```html
> <div id="content">
>   <h2>Content area</h2>
> </div>
> ```

Now we just need to update our index.html file to refer to these new components.

:point_right: _Action: Update index.html_  
In the index.html file, replace the body tag's inner HTML with the following:

> index.html (body tag inner html):
> ```html
> <div kit-component="no-model:/components/heading/heading.html"></div>
> <div kit-component="no-model:/components/navigation/navigation.html"></div>
> <div kit-component="no-model:/components/content/content.html"></div>
> ```

 We've added one element with a `kit-component` attribute for each of our 3 components.  
`kit-component` is a custom html attribute used by UI-KIT to define a component.

> <span style="color:#FFD700;font-weight:bold;">◊</span> _Note:_  
> _Normally when we define a component with the `kit-component` attribute as above, UI-KIT expects to find a javascript module in a related location.  Since we're not covering javascript models yet in this Quick start step, we tell UI-KIT not to look for a model by prefixing the path with the `no-model:` prefix._

:point_right: _Action: Refresh browser_  
After making these updates, refresh your browser.
You should now see a page with 3 headings: 
- "Hello UI-KIT!"
- "Navigation"
- "Content area".

> <span style="color:#FFD700;font-weight:bold;">◊</span> _Note:_   
> _You may need to clear your browser's cache to see the changes.
> In Chrome, you can do this by first pressing F12 to open the developer tools, and then right-clicking the refresh button and selecting "Empty Cache and Hard Reload"._

This is a good start, but let's add some CSS styling so that each component's appearance better suits its function.   

:point_right: _Action: Add style tag to heading component template_  
In the heading component folder, add a heading.css file with the following content:

> heading.css:
> ```css
>   @scope (#heading) {
>     :scope {
>       position: fixed;
>       width: 100vw;
>       height: 60px;
>       top: 0;
>       left: 0;
>       display: flex;
>       border-bottom:1px solid black;
>       background-color: silver;
>     }
>     h2 {
>       padding: 10px;
>     }
>   }
> ```

Then update the heading.html file with a reference to this css file:

> heading.html:
> ```html
> <link rel="stylesheet" href="/components/heading/heading.css" />
> <div id="heading">
>   <h2>Hello UI-KIT!</h2>
> </div>
> ```

This fixes the position of the heading component to the top left of the page and gives it a background color.

> <span style="color:#FFD700;font-weight:bold;">◊</span> _Note:_  
> _The @scope pseudo-class sets the scope for the contained css rules.
> Setting the scope to the id of the top element in the component's template limits the css rules to the heading component.
> Using this pattern helps to isolate the css rules for each component and makes the css easier to manage._

We'll do something similar for the navigation component.  

:point_right: _Action: Add style tag to navigation component template_  
Update navigation.html with the following style tag:

> navigation.css:
> ```css
>   @scope (#navigation) {
>     :scope {
>       position: fixed;
>       left: 0;
>       width: 150px;
>       top: 60px;
>       bottom: 0;
>       border-right:1px solid black;
>       background-color: silver;
>     }
>     h2, div {
>       padding: 10px;
>     }
>   }
> ```

> navigation.html:
> ```html
> <link rel="stylesheet" href="/components/navigation/navigation.css" />
> <div id="navigation">
>   <h2>Navigation</h2>
> </div>
> ```

This fixes the position of the navigation component to the left of the page and gives it a background.

:point_right: _Action: Add style tag to content component template_  
Finally, we need to fix up the content area template so the header and navigation panels don't cover up the content.

> content.css:
> ```css
> @scope (#content) {
>     :scope {
>         margin-top:60px;
>         margin-left:150px;
> 	      padding: 10px;
>     }
> }
> ```

> content.html:
> ```html
> <link rel="stylesheet" href="/components/content/content.css" />
> <div id="content">
>   <h2>Content area</h2>
> </div>
> ```

:point_right: _Action: Save all changes and refresh browser_  
After adding the css files, updating the html files, saving all your changes, and refreshing your browser, you should see a page with clear content sections for heading, navigation, and content.

> Browser view:
> <pre>
> ----------------------------------
> |                                |
> | Welcome to UI-KIT!             |
> |             -------------------|
> |             |                  |
> | Navigation  | Content area     |
> |             |                  |
> |             |                  |
> ---------------------------------- 
> </pre>
&nbsp;  

---
## Step 3: Component Javascript models <span id="quick-start-3" /><sup><span style="font-size:8pt;">[top](#toc "table of contents") | [prev](#quick-start-2 "component html templates") | [next](#quick-start-4 "conditional rendering")</span></sup>
---
So far we've learned how to make simple components (and style them).
But components become much more flexible and useful when we can run javascript code in response to user interactions or when rendering the content of the component.
This is where "smart" components, components with associated javascript code, come in to the mix.

There are two ways to define a component with a javascript model:
1. Define the model using the `kit-model` attribute.
2. Define the model in a separate javascript file in the same folder where the component's html template is defined.

The first method is often used for simpler components where the parent component has access to all the facts needed to create the model.
The "Hello UI-KIT! HTML" code example markup at the top of this document uses this method:

> using the `data-kit-model` attribute:
> ```html
> <div kit-element 
>      kit-model="{ title: 'HELLO UI-KIT', isEasy: true, howEasy: [ 'a', 'b', 'c' ] }">
> ```

In this example, the `kit-model` attribute sets the component's javascript model to an object with 3 properties:

> javascript model:
> ```javascript
> { 
>   title: 'HELLO UI-KIT', 
>   isEasy: true,  
>   howEasy: [ 'a', 'b', 'c' ] 
> }
> ```

The javascript model is referenced in html using the `#model` alias:

> html template:
> ```html
> <h1>%{#model.title}%</h1>
> ```

Let's unpack that syntax a bit.  
The hashtag character (#) is used by UI-KIT to prefix javascript model references within html markup.  
Javascript models defined with the `kit-model` attribute always have the "model" alias.  
UI-KIT evaluates the text between `%{` and `}%` as javascript and writes the result into the html.

> <span style="color:#FFD700;font-weight:bold;">◊</span> _Notes:_  
> - _The #model alias is implicitly defined when using the `kit-model` attribute.  Other aliases may be defined with other kit-* attributes.  The alias may be referenced anywhere within that elements <u>inner html</u>._
> - _There are other `kit-` attributes that allow you to specify an alias other than "model", as we will see later._  
> - _If you ever need to render a literal `%{` or `}%` in your html, you can escape them by prefixing with a backslash: `\%{` and `\}%`._

Now let's turn to the second method for defining a component's javascript model: using a separate javascript file.  
For this, we'll learn by creating a model for our content component.  

:point_right: _Action: Remove `no-model:` prefix_  
First, in the index.html file, remove the `no-model:` prefix from the `kit-component` attribute on the element corresponding to the `content` component.

> Component tag for the content component (in index.html):
> ```html
> <div kit-component="/components/content/content.html"></div>
> ```

When UI-KIT finds a `kit-component` attribute (without the `no-model:` prefix), it expects to find a model in a Javascript file in the same folder and with the same name as the html template.  
If you specify a component html template at "/components/my-component/my-component.html", UI-KIT expects to find a javascript file at "/components/my-component/my-component.js".  
So, now that we've taken out our `no-model:` prefix, UI-KIT expects a javascript file at "/components/content/content.js".  

:point_right: _Action: Add content.js file_    
Let's add our content.js file.

> content.js:
> ```javascript
> export function createModel() {
>     return new ContentModel();
> }
> 
> class ContentModel {
>     async init(kitElement, kitObjects) {
>         this.kitElement = kitElement;
>         this.content = "Here is my content ...";
>     }
> 
>     sayHello() {
>         alert("Hiya!");
>     }
> }
> ```

Let's explore what's happening in content.js.  
UI-KIT will attempt to dynamically import the javascript file as a javascript module.  
It expects to find an exported `createModel()` function that returns the component's model.

> `createModel()` function:
> ```javascript
> export function createModel() {
>     return new ContentModel();
> }
> ```

It's up to the developer to define what the `createModel()` function returns.
In this case, we've defined a ContentModel class and the function returns an instance of that class.

It isn't required, but if the model returned from the `createModel()` function has an async `init()` method, as we do in this example, UI-KIT will call that method passing in a reference to the html element associated with the model as well as additional input objects (if any) that may have been defined through other `kit-` attributes (more on that later).  

> <span style="color:#FFD700;font-weight:bold;">◊</span> _Note:_  
> _UI-KIT will also look for an optional `onRendered()` method on the model.  If it exists, UI-KIT will call it after the component has been rendered in the document.  See  [Working with models](#reference-javascript-working-with-models "working with models") for more info._

:point_right: _Action: Update content.html_    
To make use of this javascript code, let's update content.html to reference the model:

> content.html:
> ```html
> <link rel="stylesheet" href="/components/content/content.css" />
> <div id="content">
>   <link rel="stylesheet" href="/components/content/content.css" />
>   <h2>Content area</h2>
>   <p>%{#model.content}%</p>
>   <div>
>     <button onclick="#model.sayHello()">say hello</button>
>   </div>
> </div>
> ```

Note the use of "#model" to refer to the model.  For components defined with an external html template, "model" is always implicitly defined as the alias for the model.  

:point_right: _Action: Save all changes and refresh browser_    
The content component should now display:
- "Here is my content ..."
- and a button with the text "say hello"

:point_right: _Action: Test updates_    
Clicking the "say hello" button demonstrates calling a function on the component's model and displays an alert with the text "Hiya!".

There's a little more to learn about UI-KIT javascript models, but we'll cover the rest in subsequent steps.

&nbsp;  

---
## Step 4: Conditional rendering <span id="quick-start-4" /><sup><span style="font-size:8pt;">[top](#toc "table of contents") | [prev](#quick-start-3 "component javascript models") | [next](#quick-start-5 "looping")</span></sup>
---
In this step, we'll learn how to conditionally render html content using the `kit-if` attribute.
For this step, we'll add a "currentSection" property to our content component model and use it to conditionally render only the "current content section" of our template.
In a subsequent step, we'll extend this to display the current content section based on user navigation actions.

:point_right: _Action: Update content.js_    
First, in our content component model class, let's get rid of the "content" property we added earlier and add a "currentSection" property.    
For now, we'll hard-code currentSection's value to "#section1" within the `init()` method.

> content.js:
> ```javascript
> async init(kitElement, kitObjects) {
>   this.kitElement = kitElement;
>   this.currentSection = "#section1";
> }
> ```

:point_right: _Action: Update content.html_    
Now, let's update the content.html to add different sections to the template but only render the "current" section.

> content.html:
> ```html
> <link rel="stylesheet" href="/components/content/content.css" />
> <div id="content">
>   <h2>Content area</h2>
>   <div kit-if="#model.currentSection === '#section1' || !#model.currentSection">
>     <div>Section 1 content</div>
>   </div>
>   <div kit-if="#model.currentSection === '#section2'">
>     <div>Section 2 content</div>
>   </div>
>   <div kit-if="#model.currentSection === '#section3'">
>     <div>Section 3 content</div>
>   </div>
>   <div>
>     <button onclick="#model.sayHello()">say hello</button>
>   </div>
> </div>
> ```

:point_right: _Action: Save all changes and refresh browser_    
Refreshing the browser should now display "Section 1 content" only and not any of the other sections.  

The html inside each element with a `kit-if` attribute is only rendered if the condition is true.

&nbsp;  

---
## Step 5: Looping <span id="quick-start-5" /><sup><span style="font-size:8pt;">[top](#toc "table of contents") | [prev](#quick-start-4 "conditional rendering") | [next](#quick-start-6 "navigation")</span></sup>
---
The `kit-array` attribute is used to loop over an array of items and render html content for each item in the array.  
In this step, we'll contrive to extend section 1 in the content component to use the `kit-array` attribute.  

:point_right: _Action: Update content.js_    
Our first action will be to define a method on our component model that returns an array representing the "items" in content section 1.

> content.js:
> ```javascript
> getSection1Items() {
>   return [
>     { itemId: 1, name: "Item 1" },
>     { itemId: 2, name: "Item 2" },
>     { itemId: 3, name: "Item 3" },
>     { itemId: 4, name: "Item 4" },
>     { itemId: 5, name: "Item 5" }
>   ];
> }
> ```

:point_right: _Action: Update content.html_    
Next, we'll update the element representing section 1 in content.html to use the `kit-array` attribute to loop over the items in section 1.

> content.html:
> ```html
>   <div kit-if="#model.currentSection === '#section1' || !#model.currentSection">
>       <div>Section 1 content</div>
>       <ul kit-array="#model.getSection1Items()" kit-array-item-alias="item">
>         <li id="%{#item.itemId}%">Name: %{#item.name}%</li>
>       </ul>
>   </div>
> ```

:point_right: _Action: Save all changes and refresh browser_    
Refreshing the browser should now display our list of 5 items in section 1.  

The `kit-array` attribute is used to specify the array of items to loop over.  
The `kit-array-item-alias` attribute (with the value "item" in this case) is used to specify the alias representing the current item in the array within the html template. 
The item reference name is prefixed with a hashtag just as with the `#model` alias we used earlier. 

It's also possible to provide an alias for the current item's index using the `kit-array-index-alias` attribute.
See [kit-array](#reference-html-attributes-kit-array "<kit-array>") for more info.

&nbsp;  

---
## Step 6: Navigation <span id="quick-start-6" /><sup><span style="font-size:8pt;">[top](#toc "table of contents") | [prev](#quick-start-5 "looping") | [next](#quick-start-7 "state transitions")</span></sup>
---

In the previous steps, we learned how to use the `kit-component`, `kit-if`, and `kit-array` attributes as building blocks for creating dynamic html content.
Now we're ready to use what we've learned to dynamically display content based on navigation events.  

:point_right: _Action: Update navigation.html_    
We'll start by adding navigation links to the navigation component.

> navigation.html:
> ```html
> <link rel="stylesheet" href="/components/navigation/navigation.css" />
> <div id="navigation">
>   <h2>Navigation</h2>
>   <div>
>     <a href="#section1" title="section 1">section 1</a>
>   </div>
>   <div>
>     <a href="#section2" title="section 2">section 2</a>
>   </div>
>   <div>
>     <a href="#section3" title="section 3">section 3</a>
>   </div>
> </div>
> ```

Next, we'll update the content component to respond to navigation events.  
We'll need to make 3 changes to the content component's javascript file. 

:point_right: _Action: Add import statement to content.js_    
First, we're going to refer to a constant defined in the UI-KIT library so we'll need to add an import statement at the top of the file.

> import statement:
> ```javascript
> import { KitNavigator } from "../../ui-kit.js";
> ```  

:point_right: _Action: Add `onNavigation()` method to content.js_    
Second, we need to add an `onNavigation()` method that will respond to navigation events and re-render the component:

> onNavigation() function:
> ```javascript
> async onNavigation() {      
>   this.currentSection = UIKit.navigator.getHash(UIKit.document.location.href);
>   this.loaded = false;
>   await UIKit.renderer.renderElement(this.kitElement);
> }
> ```

:point_right: _Action: Update `init()` method in content.js_    
Finally, in the `init()` method, instead of hard-coding the current section value, we'll retrieve it from the current url.  We'll also call `UIKit.messenger.subscribe()` to start listening for navigation events.  

> `init()` method:
> ```javascript
>     async init(kitElement, kitObjects) {
>       this.kitElement = kitElement;
>       this.currentSection = UIKit.navigator.getHash(UIKit.document.location.href);
>       const elementKey = UIKit.renderer.getKitElementKey(this.kitElement);
>       const subscriber = {
>         elementKey: elementKey,
>         id: `nav-${elementKey}`,
>         object: this,
>         callback: this.onNavigation.name
>       };
>       UIKit.messenger.subscribe(KitNavigator.NavTopic, subscriber);
>    }
> ```

Our `UIKit.messenger.subscribe()` call tells UI-KIT to call the `onNavigation()` method whenever a navigation event occurs.

:point_right: _Action: Save all changes and refresh browser_    
Refreshing the browser, you can now click on the navigation links (or the browser's back and forward buttons) and observe the content updating dynamically in response.  

&nbsp;  

---
## Step 7: State transitions <span id="quick-start-7" /><sup><span style="font-size:8pt;">[top](#toc "table of contents") | [prev](#quick-start-6 "navigation")</span></sup>
---
It's a common practice to organize large applications into easier to manage components.  
It's also a common pattern to separate the component's state (or model or data) from its presentation (or view). We see that here in how we separate the javascript model (the state or data) from its html template (the presentation or view). When a component's model changes, the view should be updated as well to reflect the new state.  
This is called a state transition.  

One of the remarkable capabilities of more full-featured UI frameworks like Angular, React, or Vue is that the framework automatically updates the view to reflect state changes.  
However, that synchronization magic does have a cost in terms of complexity.  The frameworks themselves are much more complex and there is a lot more that the developer needs to understand in terms of how and when synchronization might occur.  

UI-KIT takes a different (simpler) approach.  The state of component models is not tracked internally by the framework and it is left to the developer to explicitly synchronize the view after state changes occur. We saw this explicit synchronization in the previous step when we called `UIKit.renderer.renderElement()` to re-render the content component after a navigation event. In this step, we'll explore state transitions a bit more with another example:  showing a loading indicator.

It's often the case with web applications that it takes some time to get the data needed to fully present a component.  Often we need to load a file, query a database, or fetch data from an API over the internet, all of which takes some time.  To show our users that the data is on its way, it's common to initially show a loading indicator and then later, when the model changes state from not having data to having data, we update the view to show the requested data. In this step, we'll update the content component to initially display a loading indicator when section 1 data is requested and then transition to showing data.

:point_right: _Action: Update content.css_    
First, let's borrow an animated css loading indicator from the web and add it to our styles for the content component.

> content.css:
> ```css
> @scope (#content) {
>   :scope {
>       margin-top:60px;
>       margin-left:150px;
> 	    padding: 10px;
>   }
> 
>   /* From https://css-loaders.com/ */
>   /* HTML: <div class="loader"></div> */
>   .loader {
>     width: 15px;
>     aspect-ratio: 1;
>     position: relative;
>   }
>   .loader::before,
>   .loader::after {
>     content: "";
>     position: absolute;
>     inset: 0;
>     border-radius: 50%;
>     background: #000;
>   }
>   .loader::before {
>     box-shadow: -25px 0;
>     animation: l8-1 1s infinite linear;
>   }
>   .loader::after {
>     transform: rotate(0deg) translateX(25px);
>     animation: l8-2 1s infinite linear;
>   }
>   @keyframes l8-1 {
>     100%{transform: translateX(25px)}
>   }
>   @keyframes l8-2 {
>     100%{transform: rotate(-180deg) translateX(25px)}
>   }
> }

I borrowed the css for this loader from [css-loaders.com](https://css-loaders.com/ "css-loaders.com"). It looks like it's designed to be used with a div element with class "loader" so we'll need to update our html template.

:point_right: _Action: Update content.html_    
Update the section 1 part of our content template to make use of our new css loading indicator.

> section 1 of content.html:
> ```html
> ...
>     <div>Section 1 content</div>
> 
>     <!-- loading indicator -->
>     <div kit-if="#model.loading">
>       <div style="margin:20px;" class="loader"></div>
>     </div>
> 
>     <!-- content when loaded -->
>     <ul kit-if="!#model.loading" kit-array="#model.section1Items ?? []" kit-array-item-alias="item">
>       <li id="%{#item.itemId}%">Name: %{#item.name}%</li>
>     </ul>
> 
>   </div>
> ...
> ```

We've added our div with `class="loader"` for our loading indicator and wrapped in in a div element with a `kit-if` attribute so that it is only displayed when `loading` is true.
Also, we've added a `kit-if` attribute so that it is only displayed when `loading` is false, meaning it's done loading.
And note that we've changed from using the `getSection1Items()` method to using a `section1Items` property on the model to get our items array so we'll have to update our Javascript model correspondingly.

:point_right: _Action: Update content.js - add `loadContent()` method_    
There are multiple ways to accomplish this loading behavior.  
For this example, we will remove the existing `getSection1Items()` method, add a `loadContent()` method, and add static properties to hold the data.

> content.js - loadContent() method:
> ```javascript
> async loadContent() {
> 
>   this.loading = true;
>   let reRender = false;
>   if (this.currentSection === "#section1") {
> 
>     // simulate a delay getting data (3 seconds)
>     await new Promise(r => setTimeout(r, 3000));
> 
>     // set data
>     ContentModel.data = [
>       { itemId: 1, name: "Item 1" },
>       { itemId: 2, name: "Item 2" },
>       { itemId: 3, name: "Item 3" },
>       { itemId: 4, name: "Item 4" },
>       { itemId: 5, name: "Item 5" }
>     ];
>     this.section1Items = ContentModel.data;
>     reRender = true;
>   }    
>   this.loading = false;
>   ContentModel.loaded = true;
> 
>   // re-render
>   if (reRender) {
>     await UIKit.renderer.renderElement(this.kitElement);
>   }
> }
> ```

:point_right: _Action: Update content.js - update `init()` method_  
And now, add the static data properties and update `init()` to call `loadContent()`.

> content.js - init() method:
> ```javascript
> 
>     static loaded = false;
>     static data = [];
> 
>     async init(kitElement, kitObjects) {
>       this.kitElement = kitElement;
>       this.currentSection = UIKit.navigator.getHash(UIKit.document.location.href);
>       const elementKey = UIKit.renderer.getKitElementKey(this.kitElement);
>       const subscriber = {
>         elementKey: elementKey,
>         id: `nav-${elementKey}`,
>         object: this,
>         callback: this.onNavigation.name
>       };
>       UIKit.messenger.subscribe(KitNavigator.NavTopic, subscriber);
>       this.loading = false;
>       this.section1Items = ContentModel.data;
>       if (!ContentModel.loaded) {
>         this.loadContent();
>       }
>    }
> ```

In the code above, we render the component in its initial (loading) state, get the data (with an artificial delay), and then render the component again after retrieving the data.  

:point_right: _Action: Save all changes and refresh browser_    
After refreshing your browser you should now see the loading indicator for 3 seconds before seeing the list of items in section 1.  

This completes the quick start guide.  
I hope you like using UI-KIT.  For additional information see the [Reference](#reference "reference") section below.  
\- Jim Hackbarth  
\- (jim.hackbarth1@gmail.com)

&nbsp;

# Reference <span id="reference" /><sup><span style="font-size:8pt;">[top](#toc "table of contents")</span></sup>
The UI-KIT reference is organized into 3 sections:
- [HTML reference](#reference-html "html reference")
- [CSS reference](#reference-css "css reference")
- [Javascript reference](#reference-javascript "javascript reference")

&nbsp;

## HTML reference <span id="reference-html" /><sup><span style="font-size:8pt;">[top](#toc "table of contents") | [..^](#reference "reference")</span></sup>
The HTML section of the reference is divided into 3 sub-sections:
- [Tags](#reference-html-tags "html tags")
- [Attributes](#reference-html-attributes "html attributes")
- [Special characters](#reference-html-special-characters "special characters")

&nbsp;

### Tags <span id="reference-html-tags" /><sup><span style="font-size:8pt;">[top](#toc "table of contents") | [..^](#reference-html "html reference")</span></sup>
There are no special tags specific to UI-KIT.  

In some situations, especially in conjunction with `kit-if` attribute, you may want an element that doesn't itself change the visual layout of the html, but contains child elements that do.  
A `<div>` tag, with proper css styling, is the preferred convention, but you may also define a non-standard tag for this purpose.  

> Example :
>
> ```html
>  <my-tag kit-if="#myModel.hasCondition">
>    <h2>...</h2>
>    <p>...</p>
>    ...
>  </my-tag>
> ```
&nbsp;  

### Attributes <span id="reference-html-attributes" /><sup><span style="font-size:8pt;">[top](#toc "table of contents") | [..^](#reference-html "html reference")</span></sup>
This section of the reference covers special html "kit-*" attributes defined by UI-KIT:

- [kit-array](#reference-html-attributes-kit-array "kit-array attribute")
- [kit-array-index](#reference-html-attributes-kit-array-index "kit-array-index attribute")
- [kit-array-index-alias](#reference-html-attributes-kit-array-index-alias "kit-array-index-alias attribute")
- [kit-array-item](#reference-html-attributes-kit-array-item "kit-array-item attribute")
- [kit-array-item-alias](#reference-html-attributes-kit-array-item-alias "kit-array-item-alias attribute")
- [kit-attr-*](#reference-html-attributes-kit-attr-* "kit-attr-* attribute")
- [kit-component](#reference-html-attributes-kit-component "kit-component attribute")
- [kit-element](#reference-html-attributes-kit-element "kit-element attribute")
- [kit-element-key](#reference-html-attributes-kit-element-key "kit-element-key attribute")
- [kit-if](#reference-html-attributes-kit-if "kit-if attribute")
- [kit-model](#reference-html-attributes-kit-model "kit-model attribute")
- [kit-obj-*](#reference-html-attributes-kit-obj-* "kit-obj-* attribute")
- [kit-template-key](#reference-html-attributes-kit-template-key "kit-template-key attribute")
&nbsp;

---
#### kit-array <span id="reference-html-attributes-kit-array" /><sup><span style="font-size:8pt;">[top](#toc "table of contents") | [..^](#reference-html-attributes "attributes")</span></sup>
`kit-array` is used to specify the array of items to loop over.  
UI-KIT evaluates the value of this attribute as Javascript.

> kit-array example:
> ```html
> <ul kit-array="['a', 'b', 'c']" kit-array-item-alias="item">
>   <li>%{#item}%</li>
> </ul>
> 
> <!-- renders: 
> <ul kit-array>
>   <li>a</li>
>   <li>b</li>
>   <li>c</li>
> </ul>
> -->
> ```
&nbsp;

---
#### kit-array-index <span id="reference-html-attributes-kit-array-index" /><sup><span style="font-size:8pt;">[top](#toc "table of contents") | [..^](#reference-html-attributes "attributes")</span></sup>
`kit-array-index` contains the index value for an item in an array.  
This attribute is used by UI-KIT during rendering and is not typically referenced by developers.
&nbsp;

---
#### kit-array-index-alias <span id="reference-html-attributes-kit-array-index-alias" /><sup><span style="font-size:8pt;">[top](#toc "table of contents") | [..^](#reference-html-attributes "attributes")</span></sup>
`kit-array-index-alias` contains a label that, when prefixed with a hashtag, can be used to reference the index of an item in an array.
&nbsp;

---
#### kit-array-item <span id="reference-html-attributes-kit-array-item" /><sup><span style="font-size:8pt;">[top](#toc "table of contents") | [..^](#reference-html-attributes "attributes")</span></sup>
`kit-array-item` contains the value for an item in an array.  
This attribute is used by UI-KIT during rendering and is not typically referenced by developers.
&nbsp;

---
#### kit-array-item-alias <span id="reference-html-attributes-kit-array-item-alias" /><sup><span style="font-size:8pt;">[top](#toc "table of contents") | [..^](#reference-html-attributes "attributes")</span></sup>
`kit-array-item-alias` contains a label that, when prefixed with a hashtag, can be used to reference an item in an array.
&nbsp;

---
#### kit-attr-* <span id="reference-html-attributes-kit-attr-*" /><sup><span style="font-size:8pt;">[top](#toc "table of contents") | [..^](#reference-html-attributes "attributes")</span></sup>
Attributes with names starting with `kit-attr-` are used to dynamically add an attribute to an element.  
The attribute value should consist of a name-value pair delimited with a colon (:).  
If the portion of the attribute after the colon resolves to a value that is not null and not undefined, the attribute named in the portion before before the colon will be added with the resolved value.  
If the value resolves to an empty string, the attribute will be added without a value.  
This attribute is useful for adding attributes at runtime that do not have a value like `checked` or `disabled`.  
UI-KIT will only process kit-attr-* attributes on elements that also have at least one of the following attributes:
- `kit-array`
- `kit-component`
- `kit-element`
- `kit-if`

> kit-attr-* example:
> ```html
> <div kit-element kit-attr-prop1="prop1:'abc'" kit-attr-disabled="disabled:''"></div>
> 
> <!-- renders: 
> <div prop1="abc" disabled></div>
> -->
> ```

> <span style="color:#FFD700;font-weight:bold;">◊</span> _Note:_   
> _Using `%{` and `}%` can be a good way to set the value of an attribute but should not be used to add attributes as the browser may adjust the text of the added attribute in unexpected ways (changing case for example).  
`kit-attr-*` attributes are the preferred method for adding attributes with UI-KIT.
&nbsp;

---
#### kit-component <span id="reference-html-attributes-kit-component" /><sup><span style="font-size:8pt;">[top](#toc "table of contents") | [..^](#reference-html-attributes "attributes")</span></sup>  
`kit-component` is used to specify the path to an external html template.  
By default, UI-KIT expects to find a corresponding javascript file containing the model for the component.  
Alternatively, a javascript model can be passed in using the `kit-model` attribute.  
To explicitly indicate that there is not a javascript model, add the prefix "no-model:" to the attribute value.  

> kit-component examples:
> ```html
> <!-- component with javascript model contained in module at "/components/comp1/comp1.js" -->
> <div kit-component="/components/comp1/comp1.html"></div>
> 
> <!-- component with javascript model passed in using kit-model attribute -->
> <div kit-component="/components/comp1/comp1.html" kit-model="#model.getComp1Model()"></div>
> 
> <!-- component with no javascript model -->
> <div kit-component="no-model:/components/comp1/comp1.html"></div>
> 
> ```

---
#### kit-element <span id="reference-html-attributes-kit-element" /><sup><span style="font-size:8pt;">[top](#toc "table of contents") | [..^](#reference-html-attributes "attributes")</span></sup>
The `kit-element` attribute (as well as `kit-array`, `kit-component`, and `kit-if` attributes) marks an element for dynamic rendering.  
The html markup for these elements will be modified during rendering based on the resolved values of kit-obj-* and kit-attr-* attributes.  
`kit-element` is typically used in cases where dynamic resolution of a `kit-attr-*` or `kit-obj-*` attribute is needed and the element isn't decorated with `kit-array`, `kit-component`, or `kit-if`.  
&nbsp;

---
#### kit-element-key <span id="reference-html-attributes-kit-element-key" /><sup><span style="font-size:8pt;">[top](#toc "table of contents") | [..^](#reference-html-attributes "attributes")</span></sup>
`kit-element-key` is an attribute that is automatically added by UI-KIT during rendering.  
It is added to elements that have a `kit-array`, `kit-component`, `kit-element`, or `kit-if` attribute.  
&nbsp;

 ---
#### kit-if <span id="reference-html-attributes-kit-if" /><sup><span style="font-size:8pt;">[top](#toc "table of contents") | [..^](#reference-html-attributes "attributes")</span></sup>
`kit-if` is used to specify the boolean condition controlling when an element's inner html (or component template) should be rendered.  
UI-KIT evaluates the value of this attribute as Javascript.
&nbsp;

---
#### kit-model <span id="reference-html-attributes-kit-model" /><sup><span style="font-size:8pt;">[top](#toc "table of contents") | [..^](#reference-html-attributes "attributes")</span></sup>
`kit-model` is used in conjunction with the `kit-component` attribute to specify the model for a component.  
UI-KIT evaluates the value of this attribute as Javascript.
&nbsp;

---
#### kit-obj-* <span id="reference-html-attributes-kit-obj-*" /><sup><span style="font-size:8pt;">[top](#toc "table of contents") | [..^](#reference-html-attributes "attributes")</span></sup>
Attributes with names starting with `kit-obj-` are used to make additional javascript objects available to a javascript model and when rendering an element.  
The attribute value should consist of a name-value pair delimited with a colon (:).  
The portion of the attribute value before the colon is the alias for the object and the portion of the attribute value after the colon resolves to a javascript object.  
UI-KIT will only process kit-attr-* attributes on elements that also have at least one of the following attributes:
- `kit-array`
- `kit-component`
- `kit-element`
- `kit-if`

> kit-obj-* example:
> ```html
> <div kit-element kit-attr-my-data="myData:'abc'">
>   <p>%{#myData}%</p>
> </div>
> 
> <!-- renders: 
> <div kit-element>
>   <p>abc</p>
> </div>
> -->
> ```
&nbsp;

---
#### kit-template-key <span id="reference-html-attributes-kit-template-key" /><sup><span style="font-size:8pt;">[top](#toc "table of contents") | [..^](#reference-html-attributes "attributes")</span></sup>
`kit-template-key` is an attribute that is automatically added by UI-KIT during rendering.  
It is used to identify the html template used to generate the inner html for dynamically rendered elements.  
It is added to elements that have a `kit-array`, `kit-component`, `kit-element`, or `kit-if` attribute.  
&nbsp;

### Special characters <span id="reference-html-special-characters" /><sup><span style="font-size:8pt;">[top](#toc "table of contents") | [..^](#reference-html "html reference")</span></sup>
There are a few special character sequences that can be used to tell UI-KIT how to render content.  
Content between `%{` and `}%` is evaluated as javascript and the result is written into the html.

> special character example:
> ```html
> %{1 + 1}%
> <!-- renders: 2 -->
> ```

Special characters `%{` and `}%` can be escaped by prefixing with a backslash: `\%{` and `\}%`.

> escaped special character example:
> ```html
> \%{1 + 1\}%
> <!-- renders: %{1 + 1}% -->
> ```

UI-KIT also  makes special use of the hashtag character to prefix model references within html templates.

> model reference example:
> ```html
> <div kit-element kit-obj-my-model="myModel:{ prop1: 'abc', prop2: 'def' }">
>   <div>prop1 = %{#myModel.prop1}%</div>
>   <div>
>     <button onclick="alert(`prop2 = ${#myModel.prop2}`)">show prop2</button>
>   </div>
> </div>
> ```

If needed, model references may be escaped by prefixing with a backslash.

> escaped model reference example:
> ```html
> <div kit-element data-obj-my-model="myModel:{ prop1: 'abc', prop2: 'def' }">
>   <div>prop1 = %{#myModel.prop1}%</div>
>   <div>my reference to prop 1 is \#myModel.prop1</div>
> </div>
> 
> <!-- renders: 
> <div kit-element>
>   <div>prop1 = abc</div>
>   <div>my reference to prop 1 is #myModel.prop1</div>
> </div>
> -->
> ```

&nbsp;

## CSS reference <span id="reference-css" /><sup><span style="font-size:8pt;">[top](#toc "table of contents") | [..^](#reference-html "html reference")</span></sup>
There are no special css class names or rules specific to UI-KIT.  

But there is a convention that can be followed to scope css styles to a specific component so that everything having to do with a component can be found in one location.

To scope css styles to a component, we can follow a convention of specifying a class on the top-most element in the template and referencing that class using the `@scope` attribute in the css file.

> Example component html file:
>
> ```html
> <style>
> @scope (.my-component) {
>  :scope {
>    /* styles for the top-most element in the component (.my-component) */
>  }
>  .my-class {
>   /* styles for elements with class "my-class" (and that are also a descendant of .my-component) */
>  }
> }
> </style>
> <div class="my-component">
>   <link rel="stylesheet" href="/components/my-component/my-component.css" />
>   <h2>My Component</h2>
>   <div class="my-class">My class content</div>
> </div>
> ```

> <span style="color:#FFD700;font-weight:bold;">◊</span> _Tip:_   
> _For components with an "inline" inner html template, UI-KIT first removes the inner html template from the document before processing the template for display. When the component is included directly in the markup for the index.html file (rather than the markup in a component template html file), 
> the component's template may be briefly displayed in the browser before being removed.
> To prevent this brief display, add the following rule to a global stylesheet._
> 
> Prevent template initial display of inline html templates:
> ```css
> [kit-array]:not([kit-element-key]),
> [kit-component]:not([kit-element-key]),
> [kit-element]:not([kit-element-key]),
> [kit-if]:not([kit-element-key]),{
>     display: none;
> }
> ```

This rule hides elements with `kit-array`, `kit-component`, `kit-element`, or `<kit-if>` attributes that do not yet have a `kit-element-key` attribute.  
After UI-KIT has removed any inner html template from the document (and added a `kit-element-key` attribute), the component is displayed as expected.  
&nbsp;

## Javascript reference <span id="reference-javascript" /><sup><span style="font-size:8pt;">[top](#toc "table of contents") | [..^](#reference "reference")</span></sup>
The Javascript secion of the reference is divided into 2 sub-sections:
- [Working with models](#reference-javascript-working-with-models "working with models")
- [Framework classes](#reference-javascript-framework "framework classes")

&nbsp;

### Working with models <span id="reference-javascript-working-with-models" /><sup><span style="font-size:8pt;">[top](#toc "table of contents") | [..^](#reference-javascript "javascript reference")</span></sup>
There are two ways to provide a UI-KIT component with a model:
1. Pass a model to the component from its parent context using the `kit-model` attribute.
2. Implement a `createModel()` method in a Javascript module located in a file in the same folder and with the same name as the component's html template.

The first method works well in use scenarios where the parent context has all the information needed to create a model.  
The _Hello World_ example from the top of this document is a good example of the first method.

> Example of passing a model to a component using `kit-model`:
> ```html
> <div kit-component="...path.html" kit-model="{ title: 'Hello UI-KIT' }">
>   <h1>%{#model.title}%</h1>
> </div>
> ```

The example above uses the `kit-model` attribute to pass a model to the component which is implicitly aliased as "model":

The second method is useful when the model is more complex or when the model needs to be initialized with data from an external source.  

> Example:
> ```html
> <div kit-component="/components/my-component/my-component.html">
> </kit-component>
> ```

With the markup above, UI-KIT expects to find an HTML template file at the specified path *and* a Javascript file containing the component's model in the same folder and with the same name as the html template:

> Component folder structure:
> ```folder structure
> > my-component
>   - my-component.html
>   - my-component.js
> ```

UI-KIT will attempt to dynamically import the javascript file as a Javascript module. Within this module there are a few expectations specific to UI-KIT:  
- (Required) UI-KIT expects to find an exported `createModel()` function that returns the model for the component.
- (Optional) If the object returned by `createModel()` has an async method named `init()`, UI-KIT will call that method after the model is created.  
- (Optional) If the object returned by `createModel()` has an async method named `onRendered()`, UI-KIT will call that method after the component's template has been processed and the resulting markup added to the document.  

> Example of a component's javascript file:
> ```javascript
> import { KitRenderer } from "../../ui-kit.js";
> 
> // required
> export function createModel() {
>     return new MyComponentModel();
> }
> 
> class MyComponentModel {
> 
>     // optional
>     async init(kitElement, kitObjects) {
>         this.kitElement = kitElement;
>     }
> 
>     // optional
>     async onRendered() {
>         alert(this.kitElement);
>     }
> }
> ```

UI-KIT passes a reference to the model's html element as input to the `init()` method.  
UI-KIT will also pass any input provided via the `kit-obj-*` attributes.

It is common for a component to re-render itself after a state change.  The `kitElement` parameter can be passed to `UIKit.renderer.renderElement()` to re-render a component.  
Other useful UI-KIT framework methods include:
- `UIKit.renderer.render()` to re-render the entire document
- `UIKit.navigator.navigate()` to initiate navigation from Javascript code
- `UIKit.messenger.publish()` and `UIKit.messenger.subscribe()` to send and receive messages between components

See [Framework classes](#reference-javascript-framework "framework classes") below for additional information.

&nbsp;

### Framework classes <span id="reference-javascript-framework" /><sup><span style="font-size:8pt;">[top](#toc "table of contents") | [..^](#reference-javascript "javascript reference")</span></sup>
The items in this section document the capabilities of the UI-KIT framework classes:

- [UIKit](#reference-javascript-framework-ui-kit "UIKit")
- [KitResourceManager](#reference-javascript-framework-kit-resource-manager "KitResourceManager")
- [KitNavigator](#reference-javascript-framework-kit-navigator "KitNavigator")
- [KitMessenger](#reference-javascript-framework-kit-messenger "KitMessenger")
- [KitRenderer](#reference-javascript-framework-kit-renderer "KitRenderer")
&nbsp;

#### UIKit <span id="reference-javascript-framework-ui-kit" /><sup><span style="font-size:8pt;">[top](#toc "table of contents") | [..^](#reference-javascript-framework "framework classes")</span></sup>
`UIKit` performs initialization and provides global access to the other UI-KIT classes.
&nbsp;

##### Properties  

> ```javascript
> /**
>  @returns {Window}
>  */
> static get window()
> ```
Gets the window object

> ```javascript
> /**
>  @param {Window} value - The window
>  */
> static set window(value)
> ```
Sets the window object

> ```javascript
> /**
>  @returns {Document}
>  */
> static get document()
> ```
Gets the document object

> ```javascript
> /**
>  @param {Document} value - The document
>  */
> static set document(value)
> ```
Sets the document object

> ```javascript
> /**
>  @returns {Console}
>  */
> static get console()
> ```
Gets the console object

> ```javascript
> /**
>  @param {Console} value - The console
>  */
> static set console(value)
> ```
Sets the console object

> ```javascript
> /**
>  @returns {KitResourceManager}
>  */
> static get resourceManager()
> ```
Gets the resource manager

> ```javascript
> /**
>  @param {KitResourceManager} value - The resource manager
>  */
> static set resourceManager(value)
> ```
Sets the resource manager

> ```javascript
> /**
>  @returns {KitNavigator}
>  */
> static get navigator()
> ```
Gets the navigator

> ```javascript
> /**
>  @param {KitNavigator} value - The navigator
>  */
> static set navigator(value)
> ```
Sets the navigator

> ```javascript
> /**
>  @returns {KitMessenger}
>  */
> static get messenger()
> ```
Gets the messenger

> ```javascript
> /**
>  @param {KitMessenger} value - The messenger
>  */
> static set messenger(value)
> ```
Sets the messenger

> ```javascript
> /**
>  @returns {KitRenderer}
>  */
> static get renderer()
> ```
Gets the renderer

> ```javascript
> /**
>  @param {KitRenderer} value - The renderer
>  */
> static set renderer(value)
> ```
Sets the renderer

##### Methods

> ```javascript   
> /**     
> @param {string} key - The key used to find the dependency
> @returns {any}
> */  
> static getDependency(key)
> ```
> Gets a dependency by key

> ```javascript    
> /**     
> @param {string} key - The dependency key     
> @param {any} value - The dependency     
> */    
> static setDependency(key, value)
> ```
> Sets a dependency

> ```javascript    
> static async initialize() 
> ```
> Adds UIKit to the global scope, initializes navigation, and performs an initial render of the document body

---

#### KitResourceManager <span id="reference-javascript-framework-kit-resource-manager" /><sup><span style="font-size:8pt;">[top](#toc "table of contents") | [..^](#reference-javascript-framework "framework classes")</span></sup>
`KitResourceManager` encapsulates functionality for interacting with network resources.  
&nbsp;

##### Methods
&nbsp;
> ```javascript
> /**
>   @param {any} input - Resource path
>   @param {any} init - Options
>   @returns {Promise}
> */
> async fetch(input, init)
> ```
> Gets content from a network resource.

&nbsp;

> ```javascript
> /**
>   @param {string} moduleName - The name of the module to import
>   @returns {any}
> */
> async import(moduleName)
> ```
> Imports a script module.

&nbsp;

---

#### KitNavigator <span id="reference-javascript-framework-kit-navigator" /><sup><span style="font-size:8pt;">[top](#toc "table of contents") | [..^](#reference-javascript-framework "framework classes")</span></sup>
`KitNavigator` facilitates navigation functionality.
This class uses [KitMessenger](#reference-javascript-framework-kit-messenger "KitMessenger") to publish navigation events.

> Example of a component subscribing to navigation events
> ```javascript
> async init(kitElement) {
>   this.#kitElement = kitElement;
>   this.routeName = UIKit.navigator.getHash(UIKit.document.location.href) ?? "";
>   const elementKey = this.#kitElement.getAttribute("kit-element-key");
>   const subscriber = {
>     elementKey: elementKey,
>     id: `nav-${elementKey}`,
>     object: this,
>     callback: this.onNavigation.name
>   };
>   UIKit.messenger.subscribe(KitNavigator.NavTopic, subscriber);
> }

> async onNavigation(url) {
>   this.routeName = UIKit.navigator.getHash(url) ?? "";
>   await UIKit.renderer.renderElement(this.#kitElement);
> }
> ```

&nbsp;

##### Methods

> ```javascript
> async initialize()
> ```
> Configures an application to generate navigation events from the browser `popstate` event.  

&nbsp;  

>  ```javascript
> /**
>  @param {string} url - The destination url
>  */
> async navigate(url)
> ```
> Navigates to the specified url

&nbsp;  

> ```javascript
> /**
> @param {any} url - The url to examine
> @returns {string}
> */
> getHash(url) 
> ```
> Gets the hash portion of a url
---

#### KitMessenger <span id="reference-javascript-framework-kit-messenger" /><sup><span style="font-size:8pt;">[top](#toc "table of contents") | [..^](#reference-javascript-framework "framework classes")</span></sup>
`KitMessenger` is used to send and receive messages between components.

> Example of publishing a message
> ```javascript
> const msg = { prop1: "abc", prop2: "def" };
> await UIKit.messenger.publish("MyTopic", msg);
> ```

> Example of a component subscribing to receive published messages
> ```javascript
> async init(kitElement) {
>   this.kitElement = kitElement;
>   const elementKey = UIKit.renderer.getKitElementKey(this.kitElement);
>   const subscriber = {
>     elementKey: elementKey,
>     id: `my-topic-subscriber-${elementKey}`,
>     object: this,
>     callback: this.onMyTopicEvent.name
>   };
>   UIKit.messenger.subscribe("MyTopic", subscriber);
> }
> 
> async onMyTopicEvent(message) {
>   // Do something with received message here
>   ...
> }
> ```

&nbsp;

##### Methods

> ```javascript
> /**
> @param {string} topicName - The name of the topic
> @param {any} message - The message to be published
> */
> async publish(topicName, message) 
> Publish a message to subscribers of a topic
> ```

> ```javascript
> /**
> @param {string} topicName - The name of the topic
> @param {{elementKey: number, id: string, object: any, callback: string}} subscriber - The subscriber
> */
> subscribe(topicName, subscriber)
> Subscribe to receive messages published to a topic
> ```

---

#### KitRenderer <span id="reference-javascript-framework-kit-renderer" /><sup><span style="font-size:8pt;">[top](#toc "table of contents") | [..^](#reference-javascript-framework "framework classes")</span></sup>  
Renders component html elements  

##### Methods

> ```javascript
> async render()
> ```
> Renders the document body

> ```javascript
> /**
> @param {HTMLElement} element -  The element to render
> */
> async renderElement(element)
> ```
> Renders an element

> ```javascript
> /**
> @param {number} elementKey - The key for the element where the object is stored
> @param {number} objectKey - The key for the object within the element's object store
> */
> getObject(elementKey, objectKey)
> ```
> Retrieves an object from a kit element's object store by object key

> ```javascript
> /**
> @param {HTMLElement} kitElement - The kit element
> */
> getKitElementKey(kitElement)
> ```
> Retrieves the element key for a kit element

> ```javascript
> /**
> @param {HTMLElement} kitElement - The kit element
> @param {string} objectAlias - The alias for the object
> */
> getKitElementObject(kitElement, objectAlias = "model")
> ```
> Retrieves an object from a kit element's object store by alias

---

