title: First steps with Polymer

<div class="build">
  <div>
    <h3>1. Get the code - bower, zip, github, etc.</h3>
    <pre class="prettyprint">bower install --save Polymer/polymer</pre>
  </div>
  <div>
    <h3>2. Include platform.js</h3>
    <pre class="prettyprint">&lt;script src="platform.js"&gt;</pre>
  </div>
  <div>
    <h3>3. Import the polymer.html</h3>
    <pre class="prettyprint">&lt;link rel="polymer.html"&gt;</pre>
  </div>
  <div>
    <h3>4. Write your definition</h3>
    <pre class="prettyprint">&lt;polymer-element name="my-element"&gt;</pre>
  </div>
</div>

---

body_class: core-fill
content_class: flexbox vleft

<h2 class="faded" style="font-size: 54px;"><em>&lt;polymer-element&gt;</em> gives you an easy, <em>declarative</em> way to define your own <em>custom elements</em>.</h2>

---

hidden: true
id: creating-elements
title: Creating <label class="core">elements</label>
subtitle: <a href="http://www.polymer-project.org/polymer.html" class="nounderline">polymer-project.org/polymer.html</a>
class: nobackdrop nobackground segue core polymer-diagram
#content_class: flexbox vcenter
keep_content: true

<div id="blocks-3d" class="in" style="top: 10%;">
  <img id="native-3d" class="block-3d" src="./images/polymer/diagram/native.svg">
  <img id="platform-3d" class="block-3d" src="./images/polymer/diagram/platform.svg">
  <img id="polymer-3d" class="block-3d" src="./images/polymer/diagram/polymer.svg">
  <img id="elements-3d" class="block-3d" src="./images/polymer/diagram/elements.svg">
</div>

<aside class="note">
  <section>
    <p><b>Polymer is going to make this really easy for you</b></p>
  </section>
</aside>

---

hidden: true
body_class: core-fill
content_class: flexbox vcenter

<h2 class="faded"><em>Declarative</em> element registration</h2>

<aside class="note">
  <section>
    <p>The declarative syntax that Polymer enables makes it super simple to start defining your own tags.</p>
  </section>
</aside>

---

id: declarative-registration
title: Declarative registration
#subtitle: Declarative registration

<pre class="corner prettyprint">
&lt;script src="<span alt="bower install Polymer/polymer" data-tooltip="bower install Polymer/polymer">platform.js</span>">&lt;/script>
&lt;link rel="import" href="<span alt="bower install Polymer/polymer" data-tooltip="bower install Polymer/polymer">polymer.html</span>">
</pre>

<pre class="prettyprint" style="font-size:30px; line-height: 1.2;" data-lang="HTML">
&lt;polymer-element name="my-element" <b>noscript</b>&gt;
  &lt;template&gt;
    &lt;style&gt;h2 { color: orange; }&lt;/style&gt;
    &lt;h2&gt;Hello from my-element!&lt;/h2&gt;
  &lt;/template&gt;
&lt;/polymer-element&gt;
</pre>

<pre class="prettyprint" style="font-size:30px; line-height: 1.2;" data-lang="HTML">
&lt;my-element&gt;&lt;/my-element&gt;
</pre>

<div class="component-demo">
  <output style="display: block; padding: 10px;">
    <my-element></my-element>
  </output>
</div>

<aside class="note">
  <section>
    <p>This is a Polymer element definition. It's important to indicate that the name attribute must have a dash in it. That's to prevent future versions of HTML from stepping on your tag.</p>
    <p>Anything inside of the template will be stamped out when the parser sees your new tag</p>
    <p>Note that the style tag is *not* affecting the h2 at the top of the slide that says "Declarative Registration". That's because the styles are scoped by the Shadow DOM</p>
    <p>Mention noscript. That attribute tells Polymer that you're not including any JavaScript with your element.</p>
  </section>
</aside>

---

id: declarative-registration-proto
title: Declarative registration

<pre class="corner prettyprint">
&lt;script src="<span alt="bower install Polymer/polymer" data-tooltip="bower install Polymer/polymer">platform.js</span>">&lt;/script>
&lt;link rel="import" href="<span alt="bower install Polymer/polymer" data-tooltip="bower install Polymer/polymer">polymer.html</span>">
</pre>

<pre class="prettyprint" style="font-size:30px; line-height: 1.2;" data-lang="HTML">
&lt;polymer-element name="hello-element"&gt;
  &lt;template&gt;
    &lt;h2&gt;I can say hello&lt;/h2&gt;
  &lt;/template&gt;
  &lt;script&gt;
  Polymer('hello-element', {
    sayHello: function() { alert('Howdy folks!'); }
  });
  &lt;/script&gt;
&lt;/polymer-element&gt;
</pre>

<div class="component-demo">
  <output style="display: block; padding: 10px;">
    <hello-element></hello-element>
  </output>
