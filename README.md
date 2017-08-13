# Swagger vendor extensions in Mustache template

This repository explains how to access vendor extensions in a Mustache template on Swagger Codegen.


## How to implement Mustache

Add vendor extensions in the OpenAPI YAML.

```yaml
definitions:
  Pet:
    properties:
      code:
        type: string
        # vendor extension begins with x-
        x-validations:
          isbn13: true
```

Vendor extensions can be accessed in a template by the `vendorExtensions` property.

```mustache
  {{#vendorExtensions.x-validations.isbn13}}
    // Access vendor extensions in Mustache template
    @ISBN13
  {{/vendorExtensions.x-validations.isbn13}}
```


## Example

This repository contains an example of using vendor extensions.

Generate code.

```bash
./gradlew generateSwaggerCode
```

Then open `build/swagger-code/src/main/java/example/model/Pet.java`.

```java
public class Pet   {
    
  private Long id = null;

    
  private String name = null;

    @ISBN13
  private String code = null;

// snip...
```
