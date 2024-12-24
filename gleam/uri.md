
## The big URI object

todo diagram here
- list all fields in the "uri" object
- label arrows pointing to a big string uri

This object is typically created with **`uri.parse`** from a raw string. It can also be constructed manually with the default constructor.

## Working with URI “roots” and “stems” 

**`uri.origin`** stringifies the *root* part of a uri, e.g. `http://example.com/path?foo#bar >>> http://example.com`

**`uri.merge`** makes a new uri, sourcing values from two inputs: a "root" uri (`example.com:9000`) and a "stem" uri (`/users/test?code=123`). 

## Encoding and Decoding URIs

Translate url-related strings into and out of more explicit types.

todo diagram here
- col one: the raw string components
- col two: the functions in pairs
 - uri.parse, uri.to_string
 - uri.parse_query, uri.query_to_string
 - uri.path_segments
 - uri.percent_decode, uri.percent_encode
- col three: the typed code components
- XX arrows go from the left, through the parse functions to the right
- XX another set of matched arrows return to the left
