@title
The Hero Editor

@intro
Build a simple hero editor.

@description
## Setup to develop locally
Follow the [setup](guide/setup) instructions for creating a new project
named <ngio-ex path="angular-tour-of-heroes"></ngio-ex>.

The file structure should look like this:

<aio-filetree>

  <aio-folder>
    angular-tour-of-heroes
    <aio-folder>
      src
      <aio-folder>
        app
        <aio-file>
          app.component.ts
        </aio-file>


        <aio-file>
          app.module.ts
        </aio-file>


      </aio-folder>


      <aio-file>
        main.ts
      </aio-file>


      <aio-file>
        index.html
      </aio-file>


      <aio-file>
        styles.css
      </aio-file>


      <aio-file>
        systemjs.config.js
      </aio-file>


      <aio-file>
        tsconfig.json
      </aio-file>


    </aio-folder>


    <aio-file>
      node_modules ...
    </aio-file>


    <aio-file>
      package.json
    </aio-file>


  </aio-folder>


</aio-filetree>

When you're done with this page, the app should look like this <live-example></live-example>.


{@a keep-transpiling}
## Keep the app transpiling and running
Enter the following command in the terminal window:

<code-example language="sh" class="code-shell">
  npm start  
    
</code-example>

This command runs the TypeScript compiler in "watch mode", recompiling automatically when the code changes.
The command simultaneously launches the app in a browser and refreshes the browser when the code changes.

You can keep building the Tour of Heroes without pausing to recompile or refresh the browser.

## Show the hero
Add two properties to the `AppComponent`: a `title` property for the app name and a `hero` property
for a hero named "Windstorm."


<code-example path="toh-1/app/app.component.1.ts" region="app-component-1" linenums="false">

</code-example>

Now update the template in the `@Component` decorator with data bindings to these new properties.


<code-example path="toh-1/app/app.component.1.ts" region="show-hero" linenums="false">

</code-example>

The browser refreshes and displays the title and hero name.

The double curly braces are Angular's *interpolation binding* syntax.
These interpolation bindings present the component's `title` and `hero` property values,
as strings, inside the HTML header tags.


~~~ {.l-sub-section}

Read more about interpolation in the [Displaying Data](guide/displaying-data) page.


~~~

### Hero object

The hero needs more properties.
Convert the `hero` from a literal string to a class.

Create a `Hero` class with `id` and `name` properties.
Add these properties near the top of the `app.component.ts` file, just below the import statement.


<code-example path="toh-1/src/app/app.component.ts" region="hero-class-1" linenums="false">

</code-example>

In the `Hero` class, refactor the component's `hero` property to be of type `Hero`,
then initialize it with an `id` of `1` and the name `Windstorm`.


<code-example path="toh-1/src/app/app.component.ts" region="hero-property-1" linenums="false">

</code-example>

Because you changed the hero from a string to an object,
update the binding in the template to refer to the hero's `name` property.


<code-example path="toh-1/app/app.component.1.ts" region="show-hero-2">

</code-example>

The browser refreshes and continues to display the hero's name.

### Adding HTML with multi-line template strings

To show all of the hero's properties,
add a `<div>` for the hero's `id` property and another `<div>` for the hero's `name`.
To keep the template readable, place each `<div>` on its own line.

The backticks around the component template let you put the `<h1>`, `<h2>`, and `<div>` elements on their own lines,
thanks to the <i>template literals</i> feature in ES2015 and TypeScript. For more information, see
<a href="https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Template_literals" target="_blank" title="template literal">Template literals</a>.



<code-example path="toh-1/app/app.component.1.ts" region="multi-line-strings" linenums="false">

</code-example>


## Edit the hero name

Users should be able to edit the hero name in an `<input>` textbox.
The textbox should both _display_ the hero's `name` property
and _update_ that property as the user types.

You need a two-way binding between the `<input>` form element and the `hero.name` property.

### Two-way binding

Refactor the hero name in the template so it looks like this:

<code-example path="toh-1/app/app.component.1.ts" region="name-input" linenums="false">

</code-example>

`[(ngModel)]` is the Angular syntax to bind the `hero.name` property
to the textbox.
Data flow _in both directions_: from the property to the textbox;
and from the textbox back to the property.

Unfortunately, immediately after this change, the application breaks.
If you looked in the browser console, you'd see Angular complaining that
"`ngModel` ... isn't a known property of `input`."

Although `NgModel` is a valid Angular directive, it isn't available by default.
It belongs to the optional `FormsModule`.
You must opt-in to using that module.

### Import the _FormsModule_

Open the `app.module.ts` file and import the `FormsModule` symbol from the `@angular/forms` library.
Then add the `FormsModule` to the `@NgModule` metadata's `imports` array, which contains the list
of external modules that the app uses.

The updated `AppModule` looks like this:

<code-example path="toh-1/src/app/app.module.ts">

</code-example>



~~~ {.l-sub-section}

Read more about `FormsModule` and `ngModel` in the
[Two-way data binding with ngModel](guide/forms) section of the
[Forms](guide/forms) guide and the
[Two-way binding with NgModel](guide/template-syntax) section of the
[Template Syntax](guide/template-syntax) guide.


~~~

When the browser refreshes, the app should work again.
You can edit the hero's name and see the changes reflected immediately in the `<h2>` above the textbox.

## The road you've travelled
Take stock of what you've built.

* The Tour of Heroes app uses the double curly braces of interpolation (a type of one-way data binding)
to display the app title and properties of a `Hero` object.
* You wrote a multi-line template using ES2015's template literals to make the template readable.
* You added a two-way data binding to the `<input>` element
using the built-in `ngModel` directive. This binding both displays the hero's name and allows users to change it.
* The `ngModel` directive propagates changes to every other binding of the `hero.name`.

Your app should look like this <live-example></live-example>.

Here's the complete `app.component.ts` as it stands now:


<code-example path="toh-1/src/app/app.component.ts">

</code-example>


## The road ahead
In the [next tutorial page](tutorial/toh-pt2), you'll build on the Tour of Heroes app to display a list of heroes.
You'll also allow the user to select heroes and display their details.
You'll learn more about how to retrieve lists and bind them to the template.