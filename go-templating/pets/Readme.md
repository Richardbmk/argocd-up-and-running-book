# Go Templating Guide

Go templating is a powerful way to generate text output by combining templates with data. The `text/template` package provides this functionality.

## Basic Concepts

### 1. **Templates**

Templates are text files with placeholders and logic that get replaced with actual data when executed.

### 2. **Data Structures**

You define Go structs to pass data into your templates. For example:

```go
type Pet struct {
    Name   string
    Sex    string
    Intact bool
    Age    string
    Breed  string
}
```

### 3. **Template Syntax**

- `{{ .FieldName }}` - Access a field from your data struct
- `{{ range . }}` - Loop through a slice
- `{{ if condition }}` - Conditional execution
- `{{ end }}` - Close a block (range, if, etc.)
- `|` - Pipe operator to chain functions

## Key Features

### Variables

Access struct fields with the dot notation:

```
{{ .Name }}    // outputs the Name field
{{ .Age }}     // outputs the Age field
```

### Loops

Iterate over slices using `range`:

```
{{ range .Dogs }}
  Name: {{ .Name }}
{{ end }}
```

### Conditionals

Use `if` for conditional rendering:

```
{{ if .Intact }}
  Intact
{{ else }}
  Neutered/Spayed
{{ end }}
```

### Pipes and Custom Functions

Chain operations using the pipe operator and define custom functions:

```go
tmpl, err := template.New("file.tmpl").Funcs(template.FuncMap{
    "dec": func(i int) int {
        return i - 1
    },
}).ParseFiles("file.tmpl")
```

Then use in template:

```
{{ 5 | dec }}    // outputs 4
```

## Example: Pets Application

The `pets.go` example demonstrates:

- Defining a struct (`Pet`)
- Parsing a template file
- Executing the template with a slice of data
- Using custom template functions

## Learn More

For deeper understanding of these topics, check out:

- [How to Use Templates in Go](https://www.digitalocean.com/community/tutorials/how-to-use-templates-in-go)
- [Defining Structs in Go](https://www.digitalocean.com/community/tutorials/defining-structs-in-go)
- [Defining Methods in Go](https://www.digitalocean.com/community/tutorials/defining-methods-in-go)
