

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
>     <kit-component data-kit-model="{ title: 'Hello UI-Kit', isEasy: true,  howEasy: [ 'a', 'b', 'c' ] }"
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
> 
> <img src="data:image/png;base64, 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"/>

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

Let's start by creating a folder in your local file system to contain your web application.
You can name the folder anything you like.  I'll call mine "hello-ui-kit".  
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

If you are using IISExpress, once installed, open a command prompt and navigate to your application folder with the cd command:

> Navigate to your app folder:
>```cmd
>C:\>cd <path-to-your-app-folder-here>
>```

Then run the following command to start serving your application:

>Run IISExpress:
>```cmd
>"C:\Program Files (x86)\IIS Express\iisexpress" /path:%cd%\
>```

> <span style="color:gold;font-weight:bold;">◊</span> _Note:_   
> _The IISExpress command might be slightly different depending on where IISExpress was installed on your machine._

After running the command, you should see output in the command window that looks something like this:
>```cmd
>Starting IIS Express ...
>Successfully registered URL "http://localhost:8080/" for site "Development Web Site" application "/"
>```

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
> - index.html
> - ui-kit.js
>```

heading.html, navigation.html, and content.html are the templates for our new heading, navigation, and content components.
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
Replace the html inside the body tag of index.html with `<kit-component>` tags for each of our 3 components:

> index.html:
> ```html
> <kit-component data-kit-template-path="/components/heading/heading.html" data-kit-model="null"></kit-component>
> <kit-component data-kit-template-path="/components/navigation/navigation.html" data-kit-model="null"></kit-component>
> <kit-component data-kit-template-path="/components/content/content.html" data-kit-model="null"></kit-component>
> ```

`<kit-component>` is a custom html element (1 of 3) used by UI-KIT to define a component.

> <span style="color:gold;font-weight:bold;">◊</span> _Note:_  
> _Normally when we define a component with the data-kit-template-path attribute as above, UI-KIT expects to find a javascript module in a related location.  Since we're not covering javascript models yet in this Quick start step, we take a short cut by explicitly providing a (null) model using the data-kit-model attribute.  This isn't something you would do normally, but it's useful in this context._

After making these updates, refresh your browser.
You should now see a page with 3 headings: 
- "Hello UI-KIT!"
- "Navigation"
- "Content area".

> <span style="color:gold;font-weight:bold;">◊</span> _Note:_   
> _You may need to clear your browser's cache to see the changes.
> In Chrome, you can do this by first pressing F12 to open the developer tools, and then right-clicking the refresh button and selecting "Empty Cache and Hard Reload"._

This is a good start, but let's add some CSS styling so that each component's appearance better suits its function.   
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

> <span style="color:gold;font-weight:bold;">◊</span> _Note:_  
> _The @scope pseudo-class sets the scope for the contained css rules.
> Setting the scope to the id of the top element in the component's template limits the css rules to the heading component.
> Using this pattern helps to isolate the css rules for each component and makes the css easier to manage._

Now we need to add a reference to this css file in heading.html:

> heading.html:
> ```html
> <div>
>   <link rel="stylesheet" href="/components/heading/heading.css" />
>   <h2>Hello UI-KIT!</h2>
> </div>
> ```

We'll do something similar for the navigation component.  
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

And refer to this css file in navigation.html:

> navigation.html:
> ```html
> <div id="navigation">
>   <link rel="stylesheet" href="/components/navigation/navigation.css" />
>   <h2>Navigation panel</h2>
> </div>
> ```

This fixes the position of the navigation component to the left of the page and gives it a background.

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
> - index.html
> - ui-kit.js
>```

After saving your changes and refreshing your browser, you should see a page with clear content sections for heading, navigation, and content.

> Browser view:
> 
> ![Hello UI-Kit](data:image/png;base64,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)

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
> >     <kit-component data-kit-model="{ title: 'Hello UI-Kit', isEasy: true,  howEasy: [ 'a', 'b', 'c' ] }"
>                    data-kit-model-ref="model">
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

> <span style="color:gold;font-weight:bold;">◊</span> _Note:_  
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

First, undo the short-cut we took earlier by removing the `data-kit-model` attribute from the `<kit-component>` tag in index.html where the content component is referenced.

> `<kit-component>` tag in index.html for the content component:
> ```html
> <kit-component data-kit-template-path="/components/content/content.html"></kit-component>
> ```

When a component has the `data-kit-template-path` attribute and a model isn't specified using the `data-kit-model` attribute, UI-KIT expects to find a model in a Javascript file in the same folder and with the same name as the html template.  
So, if you create an html template at "/components/my-component/my-component.html", UI-KIT expects to find a javascript file at "/components/my-component/my-component.js".  
So now that we've taken out our `data-kit-model="null"` shortcut in index.html, UI-KIT expects a javascript file at "/components/content/content.js".  

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

