---
title: Geolocation
slug: Web/API/Geolocation
tags:
  - API
  - Advanced
  - Geolocation API
  - Interface
  - NeedsTranslation
  - Reference
  - Secure context
  - TopicStub
translation_of: Web/API/Geolocation
---
{{securecontext_header}}{{APIRef("Geolocation API")}}

The **`Geolocation`** interface represents an object able to programmatically obtain the position of the device. It gives Web content access to the location of the device. This allows a Web site or app to offer customized results based on the user's location.

An object with this interface is obtained using the {{domxref("navigator.geolocation")}} property implemented by the {{domxref("Navigator")}} object.

> **Note:** For security reasons, when a web page tries to access location information, the user is notified and asked to grant permission. Be aware that each browser has its own policies and methods for requesting this permission.

## Properties

_The `Geolocation` interface neither implements, nor inherits any property._

## Methods

\__The `Geolocation` interface doesn't inherit any_ method\_.

- {{domxref("Geolocation.getCurrentPosition()")}} {{securecontext_inline}}
  - : Determines the device's current location and gives back a {{domxref("GeolocationPosition")}} object with the data.
- {{domxref("Geolocation.watchPosition()")}} {{securecontext_inline}}
  - : Returns a `long` value representing the newly established callback function to be invoked whenever the device location changes.
- {{domxref("Geolocation.clearWatch()")}} {{securecontext_inline}}
  - : Removes the particular handler previously installed using `watchPosition()`.

## Specifications

| Specification                                                            | Status                           | Comment                |
| ------------------------------------------------------------------------ | -------------------------------- | ---------------------- |
| {{SpecName('Geolocation', '#geolocation_interface')}} | {{Spec2('Geolocation')}} | Initial specification. |

## Browser compatibility

{{Compat("api.Geolocation")}}

## See also

- [Using geolocation](/de/docs/WebAPI/Using_geolocation)
