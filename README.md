# XML Isomorphic Markup Language (XIML)

An XML alternative that uses a more concise, bracket-free syntax with support for namespaces, attributes, and comments.

## Language Specification

### Basic Syntax

XIML is a markup language that represents hierarchical data without angle brackets. Instead, it uses braces `{}` for nesting and a pipe `|` delimiter for attributes. Every tag must have opening and closing braces.

### Tags and Nesting

Tags are written as identifiers followed by their content in braces. For tags with small content, the opening brace can be placed on the same line:

```ximl
title { My Document }
created { 2024-01-15 }
```

For more complex structures, the opening brace can be placed on a new line:

```ximl
tagname
{
  // content goes here
}
```

Empty tags still require braces:

```ximl
emptytag { }
```

### Attributes

Attributes are specified after a tag name, each on a new line with pipes forming a vertical line to the tag. There is no equals sign between attribute names and values—the value immediately follows the attribute name:

```ximl
tagname
| attrname attrvalue
| anothername anothervalue
{
  // content
}
```

### Namespaces

#### Default Namespace

To specify a default namespace for a tag, use the special attribute name `@`:

```ximl
root
| @ http://example.com/ns
{
  child { }
}
```

#### Prefixed Namespaces

To declare a namespace with a prefix, use `@prefixname` followed by the namespace URI:

```ximl
root
| @myprefix http://example.com/myns
{
  myprefix:child { }
}
```

### Comments

XIML supports C++ style comments:

- **Single-line comments**: `// comment text`
- **Multi-line comments**: `/* comment text */`

```ximl
// This is a single-line comment

/*
  This is a multi-line comment
  that spans several lines
*/

tagname
{
  // Another comment
}
```

### Complete Example

```ximl
root
| @ http://example.com/root
| @soap http://schemas.xmlsoap.org/soap/envelope/
{
  // Default namespace comments
  metadata
  | version 1.0
  | author John
  {
    title { My Document }
    created { 2024-01-15 }
  }

  /* Multi-line comment
     explaining a section */
  soap:body
  | id main-body
  {
    message
    | type greeting
    {
      text { Hello World }
    }
  }
}
```

This is equivalent to XML:

```xml
<?xml version="1.0"?>
<root xmlns="http://example.com/root" xmlns:soap="http://schemas.xmlsoap.org/soap/envelope/">
  <!-- Default namespace comments -->
  <metadata version="1.0" author="John">
    <title>My Document</title>
    <created>2024-01-15</created>
  </metadata>

  <!-- Multi-line comment
       explaining a section -->
  <soap:body id="main-body">
    <message type="greeting">
      <text>Hello World</text>
    </message>
  </soap:body>
</root>
```

## Key Features

- **No angle brackets**: Cleaner, more readable syntax
- **Flexible brace placement**: Braces can be on the same line for simple content or on new lines for complex structures
- **Pipe-aligned attributes**: Attributes aligned vertically with pipes for visual clarity, no equals signs
- **Namespace support**: Both default and prefixed namespaces
- **Comment support**: C++ style single-line and multi-line comments
- **XML-isomorphic**: Can be losslessly converted to and from XML