> <span style="color:gold;font-weight:bold;">◊</span> _Note:_  
> _UI-KIT will also look for an optional `onLoadedInDocument()` method on the model.  If it exists, UI-KIT will call it after the component has been rendered in the document.  See  [Working with models](#reference-javascript-working-with-models "working with models") for more info._


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

The content component should now display:
- "Here is my content ..."
- and a button with the text "display component id"

Clicking the button demonstrates calling a function on the component's model and displays an alert with the text "my component id is: 4".

> <span style="color:gold;font-weight:bold;">◊</span> _Note:_  
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

First, in our content component model class, let's get rid of the "content" property we added earlier and add a "currentSection" property.    
For now, we'll hard-code currentSection's value to "#section1" within the `initialize()` method.

> content.js:
> ```javascript
> async initialize(componentId) {
>   this.myComponentId = componentId;
>   this.currentSection = "#section1";
> }
> ```

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

Refreshing the browser should now display "Section 1 content" only and not any of the other sections.  
The value of `data-kit-condition` is evaulated for each `<kit-if>` tag.  
The html inside each `<kit-if>` tag is only rendered if the condition is true.

&nbsp;  

---
## Step 5: Looping <span id="quick-start-5" /><sup><span style="font-size:8pt;">[top](#toc "table of contents") | [prev](#quick-start-4 "conditional rendering") | [next](#quick-start-6 "navigation")</span></sup>
---
The `<kit-array>` tag is used to loop over an array of items and render html content for each item in the array.  
In this step, we'll contrive to extend section 1 in the content component to use the `<kit-array>` tag.  

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
First, we're going to be calling some methods in the UI-KIT library so we'll need to add an import statement at the top of the file.

> import statement:
> ```javascript
> import { KitMessenger, KitNavigator, KitRenderer } from "../../ui-kit.js";
> ```

Second we need to add an `onNavigation()` method that will respond to navigation events and re-render the component:

> onNavigation() function:
> ```javascript
> onNavigation(url) {      
>   this.initialize(this.myComponentId);
> }
> ```

Finally, in the `initialize()` method, instead of hard-coding the current section value, we'll retrieve it from the current url.  We'll also call `KitMessenger.subscribe()` to start listening for navigation events.  

> `initialize()` method:
> ```javascript
> async initialize(componentId) {
>   this.myComponentId = componentId;
>   this.currentSection = KitNavigator.getCurrentUrlFragment();
>   KitMessenger.subscribe(KitNavigator.navTopicName, this.myComponentId, this.onNavigation.name);
> }
> ```

Our `KitMessenger.subscribe()` call tells UI-KIT to call the `onNavigation()` method whenever a navigation event occurs.



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

It's a pretty common scenario with web applications that it takes some time to get the data needed to fully present a component.  Often we need to load a file, query a database, or fetch data from an API over the internet, all of which takes some time.  To show our users that the data is on its way, it's common to initially show a loading indicator and then later, when the model changes state from not having data to having data, we update the view to show the requested data. In this step, we'll update the content component to initially display a loading indicator when section 1 data is requested and then transition to showing data.

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

I borrowed the css for this loader from [css-loaders.com](https://css-loaders.com/ "css-loaders.com"). It looks like it's designed to be used with a div element with class "loader".
So next, let's update the section 1 part of our content template to make use of our new css loading indicator.

> section 1 of content.html:
> ```html
> <kit-if data-kit-condition="#model.currentSection === '#section1' || !#model.currentSection">
>     <div>Section 1 content</div>
>     <kit-if data-kit-condition="#model.isSection1Loading">
>       <div style="margin:20px;" class="loader"></div>
>     </kit-if>
>     <kit-if data-kit-condition="!#model.isSection1Loading">
>       <ul>
>       <kit-array data-kit-array="#model.section1Items" data-kit-item-ref="item">
> 	      <li id="%{#item.itemId}%">Name: %{#item.name}%</li>
>       </kit-array>
>       </ul>
>     </kit-if>
>   </kit-if>
> ```

We've added our div with `class="loader"` for our loading indicator and wrapped in in a `<kit-if>` tag so that it is only displayed when `isSection1Loading` is true.
Also, we've wrapped the main content of section 1 in a `<kit-if>` tag so that it is only displayed when `isSection1Loading` is false, meaning it's done loading.
And note that we've changed from using the `getSection1Items()` method to using a `section1Items` property on the model to get our items array.

Finally, we have to update our model to go with these changes.  
We will remove our existing `getSection1Items()` method and instead add a `section1Items` property that gets set in the `initialize()` method.

> content.js:
> ```javascript
>     async initialize(componentId) {
>         this.myComponentId = componentId;
>         this.currentSection = KitNavigator.getCurrentUrlFragment();
>         KitMessenger.subscribe(KitNavigator.navTopicName, this.myComponentId, this.onNavigation.name);
> 
>         if (this.currentSection === "#section1") {
>           
>           // show state without data (loading)
>           this.section1Items = [];
>           this.isSection1Loading = true;
>           KitRenderer.renderComponent(this.myComponentId);
>           
>           // get data (simulating a 3-second delay)
>           await new Promise(r => setTimeout(r, 3000));
>           this.section1Items = [
>             { itemId: 1, name: "Item 1" },
>             { itemId: 2, name: "Item 2" },
>             { itemId: 3, name: "Item 3" },
>             { itemId: 4, name: "Item 4" },
>             { itemId: 5, name: "Item 5" }
>           ];
>           this.isSection1Loading = false;
>         }
>         
>         // synchronize view after state update
>         KitRenderer.renderComponent(this.myComponentId);
>     }
> ```

In the code above, we render the component in its initial (loading) state, get the data (with an artificial delay), and then render the component again after retrieving the data. Updating your browser should now show the loading indicator for 3 seconds before displaying the list of items in section 1.  
This completes the quick start guide.  I hope you like using UI-KIT.  For additional information see the [Reference](#reference "reference") section below.

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

> <span style="color:gold;font-weight:bold;">◊</span> _Note:_   
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

> <span style="color:gold;font-weight:bold;">◊</span> _Tip:_   
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

> <span style="color:gold;font-weight:bold;">◊</span> _Note:_   
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
