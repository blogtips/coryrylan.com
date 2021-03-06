---
layout: post
title:  Angular 2 ngFor syntax
description: A quick look into the new Angular 2 ngFor syntax.
keywords: Cory Rylan, Web, Angular 2, JavaScript, ng-repeat, ngFor
tags: angular2, angularjs, javascript
date: 2015-06-22
updated: 2016-07-31
demo: http://plnkr.co/edit/0s3qtC0TvHdiJLmz4H3m?p=preview
permalink: /blog/angular-2-ng-for-syntax
---

Angular 2 will contain many new changes and improvements over Angular 1.x This post will cover the new `ngFor`
syntax and a simple comparison of version 1 `ng-repeat` to version 2 `ngFor`. Note Angular 2 is still in development and the API's are actively changing.
At the writing of this post Angular 2 is at RC 1. To get an idea on the progress of the project check
out <a href="http://splintercode.github.io/is-angular-2-ready/" target="_blank">Is Angular 2 Ready?</a>

First we will take a look at a simple Angular 1.x repeater that displays the index of the repeated item and the item value.

<pre class="language-markup">
<code>
{% raw %}
&lt;!-- Angular 1.x --&gt;
&lt;ul&gt;
  &lt;li ng-repeat=&quot;item in items&quot;&gt;
    {{$index}} {{item}}
  &lt;/li&gt;
&lt;/ul&gt;
{% endraw %}
</code>
</pre>

Here is the new `ngFor` syntax.

<pre class="language-markup">
<code>
{% raw %}
&lt;!-- Angular 2.0 --&gt;
&lt;ul&gt;
  &lt;li *ngFor=&quot;let item of items; let i = index&quot;&gt;
    {{i}} {{item}}
  &lt;/li&gt;
&lt;/ul&gt;
{% endraw %}
</code>
</pre>

The new syntax has a couple of things to note. The first is `*ngFor`. The `*` is a shorthand for
using the new Angular 2 template syntax with the template tag. This is also called a structural Directive.
It is helpful to know that `*` is just a shorthand to explicitly defining the data bindings on a template tag.
The template tag prevents the browser from reading or executing the code within it.

<pre class="language-markup">
<code>
{% raw %}
&lt;!-- Angular 2.0 longhand ngFor --&gt;
&lt;template ngFor let-item=&quot;$implicit&quot; [ngForOf]=&quot;items&quot; let-i=&quot;index&quot;&gt;
  {{i}} {{item}}
&lt;/template&gt;
{% endraw %}
</code>
</pre>

So below is the typical syntax for an Angular 2 list.

<pre class="language-markup">
<code>
{% raw %}
&lt;ul&gt;
  &lt;li *ngFor=&quot;let item of items; let i = index&quot;&gt;
    {{i}} {{item}}
  &lt;/li&gt;
&lt;/ul&gt;
{% endraw %}
</code>
</pre>

Looking back at our `ngFor` the next interesting thing to note is `let item of items;`. The `let`
key is part of the Angular 2 template syntax. `let` creates a local variable that can be referenced anywhere in our template.
So in our case we are creating a local variable `let item`.

The `let i` creates a template local variable to get the index of the array. If you do not need access to the index in your list
the `ngFor` simply boils down to the following code.

<pre class="language-markup">
<code>
{% raw %}
&lt;ul&gt;
  &lt;li *ngFor=&quot;let item of items&quot;&gt;
    {{item}}
  &lt;/li&gt;
&lt;/ul&gt;
{% endraw %}
</code>
</pre>

One thing to note the camelCase syntax was introduced in <a href="https://github.com/angular/angular/blob/master/modules/angular2/docs/migration/kebab-case.md" target="_blank">Alpha 52</a>.
A new custom HTML parser was introduced that allowed camelCasing in templates to replace the kebab-case syntax.

## Track By
Angular 2 also includes the `trackBy` feature from Angular 1.x that allows performance improvements in our list rendering by tracking a unique identifier
on our list items.

<pre class="language-markup">
<code>
{% raw %}
&lt;ul&gt;
  &lt;li *ngFor=&quot; let item of items; trackBy:item.id;&quot;&gt;
    {{item}}
  &lt;/li&gt;
&lt;/ul&gt;
{% endraw %}
</code>
</pre>

The new angular syntax will allow Angular to work with native web components and gain the
benefits of using <a href="http://coryrylan.com/blog/introduction-to-web-components">Web Components</a>.
Angular 2 will bring many exciting improvements over angular 1 and will soon allow us to create even more scalable web applications.