</div>

<aside class="note">
  <section>
    <p>If you do want to include JavaScript with your element you can omit the noscript attribute and include a script tag that calls the Polymer constructor.</p>
    <p>The Polymer constructor requires that you pass in your element's name, and a protoyper object. Properties and methods that you add to this prototype object are available on every instance of your new tag.</p>
    <p>In this example I've added some code to the page that listens for click events and calls target.sayHello().  (click on the elements)</p>
    <p>So easy to create an API for your element... but I want to add some data to this thing!</p>
  </section>
</aside>

---

body_class: core-fill
content_class: flexbox vleft

<h2 class="faded" style="font-size: 54px;">The <em>polymer-ready</em> event will tell you when all elements are <em>upgraded</em> and <em>ready to use</em>.</h2>

---

title: Listening for polymer-ready

<pre class="prettyprint" style="font-size:27px; line-height: 1.2;" data-lang="HTML">
&lt;polymer-element name="x-foo"&gt;
  &lt;template&gt;...&lt;/template&gt;
  &lt;script&gt;
    Polymer('x-foo', {
      sayHello: function() {
        ...
      }
    });
  &lt;/script&gt;
&lt;/polymer-element&gt;
</pre>

<pre class="prettyprint" style="font-size:27px; line-height: 1.2;" data-lang="HTML">
&lt;script&gt;
  document.addEventListener('polymer-ready', function() {
    var foo = document.querySelector('x-foo').sayHello();
  });
&lt;/script&gt;
</pre>

---

title: Now you try!
body_class: stormtroopers
class: nobackdrop nobackground highlight

---

body_class: core-fill
content_class: flexbox vleft

<h2 class="faded" style="font-size: 54px;"><em>Lifecycle callbacks</em> allow you to <em>hook into</em> and <em>react</em> to major changes.</h2>

---

# title: Lifecycle explained
content_class: no-top-margin

<div class="build callback-list">
  <div>
    <pre class="prettyprint">created: function() {...}</pre>
    An instance of the element is created.
  </div>
  <div>
    <pre class="prettyprint">ready: function() {...}</pre>
    The &lt;polymer-element&gt; has been fully prepared (e.g. Shadow DOM created, property observers setup, event listeners attached, etc). <b>Preferred over created</b>.
  </div>
  <div>
    <pre class="prettyprint">attached: function() {...}</pre>
    An instance of the element was inserted into the DOM. Guaranteed to have a parent.
  </div>
  <div>
    <pre class="prettyprint">domReady: function() {...}</pre>
    The element’s initial set of children are guaranteed to exist.
  </div>
  <div>
    <pre class="prettyprint">detached: function() {...}</pre>
    An instance was removed from the DOM.
  </div>
  <div>
    <pre class="prettyprint">attributeChanged: function(attrName, oldVal, newVal) {...}</pre>
    An attribute was added, removed, or updated. <b>Prefer changed watchers, except for native attributes</b>
  </div>
</div>

---

id: lifecycle-callbacks
title: Lifecycle Callbacks

<pre class="prettyprint" style="font-size:25px; line-height: 1.2;" data-lang="HTML">
&lt;polymer-element name="fat-unicorn"&gt;
  &lt;template&gt;
    &lt;h1&gt;
      Hello, my name is: <b>&lt;span id="myName"&gt;&lt;/span&gt;</b>
    &lt;/h1&gt;
  &lt;/template&gt;
  &lt;script&gt;
    Polymer('fat-unicorn', {
      ready: function() {
        var myName = <b>this.shadowRoot.getElementById('myName');</b>
        myName.textContent = 'Fat Unicorn';
      }
    });
  &lt;/script&gt;
&lt;/polymer-element&gt;
</pre>

<div class="component-demo">
  <output style="display: block; padding: 10px;">
    <fat-unicorn></fat-unicornst>
  </output>
</div>

---

body_class: core-fill
content_class: flexbox vleft

<h2 class="faded" style="font-size: 54px;"><em>Automatic node finding</em> makes it easy to <em>query</em> for elements in your <em>Shadow DOM</em>.</h2>

---

id: automatic-node-finding
title: Automatic Node Finding

<pre class="prettyprint" style="font-size:25px; line-height: 1.2;" data-lang="HTML">
&lt;polymer-element name="fat-unicorn"&gt;
  &lt;template&gt;
    &lt;h1&gt;
      Hello, my name is: <b>&lt;span id="myName"&gt;&lt;/span&gt;</b>
    &lt;/h1&gt;
  &lt;/template&gt;
  &lt;script&gt;
    Polymer('fat-unicorn', {
      ready: function() {
        // this.$ selects anything with an id
        var myName = <b>this.$.myName</b>;
        myName.textContent = 'Fat Unicorn';
      }
    });
  &lt;/script&gt;
&lt;/polymer-element&gt;
</pre>

