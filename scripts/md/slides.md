body_class: core-fill
content_class: flexbox vcenter

<h2 class="faded"><em>Creating</em> elements</h2>

<aside class="note">
  <section>
    <p>We've talked a bit about using elements, now let's look at how you can create your own elements. Polymer is going to make this really easy for you!</p>
  </section>
</aside>

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
&lt;script src="<span alt="bower install polymer" data-tooltip="bower install polymer">platform.js</span>">&lt;/script>
&lt;link rel="import" href="<span alt="bower install polymer" data-tooltip="bower install polymer">polymer.html</span>">
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
&lt;script src="<span alt="bower install polymer" data-tooltip="bower install polymer">platform.js</span>">&lt;/script>
&lt;link rel="import" href="<span alt="bower install polymer" data-tooltip="bower install polymer">polymer.html</span>">
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
content_class: flexbox vcenter

<h2 class="faded"><em>Lifecycle</em> callbacks</h2>

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
content_class: flexbox vcenter

<h2 class="faded">Automatic <em>node finding</em></h2>

---

id: automatic-node-finding
title: Automatic Node Finding

<pre contenteditable class="prettyprint" style="font-size:25px; line-height: 1.2;" data-lang="HTML">
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

title: Time 4 Exercise!
body_class: fatunicorn
class: nobackdrop nobackground highlight

---

body_class: core-fill
content_class: flexbox vcenter

<h2 class="faded"><em>Binding</em> expressions</h2>

<aside class="note">
  <section>
    <p>To work with data in an element we use binding expressions</p>
  </section>
</aside>

---

id: two-way-binding
title: Binding Expressions

<pre class="prettyprint" style="font-size:27px; line-height: 1.2;" data-lang="HTML">
&lt;polymer-element name="owner-element"&gt;
  &lt;template&gt;
    &lt;h2&gt;<b>{{owner}}</b> built me with Polymer&lt;/h2&gt;
  &lt;/template&gt;
  &lt;script&gt;
  Polymer('owner-element', {
    <b>owner: 'Rob'</b>
  });
  &lt;/script&gt;
&lt;/polymer-element&gt;
</pre>

<pre class="prettyprint" style="font-size:30px; line-height: 1.2;" data-lang="HTML">
&lt;owner-element&gt;&lt;/owner-element&gt;
</pre>

<div class="component-demo">
  <output style="display: block; padding: 10px;">
    <owner-element></owner-element>
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
content_class: flexbox vcenter

<h2 class="faded"><em>Published</em> properties</h2>

<aside class="note">
  <section>
    <p>To do that we've created published properties</p>
  </section>
</aside>

---

id: published-properties
title: Published properties

<pre class="prettyprint" style="font-size:27px; line-height: 1.2;">
&lt;polymer-element name="owner-element" <b>attributes="owner"</b>&gt;
  &lt;template&gt;
    &lt;h2&gt;<b>{{owner}}</b> built me with Polymer&lt;/h2&gt;
  &lt;/template&gt;
  &lt;script&gt;
  Polymer('owner-element', {
    <b>owner: 'Rob'</b>
  });
  &lt;/script&gt;
&lt;/polymer-element&gt;
</pre>

<pre class="prettyprint" style="font-size:27px; line-height: 1.2;">
&lt;owner-element <b>owner="Alex"</b>&gt;&lt;/owner-element&gt;
</pre>

<div class="component-demo">
  <output style="display: block; padding: 10px;">
    <owner-element owner="Alex"></owner-element>
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

body_class: core-fill
content_class: flexbox vcenter

<h2 class="faded">Declarative <em>event bindings</em></h2>

<aside class="note">
  <section>
    <p>To quickly add interactivity we can use declarative event bindings</p>
  </section>
</aside>

---

id: declarative-event-bindings
title: Declarative Event Handlers

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
content_class: flexbox vcenter

<h2 class="faded">Changed <em>Watchers</em></h2>

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
        this.$.email.style.border = '1px solid silver';
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

id: polymerurl
class: nobackdrop nobackground yum do-transition
content_class: flexbox vcenter centered

<div class="build">
<h2><a href="http://polymer-project.org"><span class="elements">polymer</span><span class="hide">-</span><span class="core">project</span><span class="hide">.</span><span class="platform">org</span></a></h2>
</div>
