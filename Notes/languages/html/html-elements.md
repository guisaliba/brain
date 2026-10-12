---
# Mandatory fields
id: "71f7d908-ed6e-4f9d-854a-e6817bdbfc99"
# Optional fields
title: "HTML Elements"
tags: []
source: ""
source_title: ""
source_description: ""
source_image_url: ""
created_date: "13-09-2023"
modified_date: "13-09-2023"
---
Anything that has to be done with the DOM has to essentially originate from a Document instance. In the context of a browser, this instance is the global document object; more on that later in this chapter.

Coming to HTML documents, HTML elements are represented by the HTMLElement class. Shown below is a brief overview of some of the HTML-specific classes in the DOM API:

Class	Purpose
HTMLElement ->	Represents an HTML element node.
HTMLHtmlElement ->	Represents the <html> element node.
HTMLHeadElement	 -> Represents the <head> element node.
HTMLBodyElement -> Represents the <body> element node.
HTMLDivElement -> Represents a <div> element node.
HTMLSpanElement ->	Represents a <span> element node.
HTMLParagraphElement ->	Represents a <p> element node.
HTMLFormElement ->	Represents a <form> element node.
HTMLInputElement-> 	Represents an <input> element node.
HTMLAudioElement ->	Represents an <audio> element node.
HTMLVideoElement ->	Represents a <video> element node.
...	...

Every node in a DOM tree is an instance of the class **Node**. The class Node inherits from the EventTarget class. All elements, represented by the **Element** class is also a Node. Text and comment nodes inherits from **Text** and **Comment** classes which turns to inherit both from the Node class, that's why they are nodes as well.

The main document is represented by the **HTMLDocument** class, which extends the **Document class**. And for every element in the document, we have the **HTMLElement** class from which all of the above mentioned classes inherits from. This father class extends the **Element** class which turns out to be a Node as well.

For example, the <head> tag is represented by the HTMLHeadElement class, which on its own extends the HTMLElement class (which extends Element, which extends Node. That's why they're all nodes in the DOM).

This structure is similar as writing something like:
```
class HTMLDocument : Document {
  class HTMLElement : HTMLDocument : Element {
    class HTMLHtmlElement : HTMLElement {}
    class HTMLHeadElement : HTMLElement {}
    class HTMLBodyElement : HTMLElement {}
     ...
  }
}
```