<div class="component-demo">
  <output style="display: block; padding: 10px;">
    <fat-unicorn></fat-unicornst>
  </output>
</div>

---

body_class: core-fill
content_class: flexbox vleft

<h2 class="faded" style="font-size: 54px;"><em>Binding expressions</em> cut down on <em>glue code</em> and keep your elements <em>tidy</em>.</h2>

---

title: Binding Expressions

<pre class="prettyprint" style="font-size:27px; line-height: 1.2;" data-lang="HTML">
&lt;polymer-element name="fat-unicorn"&gt;
  &lt;template&gt;
    &lt;h1&gt;Hello, my name is: <b>{{myName}}</b>&lt;/h1&gt;
  &lt;/template&gt;
  &lt;script&gt;
    Polymer('fat-unicorn', {
      <b>myName: 'Princess Omnomnomnom'</b>
    });
  &lt;/script&gt;
&lt;/polymer-element&gt;
</pre>

<pre class="prettyprint" style="font-size:30px; line-height: 1.2;" data-lang="HTML">
&lt;fat-unicorn&gt;&lt;/fat-unicorn&gt;
</pre>

<div class="component-demo">
  <output style="display: block; padding: 10px;">
    <fat-unicorn2></fat-unicorn2>
  </output>
</div>

<aside class="note">
  <section>
    <p>In this example we're using mustache syntax to bind the value owner in our template, to a property on our prototype.</p>
    <p>Press the 'h' key to focus the slide</p>
    <p>When this element renders, you'll see 'Rob built me with Polymer'.</p>
    <p>But elements are supposed to be configurable, so how do we let the user set the value of owner?</p>
  </section>
</aside>

---

body_class: core-fill
content_class: flexbox vleft

<h2 class="faded" style="font-size: 54px;">Create <em>two-way data bindings</em> using <em>published properties</em>.</h2>

---

id: published-properties
title: Published properties

<pre class="prettyprint" style="font-size:27px; line-height: 1.2;">
&lt;polymer-element name="fat-unicorn" <b>attributes="myName"</b>&gt;
  &lt;template&gt;
    &lt;h1&gt;Hello, my name is: <b>{{myName}}</b>&lt;/h1&gt;
  &lt;/template&gt;
  &lt;script&gt;
    Polymer('fat-unicorn', {
      <b>myName: 'Princess Omnomnomnom'</b>
    });
  &lt;/script&gt;
&lt;/polymer-element&gt;
</pre>

<pre class="prettyprint" style="font-size:27px; line-height: 1.2;">
&lt;fat-unicorn <b>myName="Butterchub"</b>&gt;&lt;/fat-unicorn&gt;
</pre>

<div class="component-demo">
  <output style="display: block; padding: 10px;">
    <fat-unicorn3 myName="Butterchub"></fat-unicorn3>
  </output>
</div>

<aside class="note">
  <section>
  <p>Notice the attributes attribute I've created at the end of my polymer-element. That allows me to expose the owner property from my prototype to the outside world.</p>
  <p>This property is now 2-way data bound</p>
  <p>Now when someone uses our tag they can configure owner and set it to 'Alex', which renders: 'Alex built me with Polymer'</p>
  <p>So we've got a bit of data in here, how about interactivity?</p>
  </section>
</aside>

---

title: Time 4 Exercise!
body_class: fatunicorn
class: nobackdrop nobackground highlight

---

body_class: core-fill
content_class: flexbox vleft

<h2 class="faded" style="font-size: 54px;"><em>Changed watchers</em> automatically fire whenever a <em>custom attribute</em> is <em>updated</em>.</h2>

---

id: changed-watchers
content_class: no-top-margin no-bold

<pre class="prettyprint" style="font-size:27px; line-height: 1.2;">
&lt;polymer-element name="email-field" <b>attributes="address"</b>&gt;
  &lt;template&gt;
    &lt;label for="email"&gt;Enter email:&lt;/label&gt;
    <b>&lt;input type="text" id="email" value="{{address}}"&gt;</b>
  &lt;/template&gt;
  &lt;script&gt;
    Polymer('email-field', {
      <b>addressChanged: function(oldVal, newVal) {
        if (newVal &amp;&amp; newVal.indexOf('@') != -1) {
          return this.$.email.style.border = '3px solid green';
        }
        ...
      }</b>
    });
  &lt;/script&gt;
&lt;/polymer-element&gt;
</pre>

<div class="component-demo">
  <output style="display: block; padding: 10px; zoom: 2;">
    <!-- prevent the slide deck from transitioning when we type -->
    <email-field class="disable-keyboard-events">
    </email-field>
  </output>
</div>

---

body_class: core-fill
content_class: flexbox vleft

<h2 class="faded" style="font-size: 54px;"><em>Declarative event bindings</em> handle <em>setting up</em> and <em>tearing down</em> event handlers.</h2>

