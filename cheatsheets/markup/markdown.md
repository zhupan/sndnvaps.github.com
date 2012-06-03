---
layout: page
title: "Markdown Cheatsheet"
description: "A Markdown Cheatsheet"

---
{% include JB/setup %}

* [Block Elements](#block_elements)
  * [Paragraph](#paragraph)
  * [Manual Line Break](#manual_line_breaks)
  * [Headers](#headers)
  * [Bockquotes](#blockquotes)
  * [Lists](#lists)
  * [Preformatted Code Blocks](#preformatted_code_blocks)
  * [Horizontal Rule](#horizontal_rule)
* [Span Elements](#span_elements)
  * [Links](#links)
  * [Images](#images)
  * [Phrase Emphasis](#phrase_emphasis)
  * [Code Spans](#code_spans)
* [Miscellaneous](#miscellaneous)
  * [Backslash Escapes](#backslash_escapes)
  * [Automatic Links](#automatic_links)
* [References](#references)

## <a name="block_elements"></a>Block Elements

### <a name="paragraph"></a>Paragraph

To create a paragraph you just need a body of text with a single line break betwee them.

{% highlight text %}

Lorem ipsum occaecat pariatur esse culpa aliquip dolor exercitation culpa eiusmod sit irure in nulla aliquip. Lorem ipsum enim esse voluptate cupidatat incididunt exercitation nulla laborum cillum Ut eu sunt qui in occaecat fugiat ut dolor Ut pariatur sunt dolore occaecat adipisicing Ut nulla. 

Lorem ipsum occaecat pariatur esse culpa aliquip dolor exercitation culpa eiusmod sit irure in nulla aliquip. Lorem ipsum enim esse voluptate cupidatat incididunt exercitation nulla laborum cillum Ut eu sunt qui in occaecat fugiat ut dolor Ut pariatur sunt dolore occaecat adipisicing Ut nulla. 

{% endhighlight %}

---

### <a name="manual_line_breaks"></a>Manual Line Breaks

End a line with two or more spaces to perform a line break.

This is line one  
This is line two  

{% highlight text %}

This is line one  
This is line two 

{% endhighlight %}

---

### <a name="headers"></a>Headers

There are two different styles here setext-stle ("=" or "-") and the atx-style (closing #'s are optional) 

# Heading 1

{% highlight text %}
# Heading 1
# Heading 1 #

Heading 1
========= 
{% endhighlight %}

## Heading 2

{% highlight text %}
## Heading 2
## Heading 2 ##

Heading 2
---------
{% endhighlight %}

### Heading 3

{% highlight text %}
### Heading 3
### Heading 3 ###
{% endhighlight %}

#### Heading 4

{% highlight text %}
#### Heading 4
#### Heading 4 ####
{% endhighlight %}

##### Heading 5

{% highlight text %}
##### Heading 5
##### Heading 5 #####
{% endhighlight %}

###### Heading 6

{% highlight text %}
###### Heading 6
###### Heading 6 ######
{% endhighlight %}

---

### <a name="blockquotes"></a>Blockquotes

Blockquotes are done with using the greater than symbol (&gt;) infront of content.

> Greater than brackets
> are used for blockquotes.

>> Nested blockquote

> #### Headers in blockquotes
> 
> * Quote a list
> * etc.

{% highlight text %}

> Greater than brackets
> are used for blockquotes.

>> Nested

> #### Headers in blockquotes
> 
> * Quote a list
> * etc.

{% endhighlight %}

---

### <a name="lists"></a>Lists

Ordered, without paragraphs

1. foo
2. bar

{% highlight text %}

1. foo
2. bar

{% endhighlight %}

*Note*: Markdown will not change up the numbering of the ordered list. So no matter what number you start with the code will always be generated as follows:

{% highlight html %}

<ol>
  <li>Lorem ipsum dolor sit amet, consectetuer adipiscing elit.</li>
  <li>Aliquam tincidunt mauris eu risus.</li>
  <li>Vestibulum auctor dapibus neque.</li>
</ol>

{% endhighlight %}


Unordered, with paragraphs

* A list item.
  
  With a paragraph

  With another paragraph

* Another list item

{% highlight text %}

* A list item.
  
  With a paragraph

  With another paragraph

* Another list item

{% endhighlight %}

A nested example

* Foo
  * Bar
* Unordered with an ordered list
  1. Foo
  2. Bar
     * Unordered
  3. Zap
* Zap

{% highlight text %}

* Foo
  * Bar
* Unordered with an ordered list
  1. Foo
  2. Bar
     * Unordered
  3. Zap
* Zap

{% endhighlight %}

---

### <a name="preformatted_code_blocks"></a>Preformatted Code Blocks

Indent every line of a code block by at least 4 spaces or 1 tab.

    This is a preformatted
    code block.

{% highlight text %}

This is a normal paragraph

    This is a preformatted
    code block.

{% endhighlight %}

---

### <a name="horizontal_rule"></a>Horizontal Rule

{% highlight text %}

---

***

- - - -

{% endhighlight %}

---

## <a name="span_elements"></a>Span Elements

### <a name="links"></a>Links

These are basic uses of setting up links

{% highlight text %}

This is [an example](http://example.com "Titel") inline link.

[This Link](http://example.com) has no title attribute.

{% endhighlight %}

Referring to a local resource

{% highlight text %}

See my [About](/about/) page for details.

{% endhighlight %}

#### Reference Style links

Refrence style links are great when you need to re-use or want to organize you links for the given page.

{% highlight text %}

This is a reference [link][link]

This is how you would define the reference (normally at the bottom of the page)

[link]: http://example.com "Example Title"

So for basic reference:

Link: 
[Text to display][reference_id]

Reference: 
[reference_id]: url "title"

{% endhighlight %}

#### Anchor Reference

If you need to link to an anchor tag on the page add a standard `<a name="anchor_name"></a>` to the location you want anchored and then in the markdown url tag simply use a "#" with the name that was used in the `name` attibute of the anchor tag.

Example:

{% highlight text %}

[Text To Anchor](#anchor)

<a name="anchor"></a>Text To Anchor

{% endhighlight %}

---

### <a name="images"></a>Images

{% highlight text %}

![Alt text](/path/to/img.jpg)

![Alt text](/path/to/img.jpg "Optional title")

Reference Style:

![Alt Text][reference_id]

[reference_id]: url/to/image "optional title attribute"

{% endhighlight %}

---

### <a name="phrase_emphasis"></a>Phrase Emphasis

*Italic* **Bold**

{% highlight text %}

*italic* **bold**
_italic_ __bold__

{% endhighlight %}

---

### <a name="code_spans"></a>Code Spans

`Code spans` are delimeted by backticks (`). This is normally the first key on the left of the numbers row with the tildie (~) above it.

{% highlight text %}

`Code spans`

{% endhighlight %}

---

## <a name="miscellaneous"></a>Miscellaneous

### <a name="backslash_escapes"></a>Backslash Escapes

NOTE: This is taken from <http://daringfireball.net/projects/markdown/syntax#backslash>

Markdown allows you to use backslash escapes to generate literal characters which would otherwise have special meaning in Markdown’s formatting syntax. For example, if you wanted to surround a word with literal asterisks (instead of an HTML &lt;em&gt; tag), you can use backslashes before the asterisks, like this:

{% highlight text %}

\*literal asterisks\*

{% endhighlight %}

Markdown provides backslash escapes for the following characters:

{% highlight text %}

\   backslash
`   backtick
*   asterisk
_   underscore
{}  curly braces
[]  square brackets
()  parentheses
#   hash mark
+   plus sign
-   minus sign (hyphen)
.   dot
!   exclamation mark

{% endhighlight %}

---

### <a name="automatic_links"></a>Automatic Links

Automatic links are created by just wrapping a URL with &lt; & &gt; brackets

{% highlight text %}

<http://example.com>

{% endhighlight %}

The same can be done with email addresses:

{% highlight text %}

<nobody@nowhere.com>

Will generate something like this:

<a href="&#x6D;&#x61;i&#x6C;&#x74;&#x6F;:&#x61;&#x64;&#x64;&#x72;&#x65;&#115;&#115;&#64;&#101;&#120;&#x61;&#109;&#x70;&#x6C;e&#x2E;&#99;&#111;&#109;">&#x61;&#x64;&#x64;&#x72;&#x65;&#115;&#115;&#64;&#101;&#120;&#x61;&#109;&#x70;&#x6C;e&#x2E;&#99;&#111;&#109;</a>

{% endhighlight %}

---

## <a name="references"></a>References

The following are references used for developing this cheatsheet.

* [Official Markdown project at Daring Fireball](http://daringfireball.net/projects/markdown/syntax)
* [Official Wikipedia Page](http://en.wikipedia.org/wiki/Markdown)