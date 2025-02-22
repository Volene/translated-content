---
title: CustomElementRegistry
slug: Web/API/CustomElementRegistry
tags:
  - API
  - CustomElementRegistry
  - Experimental
  - Interface
  - Landing
  - NeedsTranslation
  - Reference
  - TopicStub
  - Web Components
  - custom elements
translation_of: Web/API/CustomElementRegistry
---
{{DefaultAPISidebar("Web Components")}}

The **`CustomElementRegistry`** interface provides methods for registering custom elements and querying registered elements. To get an instance of it, use the {{domxref("window.customElements")}} property.

## Methods

- {{domxref("CustomElementRegistry.define()")}}
  - : Defines a new [custom element](/de/docs/Web/Web_Components/Custom_Elements).
- {{domxref("CustomElementRegistry.get()")}}
  - : Returns the constuctor for the named custom element, or `undefined` if the custom element is not defined.
- {{domxref("CustomElementRegistry.upgrade()")}}
  - : Upgrades a custom element directly, even before it is connected to its shadow root.
- {{domxref("CustomElementRegistry.whenDefined()")}}
  - : Returns an empty {{jsxref("Promise", "promise")}} that resolves when a custom element becomes defined with the given name. If such a custom element is already defined, the returned promise is immediately fulfilled.

## Examples

The following code is taken from our [word-count-web-component](https://github.com/mdn/web-components-examples/tree/master/word-count-web-component) example ([see it live also](https://mdn.github.io/web-components-examples/word-count-web-component/)). Note how we use the {{domxref("CustomElementRegistry.define()")}} method to define the custom element after creating its class.

```js
// Create a class for the element
class WordCount extends HTMLParagraphElement {
  constructor() {
    // Always call super first in constructor
    super();

    // count words in element's parent element
    var wcParent = this.parentNode;

    function countWords(node){
      var text = node.innerText || node.textContent
      return text.split(/\s+/g).length;
    }

    var count = 'Words: ' + countWords(wcParent);

    // Create a shadow root
    var shadow = this.attachShadow({mode: 'open'});

    // Create text node and add word count to it
    var text = document.createElement('span');
    text.textContent = count;

    // Append it to the shadow root
    shadow.appendChild(text);


    // Update count when element content changes
    setInterval(function() {
      var count = 'Words: ' + countWords(wcParent);
      text.textContent = count;
    }, 200)

  }
}

// Define the new element
customElements.define('word-count', WordCount, { extends: 'p' });
```

> **Note:** Note: The CustomElementRegistry is available through the {{domxref("Window.customElements")}} property.

## Specifications

| Specification                                                                                                                        | Status                           | Comment             |
| ------------------------------------------------------------------------------------------------------------------------------------ | -------------------------------- | ------------------- |
| {{SpecName("HTML WHATWG", "custom-elements.html#customelementregistry", "CustomElementRegistry")}} | {{Spec2("HTML WHATWG")}} | Initial definition. |

## Browser compatibility

{{Compat("api.CustomElementRegistry")}}