---

id: declarative-event-bindings
title: Declarative Event Bindings

<pre class="prettyprint" style="font-size:27px; line-height: 1.2;">
&lt;polymer-element name="click-element"&gt;
  &lt;template&gt;
    <b>&lt;button on-click="{{setMessage}}"&gt;Click me&lt;/button&gt;</b>
    <b>&lt;span&gt;{{message}}&lt;/span&gt;</b>
  &lt;/template&gt;
  &lt;script&gt;
  Polymer('click-element', {
    <b>message: 'Waiting to be clicked...'</b>
    <b>setMessage: function() { this.message = 'I was clicked!' }</b>
  });
  &lt;/script&gt;
&lt;/polymer-element&gt;
</pre>

<div class="component-demo">
  <output style="display: block; padding: 10px; zoom: 2;">
    <click-element></click-element>
  </output>
</div>

<aside class="note">
  <section>
    <p>You can press h to focus the slide</p>
    <p>To add a bit of interactivity we can use a declarative event handler. Here we're using on-click (note, not onclick) to fire an action called setMessage any time our button is clicked.</p>
    <p>setMessage will change a property on our prototype called message, which will then update inside the binding in our template</p>
    <p>Explain why onclick is bad but on-click is awesome</p>
    <p>onclick is bad because it works in the global scope and uses eval. on-click is awesome because it only has access to your element, it automatically removes the event listener when your element leaves the DOM, and it uses polymer-gestures, a library which unifies mouse, touch and pointer events.</p>
  </section>
</aside>

---

body_class: core-fill
content_class: flexbox vleft

<h2 class="faded" style="font-size: 54px;"><em><a href="http://www.polymer-project.org/docs/polymer/template.html">Template bindings</a></em> allow you to <em>stamp out</em> bits of DOM based on <em>model data</em>.</h2>

---

title: Template Bindings

<pre class="prettyprint" style="font-size:27px; line-height: 1.2;">
&lt;polymer-element name="login-form"&gt;
  &lt;input type="text" placeholder="Username"&gt;
  &lt;input type="password" placeholder="Password"&gt;
  <b>&lt;template if="{{flash}}"&gt;
    &lt;div class="alert"&gt;{{flash}}&lt;/div&gt;
  &lt;/template&gt;</b>
  &lt;script&gt;
    Polymer('login-form', {
      <b>flash: 'Your session expired!'</b>
    });
  &lt;/script&gt;
&lt;/polymer-element&gt;
</pre>

<div class="component-demo">
  <output style="display: block; padding: 10px; zoom: 1.5;">
    <login-form></login-form>
  </output>
</div>

---

content_class: no-top-margin

<pre class="prettyprint" style="font-size:27px; line-height: 1.2;">
&lt;polymer-element name="dwarf-list"&gt;
  &lt;template&gt;
    &lt;ul&gt;
      <b>&lt;template repeat="{{dwarf in dwarves}}"&gt;
        &lt;li&gt;{{dwarf.name}}&lt;/li&gt;
      &lt;/template&gt;</b>
    &lt;/ul&gt;
  &lt;/template&gt;
  &lt;script&gt;
    Polymer('dwarf-list', {
      <b>dwarves: [{name: 'Sneezy'}, {name: 'Dopey'}, ...]</b>
    });
  &lt;/script&gt;
&lt;/polymer-element&gt;
</pre>

<div class="component-demo" style="padding: 0;">
  <output style="display: block; zoom: 1.5;">
    <dwarf-list></dwarf-list>
  </output>
</div>

---

title: Hang in there!
body_class: pukingrainbows
class: nobackdrop nobackground highlight

---

body_class: platform-fill
content_class: flexbox vleft

<h2 class="faded" style="font-size: 54px;"><em>Insertion points</em> invite content from the host element into the <em>Shadow DOM</em>.</h2>
<br>
<h2 class="faded" style="font-size: 54px;">Nodes that cross over are called <em>distributed nodes</em>.</h2>

---

title: Insertion Points

<pre class="prettyprint" style="font-size:27px; line-height: 1.2;">
&lt;polymer-element name="x-pokemon" noscript&gt;
  &lt;template&gt;
    <b>&lt;h1&gt;A wild &lt;content&gt;&lt;/content&gt; appeared!&lt;/h1&gt;</b>
  &lt;/template&gt;
&lt;/polymer-element&gt;
</pre>

<pre class="prettyprint" style="font-size:27px; line-height: 1.2;">
<b>&lt;x-pokemon&gt;Jigglypuff&lt;/x-pokemon&gt;</b>
</pre>

<div class="component-demo">
  <output style="display: block; padding: 10px; zoom: 1.5;">
    <x-pokemon>Jigglypuff</x-pokemon>
  </output>
</div>

---

body_class: platform-fill
content_class: flexbox vleft

