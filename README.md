# draft-liquid2-spec

Development of a Liquid specification.

Discuss ideas with [GitHub discussions](https://github.com/liquid2-org/draft-liquid2-spec/discussions) or report [issues](https://github.com/liquid2-org/draft-liquid2-spec/issues) with the spec.

## Overview

This specification is under active development. If you’re already familiar with Liquid, here are some highlights of the changes Liquid2 introduces.

### Conditional expressions

Conditional expressions (those in `if` and `unless` tags, and in ternary expressions) support a logical `not` operator and grouping terms with parentheses. Unlike Shopify/Liquid, without parentheses, `and` binds more tightly than `or`.

### Variables

Every variable is a query following [RFC 9535](https://datatracker.ietf.org/doc/html/rfc9535) syntax and semantics (See [discussion](https://github.com/liquid2-org/draft-liquid2-spec/discussions/1)).

### Whitespace Control

In addition to `-` for trimming whitespace from preceding or trailing content, we add `+` and `~`. `+` explicitly retains all whitespace when in _auto trim mode_. `~` removes newlines, but keeps space and tab characters.

### Ternary expressions

`{% assign %}`, `{% echo %}` and the output statement support inline conditions. For example:

```
{{ foo if bar else baz }}
{{ foo | upcase if bar else baz || split }}
```

### Comments

The legacy comment tag is dropped in favour of a new comment syntax. Anything inside `{#` and `#}` is a comment. Additional `#`’s can be added to comment out blocks of markup that already contain comments, as long as the number of hashes match.

```
{# I'm a comment #}
```

```
{##
{# I'm a nested comment #}
{% assign foo = bar %}
##}
```

### String interpolation

As a shorthand for some uses of the `capture` tag, string literals support simple interpolation.

```
{% assign animal = "dog" -%}
{% assign speak = "woof" -%}
{% assign sentence = "The {{animal}} says {{ speak | upcase }}!" %}
```

### Template inheritance

`{% block %}` and `{% extends %}` tags are now standard. See [Python Liquid's definition](https://jg-rp.github.io/liquid/extra/tags#extends--block) for now.

### Arguments

Filter and tag named arguments can be separated by a `:` or `=`.

### Dropped tags

`{% tablerow %}` and `{% ifchanged %}` are no longer standard, but can be implemented as tag extensions.

### Dropped filters

All base64 filters are no longer standard.

## Note

These efforts are unofficial, with no affiliation to Shopify, the original authors of Liquid.

The style of this specification, both visual and in prose, is influenced by RFC's from the IETF, such as [RFC 9535]. This is not an IETF document nor is there any affiliation with the Internet Engineering Task Force.

## Thanks

Special thanks go to:

- Shopify and the developers at Shopify who authored [Shopify/Liquid](https://github.com/Shopify/liquid).
- The team behind [RFC 9535], on which this specification depends.
- [riggraz/no-style-please], who's Jekyll theme was adapted for this project's site.

[RFC 9535]: https://datatracker.ietf.org/doc/html/rfc9535
[riggraz/no-style-please]: https://github.com/riggraz/no-style-please
