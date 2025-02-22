---
title: Range
slug: Web/API/Range
tags:
  - API
  - DOM
  - NeedsTranslation
  - TopicStub
translation_of: Web/API/Range
---
{{ APIRef("DOM") }}

The **`Range`** interface represents a fragment of a document that can contain nodes and parts of text nodes.

A range can be created using the {{ domxref("Document.createRange", "createRange()") }} method of the {{ domxref("Document") }} object. Range objects can also be retrieved by using the {{ domxref("Selection/getRangeAt", "getRangeAt()") }} method of the {{ domxref("Selection") }} object or the {{domxref("Document/caretRangeFromPoint", "caretRangeAtPoint()")}} method of the {{domxref("Document")}} object.

There also is the {{domxref("Range.Range()", "Range()")}} constructor available.

## Properties

_There are no inherited properties._

- {{domxref("Range.collapsed")}} {{readonlyInline}}
  - : Returns a {{domxref("Boolean")}} indicating whether the range's start and end points are at the same position.
- {{domxref("Range.commonAncestorContainer")}} {{readonlyInline}}
  - : Returns the deepest {{ domxref("Node") }} that contains the `startContainer` and `endContainer` nodes.
- {{domxref("Range.endContainer")}} {{readonlyInline}}
  - : Returns the {{ domxref("Node") }} within which the `Range` ends.
- {{domxref("Range.endOffset")}} {{readonlyInline}}
  - : Returns a number representing where in the `endContainer` the `Range` ends.
- {{domxref("Range.startContainer")}} {{readonlyInline}}
  - : Returns the {{ domxref("Node") }} within which the `Range` starts.
- {{domxref("Range.startOffset")}} {{readonlyInline}}
  - : Returns a number representing where in the `startContainer` the `Range` starts.

## Constructor

- {{ domxref("Range.Range()", "Range()") }} {{experimental_inline}}
  - : Returns a `Range` object with the global {{domxref("Document")}} as its start and end.

## Methods

_There are no inherited methods._

- {{ domxref("Range.setStart()")}}
  - : Sets the start position of a `Range`.
- {{ domxref("Range.setEnd()")}}
  - : Sets the end position of a `Range`.
- {{ domxref("Range.setStartBefore()")}}
  - : Sets the start position of a `Range` relative to another {{ domxref("Node") }}.
- {{ domxref("Range.setStartAfter()")}}
  - : Sets the start position of a `Range` relative to another {{ domxref("Node") }}.
- {{ domxref("Range.setEndBefore()")}}
  - : Sets the end position of a `Range` relative to another {{ domxref("Node") }}.
- {{ domxref("Range.setEndAfter()")}}
  - : Sets the end position of a `Range` relative to another {{ domxref("Node") }}.
- {{ domxref("Range.selectNode()")}}
  - : Sets the `Range` to contain the {{ domxref("Node") }} and its contents.
- {{ domxref("Range.selectNodeContents()")}}
  - : Sets the `Range` to contain the contents of a {{ domxref("Node") }}.
- {{ domxref("Range.collapse()")}}
  - : Collapses the `Range` to one of its boundary points.
- {{ domxref("Range.cloneContents()")}}
  - : Returns a {{ domxref("DocumentFragment") }} copying the nodes of a `Range`.
- {{ domxref("Range.deleteContents()")}}
  - : Removes the contents of a `Range` from the {{ domxref("Document") }}.
- {{ domxref("Range.extractContents()")}}
  - : Moves contents of a `Range` from the document tree into a {{ domxref("DocumentFragment") }}.
- {{ domxref("Range.insertNode()")}}
  - : Insert a {{ domxref("Node") }} at the start of a `Range`.
- {{ domxref("Range.surroundContents()")}}
  - : Moves content of a `Range` into a new {{ domxref("Node") }}.
- {{ domxref("Range.compareBoundaryPoints()")}}
  - : Compares the boundary points of the `Range` with another `Range`.
- {{ domxref("Range.cloneRange()")}}
  - : Returns a `Range` object with boundary points identical to the cloned `Range`.
- {{ domxref("Range.detach()")}}
  - : Releases the `Range` from use to improve performance.
- {{ domxref("Range.toString()")}}
  - : Returns the text of the `Range`.
- {{ domxref("Range.compareNode()")}} {{ Obsolete_inline }}{{non-standard_inline}}
  - : Returns a constant representing whether the {{domxref("Node")}} is before, after, inside, or surrounding the range.
- {{ domxref("Range.comparePoint()")}} {{experimental_inline}}
  - : Returns -1, 0, or 1 indicating whether the point occurs before, inside, or after the `Range`.
- {{ domxref("Range.createContextualFragment()")}}{{experimental_inline}}
  - : Returns a {{ domxref("DocumentFragment") }} created from a given string of code.
- {{ domxref("Range.getBoundingClientRect()") }} {{experimental_inline}}
  - : Returns a {{ domxref("DOMRect") }} object which bounds the entire contents of the `Range`; this would be the union of all the rectangles returned by {{ domxref("range.getClientRects()") }}.
- {{ domxref("Range.getClientRects()") }} {{experimental_inline}}
  - : Returns a list of {{ domxref("DOMRect") }} objects that aggregates the results of {{ domxref("Element.getClientRects()") }} for all the elements in the `Range`.
- {{ domxref("Range.intersectsNode()")}} {{experimental_inline}}
  - : Returns a `boolean` indicating whether the given node intersects the `Range`.
- {{ domxref("Range.isPointInRange()")}} {{experimental_inline}}
  - : Returns a `boolean` indicating whether the given point is in the `Range`.

## Specifications

| Specification                                                                                                        | Status                                       | Comment                                                                                                                                                                                                                               |
| -------------------------------------------------------------------------------------------------------------------- | -------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| {{SpecName('DOM WHATWG', '#interface-range', 'Range')}}                                             | {{Spec2('DOM WHATWG')}}             | Do not use `RangeException` anymore, use `DOMException` instead. Made the second parameter of `collapse()` optional. Added the methods `isPointInRange()`, `comparePoint()`, and `intersectsNode()`. Added the constructor `Range()`. |
| {{SpecName('DOM Parsing', '#extensions-to-the-range-interface', 'Extensions to Range')}} | {{Spec2('DOM Parsing')}}             | Added the method `createContextualFragment()`.                                                                                                                                                                                        |
| {{SpecName('CSSOM View', '#extensions-to-the-range-interface', 'Extensions to Range')}} | {{Spec2('CSSOM View')}}             | Added the methods `getClientRects()` and `getBoundingClientRect()`.                                                                                                                                                                   |
| {{SpecName('DOM2 Traversal_Range', 'ranges.html#Level-2-Range-Interface', 'Range')}}     | {{Spec2('DOM2 Traversal_Range')}} | Initial specification.                                                                                                                                                                                                                |

## Browser compatibility

{{Compat}}

\[1] Starting with Gecko 13.0 {{ geckoRelease("13.0") }} the `Range` object throws a {{ domxref("DOMException") }} as defined in DOM 4, instead of a `RangeException` defined in prior specifications.

\[2] Gecko supported it up to Gecko 1.9, then removed it until Gecko 17 where it was reimplemented, matching the spec.

## See also

- [The DOM interfaces index](/de/docs/DOM/DOM_Reference)