<h2 class="faded" style="font-size: 54px;"><em>Specific content</em> can be targeted with the <em>select</em> attribute.</h2>

---

# title: Insertion Points
content_class: no-top-margin

<pre class="prettyprint" style="font-size:27px; line-height: 1.2;">
&lt;polymer-element name="user-info" noscript&gt;
  &lt;template&gt;
    &lt;h2&gt;Last Name: <b>&lt;content select=".last-name"&gt;</b>&lt;/content&gt;&lt;/h2&gt;
    &lt;h2&gt;First Name: <b>&lt;content select=".first-name"&gt;</b>&lt;/content&gt;&lt;/h2&gt;
    &lt;h2&gt;<b>&lt;content&gt;&lt;/content&gt;</b>&lt;/h2&gt;
  &lt;/template&gt;
&lt;/polymer-element&gt;
</pre>

<pre class="prettyprint" style="font-size:27px; line-height: 1.2;">
&lt;user-info&gt;
  Hello World
  &lt;span class="first-name"&gt;Rob&lt;/span&gt;
  &lt;span class="last-name"&gt;Dodson&lt;/span&gt;
&lt;/user-info&gt;
</pre>

<div class="component-demo">
  <output style="display: block; zoom: 1.2;">
    <user-info>
      Hello World
      <span class="first-name">Rob</span>
      <span class="last-name">Dodson</span>
    </user-info>
  </output>
</div>

---

body_class: platform-fill
content_class: flexbox vleft

<h2 class="faded" style="font-size: 54px;">You can <em>style distributed nodes</em> with the <em>::content</em> pseudo element.</h2>
<br>
<h2 class="faded" style="font-size: 54px;">Use the <em>polyfill-next-selector</em> to <em>shim support</em> for ::content in other browsers.</h2>

---

# title: Styling distributed nodes
content_class: no-top-margin

<pre class="prettyprint" style="font-size:27px; line-height: 1.2;">
&lt;polymer-element name="name-tag" noscript&gt;
  &lt;template&gt;
    &lt;style&gt;
      polyfill-next-selector { content: ':host > h2' }
      ::content h2 {
        font-family: sans-serif;
        color: green;
      }
    &lt;/style&gt;
    &lt;content select=".name"&gt;&lt;/content&gt;
  &lt;/template&gt;
&lt;/polymer-element&gt;
</pre>

<pre class="prettyprint" style="font-size:27px; line-height: 1.2;">
&lt;name-tag&gt;
  &lt;h2 class="name"&gt;Hi, I'm Rob Dodson&lt;/h2&gt;
&lt;/name-tag&gt;
</pre>

<div class="component-demo">
  <output style="display: block; padding: 10px;">
    <name-tag>
      <h2 class="name">Hi, I'm Rob Dodson</h2>
    </name-tag>
  </output>
</div>

<a style="display: inline-block; margin-top: 15px;" href="http://jsbin.com/monam/6/edit">Example JSBin</a>

---

body_class: platform-fill
content_class: flexbox vleft

<h2 class="faded" style="font-size: 54px;">To <em>access distributed content</em>, use the <em><a href="http://www.html5rocks.com/en/tutorials/webcomponents/shadowdom-301/#toc-getDistributedNodes">getDistributedNodes</a></em> method.</h2>

---

title: OK. Your turn to type!
body_class: colbertpizza
class: nobackdrop nobackground highlight

---

body_class: elements-fill
content_class: flexbox vleft

<h2 class="faded" style="font-size: 54px;">To target your <em>Shadow Host</em> for styling, use the new <em>:host</em>, <em>:host()</em>, and <em>:host-context()</em> pseudo-classes.</h2>

---

title: Styling Host

<pre class="prettyprint" style="font-size:27px; line-height: 1.2;">
&lt;polymer-element name="hai-element" noscript&gt;
  &lt;template&gt;
    &lt;style&gt;
      :host {
        display: inline-block;
        border: 5px solid red;
      }
    &lt;/style&gt;
    &lt;h1&gt;Oh hai!&lt;/h1&gt;
  &lt;/template&gt;
&lt;/polymer-element&gt;
</pre>

<div class="component-demo">
  <output style="display: block; padding: 10px; zoom: 1.5;">
    <hai-element></hai-element>
  </output>
</div>

---

# title: Styling Host
content_class: no-top-margin

<pre class="prettyprint" style="font-size:24px; line-height: 1.2;">
&lt;polymer-element name="hai-element" noscript&gt;
  &lt;template&gt;
    &lt;style&gt;
      :host {
        display: inline-block;
      }

      <b>:host(.bordered) {
        border: 5px solid red;
      }</b>
    &lt;/style&gt;
    &lt;h1&gt;Oh hai!&lt;/h1&gt;
  &lt;/template&gt;
&lt;/polymer-element&gt;
</pre>

