

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

In concept, UI-KIT is similar to Angular, React, or Vue, but with pared-down functionality and less to learn for developers new to UI development.
UI-KIT defines 3 custom html elements (`<kit-component>`, `<kit-if>`, and `<kit-array>`) and makes use of a couple of simple javascript conventions.
All that is needed as a prerequisite is a basic understanding of HTML, CSS, and Javascript:

> Hello UI-Kit! HTML code example:
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
>   <div>
>     <kit-component data-kit-model="{ title: 'HELLO UI-KIT', isEasy: true,  howEasy: [ 'a', 'b', 'c' ] }"
>                    data-kit-model-ref="model">
>       <h1>%{#model.title}%</h1>
>         <kit-if data-kit-condition="#model.isEasy">
>           <br />
>           <p>This is as easy as:</p>
>           <kit-array data-kit-array="#model.howEasy"
>                      data-kit-item-ref="item"
>                      data-kit-item-index-ref="i">
>             <div>
>               <kit-if data-kit-condition="#i < #model.howEasy.length - 1">%{#item}%,</kit-if>
>               <kit-if data-kit-condition="#i === #model.howEasy.length - 1">%{#item}%!</kit-if>
>             </div>
>           </kit-array>
>         </kit-if>
>       </kit-component>
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
> | a,                      |
> | b,                      |
> | c!                      |
> |                         |
> ---------------------------
> </pre>


The [Quick start guide](#quick-start "quick start guide") below offers a break down on the code concepts illustrated above as well as a step-by-step guide for building a simple single-page web application with UI-KIT. After exploring the quick start topics below you should be able to drop the ui-kit.js file into your web application and start using `<kit-component>`, `<kit-if>`, and `<kit-array>` tags to build applications.  
A full reference on the UI-KIT html tags and attributes and Javascript framework can be found in the [Reference](#reference "reference") section at the end of this document.

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
      - [\<kit-array>](#reference-html-tags-kit-array "<kit-array>")
      - [\<kit-component>](#reference-html-tags-kit-component "<kit-component>")
      - [\<kit-if>](#reference-html-tags-kit-if "<kit-if>")
    - [Attributes](#reference-html-attributes "html attributes")
      - [data-kit-add-attributes](#reference-html-attributes-data-kit-add-attributes "data-kit-add-attributes attribute")
      - [data-kit-array](#reference-html-attributes-data-kit-array "data-kit-array attribute")
      - [data-kit-array-ref](#reference-html-attributes-data-kit-array-ref "data-kit-array-ref attribute")
      - [data-kit-component-id](#reference-html-attributes-data-kit-component-id "data-kit-component-id attribute")
      - [data-kit-condition](#reference-html-attributes-data-kit-condition "data-kit-condition attribute")
      - [data-kit-item-index-ref](#reference-html-attributes-data-kit-item-index-ref "data-kit-item-index-ref attribute")
      - [data-kit-item-ref](#reference-html-attributes-data-kit-item-ref "data-kit-item-ref attribute")
      - [data-kit-model](#reference-html-attributes-data-kit-model "data-kit-model attribute")
      - [data-kit-model-input](#reference-html-attributes-data-kit-model-input "data-kit-model-input attribute")
      - [data-kit-model-ref](#reference-html-attributes-data-kit-model-ref "data-kit-model-ref attribute")
      - [data-kit-template-path](#reference-html-attributes-data-kit-template-path "data-kit-template-path attribute")
    - [Special characters](#reference-html-special-characters "special characters")
  - [CSS reference](#reference-css "css reference")
  - [Javascript reference](#reference-javascript "javascript reference")
    - [Working with models](#reference-javascript-working-with-models "working with models")
    - [Framework classes](#reference-javascript-framework "framework classes")
      - [KitComponent](#reference-javascript-framework-kit-component "KitComponent")
      - [KitComponentOptions](#reference-javascript-framework-kit-component-options "KitComponentOptions")
      - [KitComponentType](#reference-javascript-framework-kit-component-type "KitComponentType")
      - [KitDependencyManager](#reference-javascript-framework-kit-dependency-manager "KitDependencyManager")
      - [KitMessenger](#reference-javascript-framework-kit-messenger "KitMessenger")
      - [KitMutationObserverFactory](#reference-javascript-framework-kit-mutation-observer-factory "KitMutationObserverFactory")
      - [KitNavigator](#reference-javascript-framework-kit-navigator "KitNavigator")
      - [KitRenderer](#reference-javascript-framework-kit-renderer "KitRenderer")
      - [KitResourceManager](#reference-javascript-framework-kit-resource-manager "KitResourceManager")
      - [KitStartup](#reference-javascript-framework-kit-startup "KitStartup")

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
Each UI-KIT component (represented by a `<kit-component>` tag) is comprised of an html fragment as a template and (optionally) a javascript model. We'll get to the javascript in later steps.  In this step, we're just focusing on the html templates.  
A component's html template can either be defined "inline" as the `<kit-component>` tag's inner html, or it can be loaded from an external file using the data-kit-template-path attribute.
We've seen an example of the inline approach in the "Hello UI-Kit! HTML" code example at the top of this document.
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
> <kit-component data-kit-template-path="/components/heading/heading.html" data-kit-model="null"></kit-component>
> <kit-component data-kit-template-path="/components/navigation/navigation.html" data-kit-model="null"></kit-component>
> <kit-component data-kit-template-path="/components/content/content.html" data-kit-model="null"></kit-component>
> ```

 We've added one `<kit-component>` tag for each of our 3 components.  
`<kit-component>` is a custom html element (1 of 3) used by UI-KIT to define a component.

> <span style="color:#FFD700;font-weight:bold;">◊</span> _Note:_  
> _Normally when we define a component with the data-kit-template-path attribute as above, UI-KIT expects to find a javascript module in a related location.  Since we're not covering javascript models yet in this Quick start step, we take a short cut by explicitly providing a (null) model using the data-kit-model attribute.  This isn't something you would do normally, but it's useful in this context._

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

:point_right: _Action: Add heading.css_  
In the folder for the header component, add a css file called heading.css.

> heading.css:
> ```css
> @scope (#heading) {
>     :scope {
>         position: fixed;
>         width: 100vw;
>         height: 60px;
>         top: 0;
>         left: 0;
>         display: flex;
>         border-bottom:1px solid black;
>         background-color: silver;
>     }
>     h2 {
>         padding: 10px;
>     }
> }
> ```

This fixes the position of the heading component to the top left of the page and gives it a background color.

> <span style="color:#FFD700;font-weight:bold;">◊</span> _Note:_  
> _The @scope pseudo-class sets the scope for the contained css rules.
> Setting the scope to the id of the top element in the component's template limits the css rules to the heading component.
> Using this pattern helps to isolate the css rules for each component and makes the css easier to manage._

:point_right: _Action: Add reference to heading.css_  
Now we need to add a reference to this css file in heading.html:

> heading.html:
> ```html
> <div id="heading">
>   <link rel="stylesheet" href="/components/heading/heading.css" />
>   <h2>Hello UI-KIT!</h2>
> </div>
> ```

We'll do something similar for the navigation component.  

:point_right: _Action: Add navigation.css_  
Add a css file named navigation.css to the navigation component folder.

> navigation.css:
> ```css
> @scope (#navigation) {
>     :scope {
>         position: fixed;
>         left: 0;
>         width: 150px;
>         top: 60px;
>         bottom: 0;
>         border-right:1px solid black;
>         background-color: silver;
>     }
>     h2, div {
>     	padding: 10px;
>     }
> }
> ```

:point_right: _Action: Add reference to navigation.css_  
And refer to this css file in navigation.html:

> navigation.html:
> ```html
> <div id="navigation">
>   <link rel="stylesheet" href="/components/navigation/navigation.css" />
>   <h2>Navigation</h2>
> </div>
> ```

This fixes the position of the navigation component to the left of the page and gives it a background.

:point_right: _Action: Add content.css_  
Finally, we need to fix up the content area style so the header and navigation panels don't cover up the content.

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

:point_right: _Action: Add reference to content.css_  
And refer to this css file in content.html:

> content.html:
> ```html
> <div id="content">
>   <link rel="stylesheet" href="/components/content/content.css" />
>   <h2>Content area</h2>
> </div>
> ```

Ok, at this point your folder structure should look like this:

>```folder structure
> > hello-ui-kit
>   > components
>     > heading
>       - heading.css
>       - heading.html
>     > navigation
>       - navigation.css
>       - navigation.html
>     > content
>       - content.css
>       - content.html
>   - index.html
>   - ui-kit.js
>```

:point_right: _Action: Save all changes and refresh browser_  
After saving your changes and refreshing your browser, you should see a page with clear content sections for heading, navigation, and content.

> Browser view:
> <pre>
> ----------------------------------
> |                                |
> | Welcome to UI-KIT!             |
> |             --------------------
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
This is where "smart" components, components with associated javascript code (called the javascript model), come in to the mix.

There are two ways to define a component with a javascript model:
1. Define the model using the `data-kit-model` attribute.
2. Define the model in a separate javascript file in the same folder where the component's html template is defined.

The first method is often used for simpler components where the parent component has access to all the facts needed to create the model.
The "Hello UI-Kit! HTML" code example markup at the top of this document uses this method:

> using the `data-kit-model` attribute:
> ```html
> <kit-component data-kit-model="{ title: 'Hello UI-Kit', isEasy: true,  howEasy: [ 'a', 'b', 'c' ] }"
>                data-kit-model-ref="model">
> ```

In this example, the `data-kit-model` attribute sets the component's javascript model to an object with 3 properties:

> javascript model:
> ```javascript
> { 
>   title: 'Hello UI-Kit', 
>   isEasy: true,  
>   howEasy: [ 'a', 'b', 'c' ] 
> }
> ```

The `data-kit-model-ref` attribute provides a way to reference the model in the component's html template:

> html template:
> ```html
> <h1>%{#model.title}%</h1>
> ```

Let's unpack that syntax a bit.  
Since `data-kit-model-ref` equals "model", we can reference the model using the name "#model".  The hashtag is always used by UI-KIT to prefix a model reference within an html template.  

`%{` and `}%` are also special characters used by UI-KIT.  
UI-KIT evaluates the text between `%{` and `}%` as javascript and writes the result into the html.

> <span style="color:#FFD700;font-weight:bold;">◊</span> _Note:_  
> _If you ever need to render a literal `%{` or `}%` in your html, you can escape them by prefixing with a backslash: `\%{` and `\}%`._

The value of `data-kit-model-ref` must be unique in the context of the current html template.  
The following markup would result in an error because the child component has defined a `data-kit-model-ref` value with the same value as its parent component.:

> non-unique `data-kit-model-ref` attribute:
> ```html
> <kit-component data-kit-template-path="/comp1.html" data-kit-model-ref="myModel">
>   <kit-component data-kit-template-path="/comp2.html" data-kit-model-ref="myModel">
>   </kit-component>
> </kit-component>
> ```

Now let's turn to the second method for defining a component's javascript model: using a separate javascript file. For this, we'll learn by creating a model for our content component.  

:point_right: _Action: Remove `data-kit-model` attribute_  
First, undo the short-cut we took earlier by removing the `data-kit-model` attribute from the `<kit-component>` tag in index.html where the content component is referenced.

> `<kit-component>` tag for the content component (in index.html):
> ```html
> <kit-component data-kit-template-path="/components/content/content.html"></kit-component>
> ```

When a component has the `data-kit-template-path` attribute and a model isn't specified using the `data-kit-model` attribute, UI-KIT expects to find a model in a Javascript file in the same folder and with the same name as the html template.  
So, if you create an html template at "/components/my-component/my-component.html", UI-KIT expects to find a javascript file at "/components/my-component/my-component.js".  
So now that we've taken out our `data-kit-model="null"` shortcut in index.html, UI-KIT expects a javascript file at "/components/content/content.js".  

:point_right: _Action: Add content.js file_    
Let's add our content.js file.

> content.js:
> ```javascript
> export function createModel() {
>     return new ContentModel();
> }
> 
> class ContentModel {
>     async initialize(componentId) {
>         this.myComponentId = componentId;
>         this.content = "Here is my content ...";
>     }
> 
>     displayComponentId() {
>         alert(this.myComponentId);
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

It isn't required, but if the model returned from the `createModel()` function has an async `initialize()` method, as we do in this example, UI-KIT will call that method with the component's auto-generated component id as an argument when it first calls `createModel()` to create the component.  
In this case, in our `initialize()` method we set two properties on our model: `myComponentId` and `content`.

> <span style="color:#FFD700;font-weight:bold;">◊</span> _Note:_  
> _UI-KIT will also look for an optional `onLoadedInDocument()` method on the model.  If it exists, UI-KIT will call it after the component has been rendered in the document.  See  [Working with models](#reference-javascript-working-with-models "working with models") for more info._

:point_right: _Action: Update content.html_    
To make use of this javascript code, let's update content.html to reference the model:

> content.html:
> ```html
> <div id="content">
>   <link rel="stylesheet" href="/components/content/content.css" />
>   <h2>Content area</h2>
>   <p>%{#model.content}%</p>
>   <div>
>     <button onclick="#model.displayComponentId()">display component id</button>
>   </div>
> </div>
> ```

Note the use of "#model" to refer to the model.  For components defined with an external html template, "model" is always implicitly defined as the reference name for the model.
It's only for components where the html template is defined inline as inner html where the developer explicitly chooses a reference name for the model.  

:point_right: _Action: Save all changes and refresh browser_    
The content component should now display:
- "Here is my content ..."
- and a button with the text "display component id"

:point_right: _Action: Test updates_    
Clicking the "display component id" button demonstrates calling a function on the component's model and displays an alert with the text "my component id is: 4".

> <span style="color:#FFD700;font-weight:bold;">◊</span> _Note:_  
> _Why is component id equal to 4? UI-KIT automatically designates the document body tag as the first component.  Header is component #2, Navigation is component #3, and Content is component #4.
> We're not doing much with the component id yet.  But it's useful if you need to re-render the component as we'll see later._

There's a little more to learn about UI-KIT javascript models, but we'll cover the rest in subsequent steps.

&nbsp;  

---
## Step 4: Conditional rendering <span id="quick-start-4" /><sup><span style="font-size:8pt;">[top](#toc "table of contents") | [prev](#quick-start-3 "component javascript models") | [next](#quick-start-5 "looping")</span></sup>
---
In this step, we'll learn how to conditionally render html content using the `<kit-if>` tag.
For this step, we'll add a "currentSection" property to our content component model and use it to conditionally render only the "current content section" of our template.
In a subsequent step, we'll extend this to display the current content section based on user navigation actions.

:point_right: _Action: Update content.js_    
First, in our content component model class, let's get rid of the "content" property we added earlier and add a "currentSection" property.    
For now, we'll hard-code currentSection's value to "#section1" within the `initialize()` method.

> content.js:
> ```javascript
> async initialize(componentId) {
>   this.myComponentId = componentId;
>   this.currentSection = "#section1";
> }
> ```

:point_right: _Action: Update content.html_    
Now, let's update the content.html to add different sections to the template but only render the "current" section.

> content.html:
> ```html
> <div id="content">
>   <link rel="stylesheet" href="/components/content/content.css" />
>   <h2>Content area</h2>
>   <kit-if data-kit-condition="#model.currentSection === '#section1' || !#model.currentSection">
>     <div>Section 1 content</div>
>   </kit-if>
>   <kit-if data-kit-condition="#model.currentSection === '#section2'">
>     <div>Section 2 content</div>
>   </kit-if>
>   <kit-if data-kit-condition="#model.currentSection === '#section3'">
>     <div>Section 3 content</div>
>   </kit-if>
>   <div>
>     <button onclick="#model.displayComponentId()">display component id</button>
>   </div>
> </div>
> ```

:point_right: _Action: Save all changes and refresh browser_    
Refreshing the browser should now display "Section 1 content" only and not any of the other sections.  

The value of `data-kit-condition` is evaulated for each `<kit-if>` tag.  
The html inside each `<kit-if>` tag is only rendered if the condition is true.

&nbsp;  

---
## Step 5: Looping <span id="quick-start-5" /><sup><span style="font-size:8pt;">[top](#toc "table of contents") | [prev](#quick-start-4 "conditional rendering") | [next](#quick-start-6 "navigation")</span></sup>
---
The `<kit-array>` tag is used to loop over an array of items and render html content for each item in the array.  
In this step, we'll contrive to extend section 1 in the content component to use the `<kit-array>` tag.  

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
Next, we'll update the inner HTML of the element representing section 1 in content.html to use the `<kit-array>` tag to loop over the items in section 1.

> content.html:
> ```html
>   <kit-if data-kit-condition="#model.currentSection === '#section1' || !#model.currentSection">
>     <div>Section 1 content</div>
>     <ul>
>       <kit-array data-kit-array="#model.getSection1Items()" data-kit-item-ref="item">
> 	      <li id="%{#item.itemId}%">Name: %{#item.name}%</li>
>       </kit-array>
>     </ul>
>   </kit-if>
> ```

:point_right: _Action: Save all changes and refresh browser_    
Refreshing the browser should now display our list of 5 items in section 1.  

The `data-kit-array` attribute is used to specify the array of items to loop over.  
The `data-kit-item-ref` attribute (with the value "item") is used to reference the current item in the array within the html template. 
The item reference name is prefixed with a hashtag just as with the `data-kit-model-ref` attribute we used earlier. 

It's also possible to reference the array itself using the `data-kit-array-ref` attribute or the current item's index using the `data-kit-item-index-ref` attribute as we saw in the "Hello UI-Kit! HTML" code example at the top of this document.
See the [\<kit-array>](#reference-html-tags-kit-array "<kit-array>") for more info.

&nbsp;  

---
## Step 6: Navigation <span id="quick-start-6" /><sup><span style="font-size:8pt;">[top](#toc "table of contents") | [prev](#quick-start-5 "looping") | [next](#quick-start-7 "state transitions")</span></sup>
---

In the previous steps, we learned how to use the `<kit-component>`, `<kit-if>`, and `<kit-array>` tags as building blocks for creating dynamic html content.
Now we're ready to use what we've learned to dynamically display content based on navigation events.  

:point_right: _Action: Update navigation.html_    
We'll start by adding navigation links to the navigation component.

> navigation.html:
> ```html
> <div id="navigation">
>   <link rel="stylesheet" href="/components/navigation/navigation.css" />
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

:point_right: _Action: Add import statment to content.js_    
First, we're going to be calling some methods in the UI-KIT library so we'll need to add an import statement at the top of the file.

> import statement:
> ```javascript
> import { KitMessenger, KitNavigator, KitRenderer } from "../../ui-kit.js";
> ```  

:point_right: _Action: Add `onNavigation()` method to content.js_    
Second we need to add an `onNavigation()` method that will respond to navigation events and re-render the component:

> onNavigation() function:
> ```javascript
> onNavigation(url) {      
>   this.initialize(this.myComponentId);
> }
> ```

:point_right: _Action: Update `initialize()` method in content.js_    
Finally, in the `initialize()` method, instead of hard-coding the current section value, we'll retrieve it from the current url.  We'll also call `KitMessenger.subscribe()` to start listening for navigation events.  

> `initialize()` method:
> ```javascript
> async initialize(componentId) {
>   this.myComponentId = componentId;
>   this.currentSection = KitNavigator.getCurrentUrlFragment();
>   KitMessenger.subscribe(KitNavigator.navTopicName, this.myComponentId, this.onNavigation.name);
>   KitRenderer.renderComponent(this.myComponentId);
> }
> ```

Our `KitMessenger.subscribe()` call tells UI-KIT to call the `onNavigation()` method whenever a navigation event occurs.

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

UI-KIT takes a different (simpler) approach.  The state of component models is not tracked internally by the framework and it is left to the developer to explicitly synchronize the view after state changes occur. We saw this explicit synchronization in the previous step when we called `KitRenderer.renderComponent()` to re-render the content component after a navigation event. In this step, we'll explore state transitions a bit more with another example:  showing a loading indicator.

It's often the case with web applications that it takes some time to get the data needed to fully present a component.  Often we need to load a file, query a database, or fetch data from an API over the internet, all of which takes some time.  To show our users that the data is on its way, it's common to initially show a loading indicator and then later, when the model changes state from not having data to having data, we update the view to show the requested data. In this step, we'll update the content component to initially display a loading indicator when section 1 data is requested and then transition to showing data.

:point_right: _Action: Update content.css_    
First, let's borrow an animated css loading indicator from the web and add it to our styles for the content component.

> content.css:
> ```css
> @scope (#content) {
>   :scope {
>     margin-top:60px;
>     margin-left:150px;
> 	  padding: 10px;
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
> ```

I borrowed the css for this loader from [css-loaders.com](https://css-loaders.com/ "css-loaders.com"). It looks like it's designed to be used with a div element with class "loader" so we'll need to update our html template.

:point_right: _Action: Update content.html_    
Update the section 1 part of our content template to make use of our new css loading indicator.

> section 1 of content.html:
> ```html
> <kit-if data-kit-condition="#model.currentSection === '#section1' || !#model.currentSection">
>   <div>Section 1 content</div>
>   <kit-if data-kit-condition="#model.isSection1Loading">
>     <div style="margin:20px;" class="loader"></div>
>   </kit-if>
>   <kit-if data-kit-condition="!#model.isSection1Loading">
>     <ul>
>       <kit-array data-kit-array="#model.section1Items" data-kit-item-ref="item">
> 	      <li id="%{#item.itemId}%">Name: %{#item.name}%</li>
>       </kit-array>
>     </ul>
>   </kit-if>
> </kit-if>
> ```

We've added our div with `class="loader"` for our loading indicator and wrapped in in a `<kit-if>` tag so that it is only displayed when `isSection1Loading` is true.
Also, we've wrapped the main content of section 1 in a `<kit-if>` tag so that it is only displayed when `isSection1Loading` is false, meaning it's done loading.
And note that we've changed from using the `getSection1Items()` method to using a `section1Items` property on the model to get our items array so we'll have to update our Javascript model correspondingly.

:point_right: _Action: Update content.js_    
Remove the existing `getSection1Items()` method and update `initialize()` to set a `section1Items` property.

> content.js:
> ```javascript
> async initialize(componentId) {
>   this.myComponentId = componentId;
>   this.currentSection = KitNavigator.getCurrentUrlFragment();
>   KitMessenger.subscribe(KitNavigator.navTopicName, this.myComponentId, this.onNavigation.name);
> 
>   if (this.currentSection === "#section1") {
> 
>     // show state without data (loading)
>     this.section1Items = [];
>     this.isSection1Loading = true;
>     KitRenderer.renderComponent(this.myComponentId);
> 
>     // get data (simulating a 3-second delay)
>     await new Promise(r => setTimeout(r, 3000));
>     this.section1Items = [
>       { itemId: 1, name: "Item 1" },
>       { itemId: 2, name: "Item 2" },
>       { itemId: 3, name: "Item 3" },
>       { itemId: 4, name: "Item 4" },
>       { itemId: 5, name: "Item 5" }
>     ];
>     this.isSection1Loading = false;
>   }
> 
>   // synchronize view after state update
>   KitRenderer.renderComponent(this.myComponentId);
> }
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
This section of the reference covers the 3 special tags used by UI-KIT:
- [\<kit-array>](#reference-html-tags-kit-array "<kit-array>")
- [\<kit-component>](#reference-html-tags-kit-component "<kit-component>")
- [\<kit-if>](#reference-html-tags-kit-if "<kit-if>")

&nbsp;

---
#### `<kit-array>` <span id="reference-html-tags-kit-array" /><sup><span style="font-size:8pt;">[top](#toc "table of contents") | [..^](#reference-html-tags "tags")</span></sup>
The `<kit-array>` tag is used to loop over an array of items and render html content for each item in the array.

> kit-array example:
> ```html
> <ul>
> <kit-array data-kit-array="[{ id:'a', desc:'item a' }, { id:'b', desc:'item b' }, { id:'c', desc:'item c' }]" 
>            data-kit-array-ref="items"
>            data-kit-item-ref="item"
>            data-kit-item-index-ref="i">
>     <li id="%{#item.id}%">%{#item.desc}% (%{#i + 1}% of %{#items.length}%)</li>
> </kit-array>
> </ul>
> <!-- renders: 
> <ul>
>   <li id="a">item a (1 of 3)</li>
>   <li id="b">item b (2 of 3)</li>
>   <li id="c">item c (3 of 3)</li>
> </ul>
> -->
> ```

The following attributes are specially applicable to the `<kit-array>` tag:
- [data-kit-array](#reference-html-attributes-data-kit-array "data-kit-array attribute")
- [data-kit-array-ref](#reference-html-attributes-data-kit-array-ref "data-kit-array-ref attribute")
- [data-kit-item-index-ref](#reference-html-attributes-data-kit-item-index-ref "data-kit-item-index-ref attribute")
- [data-kit-item-ref](#reference-html-attributes-data-kit-item-ref "data-kit-item-ref attribute")

&nbsp;

---
#### `<kit-component>` <span id="reference-html-tags-kit-component" /><sup><span style="font-size:8pt;">[top](#toc "table of contents") | [..^](#reference-html-tags "tags")</span></sup>
The `<kit-component>` tag is used to define a UI-KIT component and is comprised of an html fragment as a template and (optionally) a javascript model.

> Example 1: `<kit-component>` tag with inline html template:
> ```html
> <kit-component data-kit-model="{ prop1: 'abc', prop2: 'def' }" data-kit-model-ref="myComponent">
>   <div>prop1 = %{#myComponent.prop1}%</div>
>   <div>prop2 = %{#myComponent.prop2}%</div>
> </kit-component>
> <!-- renders: 
> <div>prop1 = abc</div>
> <div>prop2 = def</div>
> -->
> ```

The html template may be defined "inline" using inner html (as above), or it can be loaded from an external file using the `data-kit-template-path` attribute.

> Example 2: `<kit-component>` tag with external html template
> ```html
> <kit-component data-kit-template-path="/components/my-component/my-component.html" 
>                data-kit-model-input="{ prop1: 'abc', prop2: 'def' }">
> </kit-component>
> ```

When a component is defined with an external html template using the `data-kit-template-path` attribute and a model is not specified in the markup using the `data-kit-model` attribute, UI-KIT expects to find a model in a javascript file in the same folder and with the same name as the html template.  
For example, if the html template is at "/components/my-component/my-component.html", UI-KIT expects to find a javascript file at "/components/my-component/my-component.js".  
For more information on defining a component's javascript model, see [Working with models](#reference-javascript-working-with-models "working with models").

The following attributes are specially applicable to the `<kit-component>` tag:
- [data-kit-model](#reference-html-attributes-data-kit-model "data-kit-model attribute")
- [data-kit-model-input](#reference-html-attributes-data-kit-model-input "data-kit-model-input attribute")
- [data-kit-model-ref](#reference-html-attributes-data-kit-model-ref "data-kit-model-ref attribute")
- [data-kit-template-path](#reference-html-attributes-data-kit-template-path "data-kit-template-path")

&nbsp;

---
#### `<kit-if>` <span id="reference-html-tags-kit-if" /><sup><span style="font-size:8pt;">[top](#toc "table of contents") | [..^](#reference-html-tags "tags")</span></sup>
The `<kit-if>` tag is used to conditionally render html elements.

> kit-if example:
> ```html
> <kit-if data-kit-condition="1 + 1 === 2">
>   <p>1 + 1 equals 2</p>
> </kit-if>
> <kit-if data-kit-condition="1 + 1 === 3">
>   <p>1 + 1 equals 3 (!?)</p>
> </kit-if>
> <!-- renders: 
> <p>1 + 1 equals 2</p>
> -->
> ```

The [data-kit-condition](#reference-html-attributes-data-kit-condition "data-kit-condition attribute") attribute is specially applicable to the `<kit-if>` tag.

&nbsp;

### Attributes <span id="reference-html-attributes" /><sup><span style="font-size:8pt;">[top](#toc "table of contents") | [..^](#reference-html "html reference")</span></sup>
This section of the reference covers special html "data-kit" attributes defined by UI-KIT:

- [data-kit-add-attributes](#reference-html-attributes-data-kit-add-attributes "data-kit-add-attributes attribute")
- [data-kit-array](#reference-html-attributes-data-kit-array "data-kit-array attribute")
- [data-kit-array-ref](#reference-html-attributes-data-kit-array-ref "data-kit-array-ref attribute")
- [data-kit-component-id](#reference-html-attributes-data-kit-component-id "data-kit-component-id attribute")
- [data-kit-condition](#reference-html-attributes-data-kit-condition "data-kit-condition attribute")
- [data-kit-item-index-ref](#reference-html-attributes-data-kit-item-index-ref "data-kit-item-index-ref attribute")
- [data-kit-item-ref](#reference-html-attributes-data-kit-item-ref "data-kit-item-ref attribute")
- [data-kit-model](#reference-html-attributes-data-kit-model "data-kit-model attribute")
- [data-kit-model-input](#reference-html-attributes-data-kit-model-input "data-kit-model-input attribute")
- [data-kit-model-ref](#reference-html-attributes-data-kit-model-ref "data-kit-model-ref attribute")
- [data-kit-template-path](#reference-html-attributes-data-kit-template-path "data-kit-template-path attribute")

&nbsp;

---
#### data-kit-add-attributes <span id="reference-html-attributes-data-kit-add-attributes" /><sup><span style="font-size:8pt;">[top](#toc "table of contents") | [..^](#reference-html-attributes "attributes")</span></sup>
`data-kit-add-attributes` contains a comma-separated list of attributes to be added to an element.
Each attribute in the list may be a name-value pair (separated by an equals sign) or just a name.  
This attribute is useful for adding attributes at runtime that do not have a value like `checked` or `disabled`.

> data-kit-add-attributes example:
> ```html
> <div data-kit-add-attributes="prop1,prop2=abc">add attribute example</div>
> <!-- renders: 
> <div prop1 prop2="abc">add attribute example</div>
> -->
> ```

> <span style="color:#FFD700;font-weight:bold;">◊</span> _Note:_   
> _Using `%{` and `}%` can be a good way to set the value of an attribute but should not be used to add attributes as the browser may adjust the text of the added attribute in unexpected ways (changing case for example).  
The `data-kit-add-attributes` attribute is the preferred method for adding attributes with UI-KIT.

&nbsp;

---
#### data-kit-array <span id="reference-html-attributes-data-kit-array" /><sup><span style="font-size:8pt;">[top](#toc "table of contents") | [..^](#reference-html-attributes "attributes")</span></sup>
`data-kit-array` is used to specify the array of items to loop over in a [\<kit-array>](#reference-html-tags-kit-array "<kit-array>") tag.  
UI-KIT evaluates the value of this attribute as Javascript.

&nbsp;

---
#### data-kit-array-ref <span id="reference-html-attributes-data-kit-array-ref" /><sup><span style="font-size:8pt;">[top](#toc "table of contents") | [..^](#reference-html-attributes "attributes")</span></sup>
`data-kit-array-ref` contains a label that when prefixed with a hashtag can be used to reference the array being looped over in a [\<kit-array>](#reference-html-tags-kit-array "<kit-array>") tag.  
Reference attributes (including `data-kit-array-ref`, `data-kit-item-index-ref`, `data-kit-item-ref`, and `data-kit-model-ref`) may not have the same value as a reference attribute defined on a parent component element.  

&nbsp;

---
#### data-kit-component-id <span id="reference-html-attributes-data-kit-component-id" /><sup><span style="font-size:8pt;">[top](#toc "table of contents") | [..^](#reference-html-attributes "attributes")</span></sup>
`data-kit-component-id` is an attribute that is automatically added by UI-KIT to each component element when it's corresponding [KitComponent](#reference-javascript-kit-component "KitComponent") instance is created.
 The value of this attribute is the component's unique id.

 &nbsp;

 ---
#### data-kit-condition <span id="reference-html-attributes-data-kit-condition" /><sup><span style="font-size:8pt;">[top](#toc "table of contents") | [..^](#reference-html-attributes "attributes")</span></sup>
`data-kit-condition` is used to specify the boolean condition controlling when a [\<kit-if>](#reference-html-tags-kit-if "<kit-if>") tag's template should be rendered.  
UI-KIT evaluates the value of this attribute as Javascript.

&nbsp;

---
#### data-kit-item-index-ref <span id="reference-html-attributes-data-kit-item-index-ref" /><sup><span style="font-size:8pt;">[top](#toc "table of contents") | [..^](#reference-html-attributes "attributes")</span></sup>
`data-kit-item-index-ref` contains a label that when prefixed with a hashtag can be used to reference the index of an item in the array being looped over in a [\<kit-array>](#reference-html-tags-kit-array "<kit-array>") tag.  
Reference attributes (including `data-kit-array-ref`, `data-kit-item-index-ref`, `data-kit-item-ref`, and `data-kit-model-ref`) may not have the same value as a reference attribute defined on a parent component element.  

&nbsp;

---
#### data-kit-item-ref <span id="reference-html-attributes-data-kit-item-ref" /><sup><span style="font-size:8pt;">[top](#toc "table of contents") | [..^](#reference-html-attributes "attributes")</span></sup>
`data-kit-item-ref` contains a label that when prefixed with a hashtag can be used to reference the item in the array being looped over in a [\<kit-array>](#reference-html-tags-kit-array "<kit-array>") tag.  
Reference attributes (including `data-kit-array-ref`, `data-kit-item-index-ref`, `data-kit-item-ref`, and `data-kit-model-ref`) may not have the same value as a reference attribute defined on a parent component element.  

&nbsp;

---
#### data-kit-model <span id="reference-html-attributes-data-kit-model" /><sup><span style="font-size:8pt;">[top](#toc "table of contents") | [..^](#reference-html-attributes "attributes")</span></sup>
`data-kit-model` is used to specify the model for a [\<kit-component>](#reference-html-tags-kit-component "<kit-component>") tag.  
UI-KIT evaluates the value of this attribute as Javascript.

&nbsp;

---
#### data-kit-model-input <span id="reference-html-attributes-data-kit-model-input" /><sup><span style="font-size:8pt;">[top](#toc "table of contents") | [..^](#reference-html-attributes "attributes")</span></sup>
`data-kit-model-input` is used to specify input passed to a model's `initialize()` method.  
See [KitComponent](#reference-javascript-kit-component "KitComponent") for more detail.  
UI-KIT evaluates the value of this attribute as Javascript.

&nbsp;

---
#### data-kit-model-ref <span id="reference-html-attributes-data-kit-model-ref" /><sup><span style="font-size:8pt;">[top](#toc "table of contents") | [..^](#reference-html-attributes "attributes")</span></sup>
`data-kit-model-ref` contains a label that when prefixed with a hashtag can be used to reference the model associated with a [\<kit-component>](#reference-html-tags-kit-component "<kit-component>") tag.  
Reference attributes (including `data-kit-array-ref`, `data-kit-item-index-ref`, `data-kit-item-ref`, and `data-kit-model-ref`) may not have the same value as a reference attribute defined on a parent component element.  

&nbsp;

---
#### data-kit-template-path <span id="reference-html-attributes-data-kit-template-path" /><sup><span style="font-size:8pt;">[top](#toc "table of contents") | [..^](#reference-html-attributes "attributes")</span></sup>  
`data-kit-template-path` is used to specify the path to an external html template for a [\<kit-component>](#reference-html-tags-kit-component "<kit-component>") tag.

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
> <kit-component data-kit-model="{ prop1: 'abc', prop2: 'def' }" data-kit-model-ref="myComponent">
>   <div>prop1 = %{#myComponent.prop1}%</div>
>   <div>
>     <button onclick="alert(`prop2 = ${#myComponent.prop2}`)">show prop2</button>
>   </div>
> </kit-component>
> ```

In the example above, setting the value of the `data-kit-model-ref` attribute to "myComponent" makes the model available to the html template as `#myComponent`.  

The following attributes provide object references using a hashtag prefix:
- [data-kit-array-ref](#reference-html-attributes-data-kit-array-ref "data-kit-array-ref attribute")
- [data-kit-item-index-ref](#reference-html-attributes-data-kit-item-index-ref "data-kit-item-index-ref attribute")
- [data-kit-item-ref](#reference-html-attributes-data-kit-item-ref "data-kit-item-ref attribute")
- [data-kit-model-ref](#reference-html-attributes-data-kit-model-ref "data-kit-model-ref attribute")

If needed, model references may be escaped by prefixing with a backslash.

> escaped model reference example:
> ```html
> <kit-component data-kit-model="{ prop1: 'abc', prop2: 'def' }" data-kit-model-ref="myComponent">
>   <div>prop1 = %{#myComponent.prop1}%</div>
>   <div>my reference to prop 1 is \#myComponent.prop1</div>
> </kit-component>
> <!-- renders: 
> <div>prop1 = abc</div>
> <div>my reference to prop 1 is #myComponent.prop1</div>
> -->
> ```

&nbsp;

## CSS reference <span id="reference-css" /><sup><span style="font-size:8pt;">[top](#toc "table of contents") | [..^](#reference-html "html reference")</span></sup>
There are no special css class names or rules specific to UI-KIT.  

But there is a convention that can be followed to scope css styles to a specific component so that everything having to do with a component can be found in one folder location.

> Example component folder structure:
> ```folder structure
> > my-component
>   - my-component.css
>   - my-component.html
>   - my-component.js
> ```

To scope css styles to a component, we can follow a convention of specifying a class on the top-most element in the template and referencing that class using the `@scope` attribute in the css file.

> Example component html file:
>
> ```html
> <div class="my-component">
>   <link rel="stylesheet" href="/components/my-component/my-component.css" />
>   <h2>My Component</h2>
>   <div class="my-class">My class content</div>
> </div>
> ```

> Example css file:
> ```css
> @scope (.my-component) {
>  :scope {
>    /* styles for the top-most element in the component (.my-component) */
>  }
>  .my-class {
>   /* styles for elements with class "my-class" (and that are also a descendant of .my-component) */
>  }
> }
> ```

> <span style="color:#FFD700;font-weight:bold;">◊</span> _Tip:_   
> _For components with an "inline" inner html template, UI-KIT first removes the inner html template from the document before processing the template for display. When the component is included directly in the markup for the index.html file (rather than the markup in a component template html file), 
> the component's template may be briefly displayed in the browser before being removed.
> To prevent this brief display, add the following rule to a global stylesheet._
> 
> Prevent template initial display of inline html templates:
> ```css
> kit-array:not([data-kit-component-id]),
> kit-component:not([data-kit-component-id]),
> kit-if:not([data-kit-component-id]) {
>     display: none;
> }
> ```

This rule hides the `<kit-array>`, `<kit-component>`, and `<kit-if>` tags that do not yet have a `data-kit-component-id` attribute.  
After UI-KIT has removed any inner html template from the document (and added a `data-kit-component-id` attribute), the component is displayed as expected.  

&nbsp;

## Javascript reference <span id="reference-javascript" /><sup><span style="font-size:8pt;">[top](#toc "table of contents") | [..^](#reference "reference")</span></sup>
The Javascript secion of the reference is divided into 2 sub-sections:
- [Working with models](#reference-javascript-working-with-models "working with models")
- [Framework classes](#reference-javascript-framework "framework classes")

&nbsp;

### Working with models <span id="reference-javascript-working-with-models" /><sup><span style="font-size:8pt;">[top](#toc "table of contents") | [..^](#reference-javascript "javascript reference")</span></sup>
There are two ways to provide a UI-KIT component with a model:
1. Pass a model to the component from its parent context using the `data-kit-model` attribute.
2. Implement a `createModel()` method in a Javascript module located in a file in the same folder and with the same name as the component's html template.

The first method works well in use scenarios where the parent context has all the information needed to create a model.  
The _Hello World_ example from the top of this document is a good example of the first method.

> Example of passing a model to a component using `data-kit-model`:
> ```html
> <kit-component data-kit-model="{ title: 'Hello UI-Kit' }" data-kit-model-ref="model">
>   <h1>%{#model.title}%</h1>
> </kit-component>
> ```

The example above uses the `data-kit-model` attribute to pass a model to the component and also uses the `data-kit-model-ref` attribute to provide a reference to the model that can be used in the component's html template:

The second method is useful when the model is more complex or when the model needs to be initialized with data from an external source.  
With this method, we use the `data-kit-template-path` attribute to specify the path to an external html template:

> Example of component markup using the `data-kit-template-path` attribute:
> ```html
> <kit-component data-kit-template-path="/components/my-component/my-component.html">
> </kit-component>
> ```

> <span style="color:#FFD700;font-weight:bold;">◊</span> _Note:_   
> _Within an external html template, the model reference is implicitly set as "model" and so the model can be referenced in the template using "#model"._

With the markup above, UI-KIT expects to find an HTML template file at the specified path *and* a Javascript file containing the component's model in the same folder and with the same name as the html template:

> Component folder structure:
> ```folder structure
> > my-component
>   - my-component.html
>   - my-component.js
> ```

UI-KIT will attempt to dynamically import the javascript file as a Javascript module. Within this module there are a few expectations specific to UI-KIT:  
- (Required) UI-KIT expects to find an exported `createModel()` function that returns the model for the component.
- (Optional) If the object returned by `createModel()` has an async method named `initialize()`, UI-KIT will call that method after the model is created.  
- (Optional) If the object returned by `createModel()` has an async method named `onLoadedInDocument()`, UI-KIT will call that method after the component's template has been processed and the resulting markup added to the document.  

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
>     async initialize(componentId) {
>         this.componentId = componentId;
>     }
> 
>     // optional
>     async onLoadedInDocument() {
>         const element = KitRenderer.getComponentElement(this.componentId);
>         alert(element.innerHTML);
>     }
> }
> ```

UI-KIT passes the unique id of the component as input to the `initialize()` method.  
The component's id can be useful in finding the component's element in the document.  
UI-KIT will also pass any input provided via the `data-kit-model-input` attribute to the `initialize()` method.

> Passing input to a component's model using the `data-kit-model-input` attribute:
> ```html
> <kit-component data-kit-template-path="/components/my-component/my-component.html" 
>                data-kit-model-input="{ prop1: 'abc', prop2: 'def' }">
>   <h1>%{#model.title}%</h1>
> </kit-component>
> ```
> ```javascript
> async initialize(componentId, modelInput) {
>   this.componentId = componentId;
>   this.prop1 = modelInput.prop1;
>   this.prop2 = modelInput.prop2;
> }
> ```

It is common for a component to re-render itself after a state change.  Pass `componentId` to the UI-KIT framework method `KitRenderer.renderComponent()` to re-render a component. Other useful UI-KIT framework methods include:
- `KitRenderer.renderDocument()` to re-render the entire document
- `KitNavigator.navigate()` to initiate navigation from Javascript code
- `KitMessenger.publish()` and `KitMessenger.subscribe()` to send and receive messages between components

See [Framework classes](#reference-javascript-framework "framework classes") below for additional information.

&nbsp;

### Framework classes <span id="reference-javascript-framework" /><sup><span style="font-size:8pt;">[top](#toc "table of contents") | [..^](#reference-javascript "javascript reference")</span></sup>
The items in this section document the capabilities of the UI-KIT framework classes:

- [KitComponent](#reference-javascript-framework-kit-component "KitComponent")
- [KitComponentOptions](#reference-javascript-framework-kit-component-options "KitComponentOptions")
- [KitComponentType](#reference-javascript-framework-kit-component-type "KitComponentType")
- [KitDependencyManager](#reference-javascript-framework-kit-dependency-manager "KitDependencyManager")
- [KitMessenger](#reference-javascript-framework-kit-messenger "KitMessenger")
- [KitMutationObserverFactory](#reference-javascript-framework-kit-mutation-observer-factory "KitMutationObserverFactory")
- [KitNavigator](#reference-javascript-framework-kit-navigator "KitNavigator")
- [KitRenderer](#reference-javascript-framework-kit-renderer "KitRenderer")
- [KitResourceManager](#reference-javascript-framework-kit-resource-manager "KitResourceManager")
- [KitStartup](#reference-javascript-framework-kit-startup "KitStartup")

&nbsp;

---
#### KitComponent <span id="reference-javascript-framework-kit-component" /><sup><span style="font-size:8pt;">[top](#toc "table of contents") | [..^](#reference-javascript-framework "framework classes")</span></sup>
`KitComponent` facilitates the mapping of html component elements to Javascript component models. UI-KIT creates a `KitComponent` instance for the `body` tag and each `<kit-array>`, `<kit-component>`, and `<kit-if>` tag in the document.

&nbsp;

##### Constructor

> ```javascript
> /** @param {KitComponentOptions} options */
> constructor(options)
> ```
> Creates a new instance of KitComponent based on the provided options.  
> See [KitComponentOptions](#reference-javascript-framework-kit-component-options "KitComponentOptions").  
> Auto-generates a value for the componentId property.

&nbsp;

##### Properties

> ```javascript
> /** @type {KitComponentType} */
> componentType;
> ```
>The type of component.  See [KitComponentType](#reference-javascript-framework-kit-component-type "KitComponentType").

&nbsp;

> ```javascript
> /** @type {number} */
> id;
> ```
> The auto-generated unique id for the component.

&nbsp;

> ```javascript
> /** @type {number} */
> index;
> ```
> When the component is a child of an array component, this is the index of the component in the array, otherwise it is null.

&nbsp;

> ```javascript
> /** @type {string} */
> indexRef;
> ```
> When the component is a child of an array component, this is the reference to the index of the component in the array, otherwise it is null.

&nbsp;

> ```javascript
> /** @type {string} */
> itemIndexRef;
> ```
> When the component is an array component, this is the reference to the index of the current item in the array, otherwise it is null.

&nbsp;

> ```javascript
> /** @type {string} */
> itemRef;
> ```
> When the component is an array component, this is the reference to the current item in the array, otherwise it is null.

&nbsp;

> ```javascript
> /** @type {any} */
> model;
> ```
> A javascript object that represents the component's state or data.

&nbsp;

> ```javascript
> /** @type {any} */
> modelInput;
> ```
> A javascript object to be passed as input to the component model's `initialize()` method.

&nbsp;

> ```javascript
> /** @type {string} */
> modelRef;
> ```
> The reference to the component's model in the html template.

&nbsp;

> ```javascript
> /** @type {KitComponent} */
> parent;
> ```
> The parent component of this component.

&nbsp;

> ```javascript
> /** @type {string} */
> template;
> ```
> The html template for the component.

&nbsp;

##### Methods

> ```javascript
> /** @param {KitComponent} component - The KitComponent to add */  
> static add(component)
> ```
> Adds a KitComponent to the global components array.

&nbsp;

> ```javascript
> /**
>   @param {number} id - The id of the KitComponent
>   @returns {KitComponent}
> */
> static find(id)
> ```
> Finds a KitComponent in the global components array by id.

&nbsp;

> ```javascript
> /** @param {number} id - The id of the KitComponent to be removed */  
> static remove(id)
> ```
> Removes a KitComponent from the global components array.

&nbsp;

---
#### KitComponentOptions <span id="reference-javascript-framework-kit-component-options" /><sup><span style="font-size:8pt;">[top](#toc "table of contents") | [..^](#reference-javascript-framework "framework classes")</span></sup>
`KitComponentOptions` encapsulates the options available when creating a KitComponent.  

&nbsp;

##### Properties

> ```javascript
> /** @type {KitComponentType} */
> componentType;
> ```
>The type of component.  See [KitComponentType](#reference-javascript-framework-kit-component-type "KitComponentType").

&nbsp;

> ```javascript
> /** @type {number} */
> index;
> ```
> When the component is a child of an array component, this is the index of the component in the array, otherwise it is null.

&nbsp;

> ```javascript
> /** @type {string} */
> indexRef;
> ```
> When the component is a child of an array component, this is the reference to the index of the component in the array, otherwise it is null.  
> Reference properties (including `indexRef`, `itemIndexRef`, `itemRef`, and `modelRef`) may not have the same value as a reference property defined on an ancestor component (via the parent property).  

&nbsp;

> ```javascript
> /** @type {string} */
> itemIndexRef;
> ```
> When the component is an array component, this is the reference to the index of the current item in the array, otherwise it is null.  
> Reference properties (including `indexRef`, `itemIndexRef`, `itemRef`, and `modelRef`) may not have the same value as a reference property defined on an ancestor component (via the parent property).  

&nbsp;

> ```javascript
> /** @type {string} */
> itemRef;
> ```
> When the component is an array component, this is the reference to the current item in the array, otherwise it is null.  
> Reference properties (including `indexRef`, `itemIndexRef`, `itemRef`, and `modelRef`) may not have the same value as a reference property defined on an ancestor component (via the parent property).  

&nbsp;

> ```javascript
> /** @type {any} */
> model;
> ```
> A javascript object that represents the component's state or data.

&nbsp;

> ```javascript
> /** @type {any} */
> modelInput;
> ```
> A javascript object to be passed as input to the component model's `initialize()` method.

&nbsp;

> ```javascript
> /** @type {string} */
> modelRef;
> ```
> The reference to the component's model in the html template.  
> Reference properties (including `indexRef`, `itemIndexRef`, `itemRef`, and `modelRef`) may not have the same value as a reference property defined on an ancestor component (via the parent property).  

&nbsp;

> ```javascript
> /** @type {KitComponent} */
> parent;
> ```
> The parent component.

&nbsp;

> ```javascript
> /** @type {string} */
> template;
> ```
> The html template for the component.

&nbsp;

---
#### KitComponentType <span id="reference-javascript-framework-kit-component-type" /><sup><span style="font-size:8pt;">[top](#toc "table of contents") | [..^](#reference-javascript-framework "framework classes")</span></sup>
`KitComponentType` is an enumeration of the types of components that can be created by UI-KIT:
- `"Component"`,
- `"ConditionalComponent"`,
- `"ArrayComponent"`

&nbsp;

---
#### KitDependencyManager <span id="reference-javascript-framework-kit-dependency-manager" /><sup><span style="font-size:8pt;">[top](#toc "table of contents") | [..^](#reference-javascript-framework "framework classes")</span></sup>
`KitDependencyManager` provides inversion of control support for objects with dependencies.
This class is used by UI-KIT to manage browser dependencies (such as the window and document objects) internally and is useful when unit testing applications using UI-KIT.

&nbsp;

##### Methods

&nbsp;

> ```javascript
> static clear()
> ```
> Remove all dependencies

&nbsp;

> ```javascript
> /**
>   @param {string} key - The dependency key used to find the dependency
>   @returns {any}
> */
> static get(key)
> ```
> Get a dependency

&nbsp;

> ```javascript
> /** @returns {Console} */
> static getConsole()
> ```
> Gets the console object

&nbsp;

> ```javascript
> /** @returns {Document} */
> static getDocument()
> ```
> Gets the document object

&nbsp;

> ```javascript
> /** @returns {KitMutationObserverFactory} */
> static getMutationObserverFactory() 
> ```
> Gets the mutation observer factory

&nbsp;

> ```javascript
> /** @returns {KitResourceManager} */
> static getResourceManager()
> ```
> Gets the resource manager

&nbsp;

> ```javascript
> /** @returns {Window} */
> static getWindow()
> ```
> Gets the window object

&nbsp;

> ```javascript
> /**
>   @param {string} key - The dependency key used to find the dependency
>   @param {any} value - The dependency
> */
> static set(key, value) 
> ```
> Sets a dependency

&nbsp;

> ```javascript
> /** @param {Console} consoleIn - The console */
> static setConsole(consoleIn)
> ```
> Sets the console object

&nbsp;

> ```javascript
> /** @param {Document} documentIn - The document */
> static setDocument(documentIn)
> ```
> Sets the document object

&nbsp;

> ```javascript
> /** @param {KitMutationObserverFactory} mutationObserverFactory - The mutation observer factory */
> static setMutationObserverFactory(mutationObserverFactory)
> ```
> Sets the mutation observer factory

&nbsp;

> ```javascript
> /** @param {KitResourceManager} resourceManager - The resource manager */
> static setResourceManager(resourceManager)
> ```
> Sets the resource manager

&nbsp;

> ```javascript
> /** @param {Window} windowIn - The window */
> static setWindow(windowIn)
> ```
> Sets the window object

&nbsp;

---
#### KitMessenger <span id="reference-javascript-framework-kit-messenger" /><sup><span style="font-size:8pt;">[top](#toc "table of contents") | [..^](#reference-javascript-framework "framework classes")</span></sup>
`KitMessenger` is used to send and receive messages between components.

> Example of subscribing to receive messages:
> ```javascript
> import { KitMessenger } from "../../ui-kit.js";
> 
> export function createModel() {
>     return new MyComponentModel();
> }
> 
> class MyComponentModel {
>   async initialize(componentId) {
>     this.componentId = componentId;
>     KitMessenger.subscribe("Topic1", this.componentId, this.onTopic1Message.name);
>   }
> 
>   onTopic1Message(msg) {
>     alert(msg);
>   }
> }
> ```

&nbsp;

##### Methods

&nbsp;

> ```javascript
> /**
>   @param {string} topicName - The name of the topic
>   @param {any} message - The message to be published
> */
> static publish(topicName, message)
> ```
> Publish a message to subscribers of a topic

&nbsp;

> ```javascript
> /**
>   @param {string} topicName - The name of the topic
>   @param {string} componentId - The id of the KitComponent subscriber
>   @param {string} callback- The name of the function receiving published messages
> */
> static subscribe(topicName, componentId, callback)
> ```
> Subscribe to receive messages published to a topic

&nbsp;

---
#### KitMutationObserverFactory <span id="reference-javascript-framework-kit-mutation-observer-factory" /><sup><span style="font-size:8pt;">[top](#toc "table of contents") | [..^](#reference-javascript-framework "framework classes")</span></sup>
`KitMutationObserverFactory` is a factory class for creating mutation observers.

&nbsp;

##### Methods

&nbsp;

> ```javascript
> /** 
>   @param {MutationCallback} callback
>   @returns {MutationObserver}
> */
> createMutationObserver(callback)
> ```
> Creates a new mutation observer

&nbsp;

---
#### KitNavigator <span id="reference-javascript-framework-kit-navigator" /><sup><span style="font-size:8pt;">[top](#toc "table of contents") | [..^](#reference-javascript-framework "framework classes")</span></sup>
`KitNavigator` facilitates navigation functionality.
This class uses [KitMessenger](#reference-javascript-framework-kit-messenger "KitMessenger") to publish navigation events.

> Example of subscribing to receive navigation messages:
> ```javascript
> import { KitMessenger, KitNavigator } from "../../ui-kit.js";
> 
> export function createModel() {
>     return new MyComponentModel();
> }
> 
> class MyComponentModel {
>   async initialize(componentId) {
>     this.componentId = componentId;
>     KitMessenger.subscribe(KitNavigator.navTopicName, this.componentId, this.onNavigation.name);
>   }
> 
>   onNavigation(url) {
>     alert(url);
>   }
> }
> ```

&nbsp;

##### Methods

&nbsp;

> ```javascript
> /** @returns {string} */
> static getCurrentUrlFragment()
> ```
> Gets the url fragment (or [hash](https://developer.mozilla.org/en-US/docs/Web/API/URL/hash "hash") property) from the current url.

&nbsp;

> ```javascript
> /** 
>   @param {string} url - The url to examine 
>   @returns {string}
> */
> static getUrlFragment(url)
> ```
> Gets the url fragment (or [hash](https://developer.mozilla.org/en-US/docs/Web/API/URL/hash "hash") property) from a url.

&nbsp;

> ```javascript
> static initialize()
> ```
> This method is called from [KitStartup](#reference-javascript-framework-kit-startup "KitStartup") to configure an application to generate navigation events by listening for browser `popstate` events.

&nbsp;

> ```javascript
> /** @param {string} url - The destination url */
> static navigate(url)
> ```
> Navigates to the specified url.

&nbsp;

---
#### KitRenderer <span id="reference-javascript-framework-kit-renderer" /><sup><span style="font-size:8pt;">[top](#toc "table of contents") | [..^](#reference-javascript-framework "framework classes")</span></sup>
`KitRenderer` is a Framework class used to render component html elements.

&nbsp;

##### Methods

&nbsp;

> ```javascript
> /**
>   @param {number} componentId - The id of the component
>   @returns {HTMLElement}
> */
> static getComponentElement(componentId)
> ```
> Gets the element associated with a component.

&nbsp;

> ```javascript
> /** @param {number} componentId -  The id of the component to render */
> static async renderComponent(componentId)
> ```
> Renders a component.

&nbsp;

> ```javascript
> static async renderDocument() {
> ```
> Renders the document body.

&nbsp;

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
#### KitStartup <span id="reference-javascript-framework-kit-startup" /><sup><span style="font-size:8pt;">[top](#toc "table of contents") | [..^](#reference-javascript-framework "framework classes")</span></sup>
`KitStartup` is a Framework class used to initialize a UI-KIT application.

&nbsp;

##### Methods

&nbsp;

> ```javascript
> static async initialize()
> ```
> This method initializes a UI-KIT application and is called when the browser [DOMContentLoaded](https://developer.mozilla.org/en-US/docs/Web/API/Document/DOMContentLoaded_event "DOMContentLoaded") event fires.

&nbsp;