<pre class="prettyprint" style="font-size:27px; line-height: 1.2;">
&lt;hai-element <b>class="bordered"</b>&gt;&lt;/hai-element&gt;
</pre>

<div class="component-demo">
  <output style="display: block; padding: 10px; zoom: 1.5;">
    <hai-element2 class="bordered"></hai-element2>
  </output>
</div>

---

# title: Styling Host Context
content_class: no-top-margin

<pre class="prettyprint" style="font-size:24px; line-height: 1.2;">
&lt;polymer-element name="smart-text" noscript&gt;
  &lt;template&gt;
    &lt;style&gt;
      :host-context(.shadow) ::content h1 {
        text-shadow: 10px 10px 10px #999;
      }
    &lt;/style&gt;
    &lt;content&gt;&lt;/content&gt;
  &lt;/template&gt;
&lt;/polymer-element&gt;
</pre>

<pre class="prettyprint" style="font-size:27px; line-height: 1.2;">
&lt;div class="shadow"&gt;
  &lt;smart-text&gt;
    &lt;h1&gt;Hello World&lt;/h1&gt;
  &lt;/smart-text&gt;
&lt;/div&gt;
</pre>

<div class="component-demo">
  <output style="display: block; padding: 10px; zoom: 1.5;">
    <div class="shadow">
      <smart-text>
        <h1>Hello World</h1>
      </smart-text>
    </div>
  </output>
</div>

---

body_class: elements-fill
content_class: flexbox vleft

<h2 class="faded" style="font-size: 54px;">To pierce <em>one level</em> of Shadow Trees use the <em>::shadow pseudo-element</em>.</h2>
<br>
<h2 class="faded" style="font-size: 54px;">To pierce <em>N levels</em> of Shadow Trees use the <em>/deep/ combinator</em>.</h2>

---

# title: Styling Host Context
content_class: no-top-margin

<pre class="prettyprint" style="font-size:24px; line-height: 1.2;">
&lt;polymer-element name="x-foo" noscript&gt;
  &lt;template&gt;
    <b>&lt;h1&gt;Hello from x-foo&lt;/h1&gt;</b>
  &lt;/template&gt;
&lt;/polymer-element&gt;
</pre>

<pre class="prettyprint" style="font-size:24px; line-height: 1.2;">
&lt;polymer-element name="x-bar" noscript&gt;
  &lt;template&gt;
    &lt;style&gt;
      <b>x-foo::shadow h1 {
        color: red;
      }</b>
    &lt;/style&gt;
    <b>&lt;x-foo&gt;&lt;/x-foo&gt;</b>
  &lt;/template&gt;
&lt;/polymer-element&gt;
</pre>

<div class="component-demo">
  <output style="display: block; padding: 10px; zoom: 1.5;">
    <x-bar></x-bar>
  </output>
</div>

---

# title: Styling Host Context
content_class: no-top-margin

<pre class="prettyprint" style="font-size:24px; line-height: 1.2;">
&lt;polymer-element name="x-baz" noscript&gt;
  &lt;template&gt;
    <b>&lt;x-foo&gt;&lt;/x-foo&gt;</b>
  &lt;/template&gt;
&lt;/polymer-element&gt;
</pre>

<pre class="prettyprint" style="font-size:24px; line-height: 1.2;">
&lt;polymer-element name="x-bar" noscript&gt;
  &lt;template&gt;
    <b>&lt;style&gt;
      x-baz /deep/ h1 {
        color: red;
      }
    &lt;/style&gt;</b>
    <b>&lt;x-baz&gt;&lt;/x-baz&gt;</b>
  &lt;/template&gt;
&lt;/polymer-element&gt;
</pre>

<div class="component-demo">
  <output style="display: block; padding: 10px; zoom: 1.5;">
    <x-bar2></x-bar2>
  </output>
</div>

---

content_class: no-top-margin

<div class="build callback-list">
  <div>
    <pre class="prettyprint">:host or :host()</pre>
    Selects a shadow host element. May contain additional identifiers in parenthesis.
  </div>
  <div>
    <pre class="prettyprint">:host-context()</pre>
    Selects a shadow host based on a matching parent element.
  </div>
  <div>
    <pre class="prettyprint">::shadow</pre>
    Selects shadow trees that are one level deep inside of an element. Will need to be combined with <code>shim-shadowdom</code> directive if used outside of a Polymer element.
  </div>
  <div>
    <pre class="prettyprint">/deep/</pre>
    Selects shadow trees that are N levels deep inside of an element. Will need to be combined with <code>shim-shadowdom</code> directive if used outside of a Polymer element.
  </div>
  <div>
    <pre class="prettyprint">::content</pre>
    Selects distributed nodes inside of an element. Needs to be paired with <code>polyfill-next-selector</code> for browsers that do not support the native selector.
  </div>
  <h3><a href="http://robdodson.me/blog/2014/04/10/shadow-dom-css-cheat-sheet/">Shadow DOM CSS Cheat Sheet</a></h3>
</div>

---

title: Yay! We're done!
body_class: cloudmoney
class: nobackdrop nobackground highlight

---

hidden: true
body_class: platform-fill
content_class: flexbox vleft

<h2 class="faded" style="font-size: 54px;"><em>External stylesheets</em> may be <em>opted-in</em> to the Shadow DOM polyfill by adding the <br><em>shim-shadowdom</em> attribute.</h2>

---

hidden: true
content_class: no-top-margin

<pre class="prettyprint" style="font-size:27px; line-height: 1.2;" data-lang="HTML">
&lt;style <b>shim-shadowdom</b>&gt;
  x-foo::shadow h1 {
    color: red;
  }
&lt;/style&gt;
</pre>

<pre class="prettyprint" style="font-size:27px; line-height: 1.2;" data-lang="HTML">
&lt;polymer-element name="x-foo" noscript&gt;
  &lt;template&gt;
    &lt;h1&gt;Hello from x-foo&lt;/h1&gt;
  &lt;/template&gt;
&lt;/polymer-element&gt;
</pre>

<pre class="prettyprint" style="font-size:27px; line-height: 1.2;" data-lang="HTML">
&lt;x-foo&gt;&lt;/x-foo&gt;
</pre>

<div class="component-demo">
  <style shim-shadowdom>
    x-foo::shadow h1 {
      color: red;
    }
  </style>
  <output style="display: block; padding: 10px;">
    <x-foo></x-foo>
  </output>
</div>

<a style="display: inline-block; margin-top: 15px;" href="http://jsbin.com/foyel/6/edit">Example JSBin</a>

---

hidden: true
id: more-complex-elements
title: Define an API
subtitle: complex elements require more juice...

<pre data-code-cycle class="prettyprint" data-lang="HTML" style="font-size:25px;line-height: 1.4;">
</pre>

<textarea selected>
<polymer-element name="my-input" noscript>
  <template>
    <input type="text" id="in" style="color: orange;">
  </template>
</polymer-element>
</textarea>
<textarea>
<polymer-element name="my-input">
  <template>
    <input type="text" id="in" style="color: orange;">
  </template>
  <script>Polymer('my-input');</script>
</polymer-element>
</textarea>
<textarea>
<polymer-element name="my-input">
  <template>
    <input type="text" id="in" style="color: orange;">
  </template>
  <script>
    Polymer('my-input', {
      get length() { return this.$.in.value.length; },
      ready: function() { ... }
    });
  </script>
</polymer-element>
</textarea>
<textarea>
&lt;polymer-element name="my-input">
  &lt;template>
    &lt;link rel="stylesheet" href="styles.css">
    &lt;input id="in" type="text">
  &lt;/template>
  &lt;script src="path/to/elements/myinput.js">&lt;/script>
&lt;/polymer-element>
</textarea>

- Properties/methods are added to `prototype`
- `this` refers to the element itself (e.g. `this.localName == "my-input"`)
- Can reference external scripts/stylesheets (e.g. CSP friendly)

<!-- <pre class="prettyprint" data-lang="HTML">
&lt;polymer-element name="my-input" constructor="MyInput">
  &lt;template>
    <b>&lt;link rel="stylesheet" href="styles.css"></b>
    &lt;input type="text">
  &lt;/template>
  <b>&lt;script src="path/to/elements/myinput.js">&lt;/script></b>
&lt;/polymer-element>
</pre> -->

---

hidden: true
title: Features in action
subtitle: responsive design...using DOM
#content_class: smaller 

<pre class="corner prettyprint">
&lt;script src="<span alt="bower install polymer" data-tooltip="bower install polymer">platform.js</span>">&lt;/script>
&lt;link rel="import" href="<span alt="bower install polymer-elements" data-tooltip="bower install polymer-elements">polymer-media-query.html</span>">
</pre>

<pre class="prettyprint" data-lang="html">
&lt;polymer-element name="responsive-layout" attributes="responsive">
  &lt;template>
    <b>&lt;polymer-media-query query="max-width:640px" queryMatches="{{isPhone}}">&lt;/...</b>
    &lt;template if="{{isPhone && responsive}}"> &lt;!-- Phone markup -->
      &lt;content>&lt;/content>
    &lt;/template>
    &lt;template if="{{!responsive}}"> &lt;!-- Non-responsive case -->
     ...
    &lt;/template>
  &lt;/template>
  &lt;script>Polymer('responsive-layout', {responsive: false});&lt;/script>
&lt;/polymer-element>
</pre>

<pre class="prettyprint" data-lang="User's HTML">
&lt;responsive-layout <b>responsive</b>>
  &lt;div>...&lt;/div>
&lt;/responsive-layout>
</pre>

---

hidden: true
id: the-platform
title: The <label class="platform">platform</label>
subtitle: <a href="http://www.polymer-project.org/docs/start/platform.html" class="nounderline">polymer-project.org/docs/start/platform</a>
class: nobackdrop nobackground segue platform polymer-diagram
#content_class: flexbox vcenter
keep_content: true

<div id="blocks-3d" class="in" style="top: 10%;">
  <img id="native-3d" class="block-3d" src="./images/polymer/diagram/native.svg">
  <img id="platform-3d" class="block-3d" src="./images/polymer/diagram/platform.svg">
  <img id="polymer-3d" class="block-3d" src="./images/polymer/diagram/polymer.svg">
  <img id="elements-3d" class="block-3d" src="./images/polymer/diagram/elements.svg">
</div>

---

hidden: true
body_class: platform-fill
content_class: flexbox vleft

<h2 class="faded" style="font-size: 54px;">The platform is a <em>layer of polyfills</em> that adds support for emerging standards, like <em>Web Components</em>, to all <em>modern browsers</em>.</h2>

---

hidden: true
id: platform-polyfills
title: Platform polyfills
subtitle: supporting new web technologies today
class: nobackdrop nobackground browser-support

<div class="flexbox">
  <h2>Templates</h2>
  <div class="browser-support-row">
    <div class="supported"><img src="images/logos/browsers/safari_logo.png"></div>
    <div class="supported"><img src="images/logos/browsers/ff_logo.png"></div>
    <div class="supported"><img src="images/logos/chrome_logo.png"></div>
    <div class="supported"><img src="images/logos/browsers/opera_logo.png"></div>
    <div><img src="images/logos/browsers/ie10_logo.png"></div>
  </div>
</div>

<div class="flexbox">
  <h2>HTML Imports</h2>
  <div class="browser-support-row">
    <div><img src="images/logos/browsers/safari_logo.png"></div>
    <div><img src="images/logos/browsers/ff_logo.png"></div>
    <div class="supported partial"><img src="images/logos/chrome_logo.png"></div>
    <div><img src="images/logos/browsers/opera_logo.png"></div>
    <div><img src="images/logos/browsers/ie10_logo.png"></div>
  </div>
</div>

<div class="flexbox">
  <h2>Custom Elements</h2>
  <div class="browser-support-row">
    <div><img src="images/logos/browsers/safari_logo.png"></div>
    <div class="supported partial"><img src="images/logos/browsers/ff_logo.png"></div>
    <div class="supported"><img src="images/logos/chrome_logo.png"></div>
    <div><img src="images/logos/browsers/opera_logo.png"></div>
    <div><img src="images/logos/browsers/ie10_logo.png"></div>
  </div>
</div>

<div class="flexbox">
  <h2>Shadow DOM</h2>
  <div class="browser-support-row">
    <div><img src="images/logos/browsers/safari_logo.png"></div>
    <div class="supported partial"><img src="images/logos/browsers/ff_logo.png"></div>
    <div class="supported"><img src="images/logos/chrome_logo.png"></div>
    <div class="supported"><img src="images/logos/browsers/opera_logo.png"></div>
    <div><img src="images/logos/browsers/ie10_logo.png"></div>
  </div>
</div>

<div class="build">
  <span id="polyfill-support-all"></span>
</div>

---

hidden: true
body_class: platform-fill
content_class: flexbox vleft

<h2 class="faded" style="font-size: 52px;">Additional features include <em>Mutation Observers</em>, <em>Pointer Events</em>, <em>Web Animations</em>, and much more.</h2>

---

hidden: true
id: evaporate-platform
class: polymer-diagram

<div id="blocks-3d">
  <img id="native-3d" class="block-3d" src="./images/polymer/diagram/native.svg">
  <img id="platform-3d" class="block-3d" src="./images/polymer/diagram/platform.svg">
  <img id="polymer-3d" class="block-3d" src="./images/polymer/diagram/polymer.svg">
  <img id="elements-3d" class="block-3d" src="./images/polymer/diagram/elements.svg">
</div>

<div class="diagram-explanations" style="margin-top: 250px;">
  <div class="diagram-explanation">
    <h3 style="font-size: 35px; line-height: 1.5;">As browsers implement the specifications supported by the platform, the need for this <br>layer <strong>decreases</strong>.</h3>
  </div>
  <div class="build">
    <div id="platform-shrink" class="diagram-explanation">
      <h3 style="font-size: 35px; line-height: 1.5;">...till eventually it's all <strong>gone</strong>.</h3>
    </div>
  </div>
</div>


---

hidden: true
id: polymerurl
class: nobackdrop nobackground yum do-transition
content_class: flexbox vcenter centered

<div class="build">
<h2><a href="http://polymer-project.org"><span class="elements">polymer</span><span class="hide">-</span><span class="core">project</span><span class="hide">.</span><span class="platform">org</span></a></h2>
</div>
