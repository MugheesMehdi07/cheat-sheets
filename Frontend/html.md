
# HTML Cheat Sheet

This cheat sheet offers a quick overview of the essential HTML elements and their usage, which is crucial for building web pages.

## Basic Structure

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document Title</title>
</head>
<body>
    <!-- Page content goes here -->
</body>
</html>
```

### Doctype Declaration

- `<!DOCTYPE html>`: Declares the document type and version of HTML.

### HTML Document Head

- `<head>`: Contains meta-information about the HTML document.
- `<title>`: Specifies the title of the document.
- `<meta>`: Specifies any metadata that cannot be defined by other HTML tags.

### HTML Document Body

- `<body>`: Contains the content of the HTML document.

## Essential Tags

### Text Formatting

- `<h1>` to `<h6>`: Header tags, `<h1>` being the most important, and `<h6>` the least.
- `<p>`: Defines a paragraph.
- `<br>`: Inserts a single line break.
- `<hr>`: Creates a horizontal line.
- `<strong>`: Makes text bold.
- `<em>`: Emphasizes text (typically italics).
- `<mark>`: Highlights text.

### Hyperlinks and Images

- `<a href="url">link text</a>`: Creates a hyperlink.
- `<img src="url" alt="alternative text">`: Embeds an image.

### Lists

- `<ul>`: Unordered list.
- `<ol>`: Ordered list.
- `<li>`: List item.

### Tables

```html
<table>
    <tr>
        <th>Header 1</th>
        <th>Header 2</th>
    </tr>
    <tr>
        <td>Data 1</td>
        <td>Data 2</td>
    </tr>
</table>
```

- `<table>`: Defines a table.
- `<tr>`: Table row.
- `<th>`: Table header.
- `<td>`: Table data cell.

### Forms

```html
<form action="submit_form.asp" method="post">
    <label for="name">Name:</label>
    <input type="text" id="name" name="name"><br><br>
    <input type="submit" value="Submit">
</form>
```

- `<form>`: Defines an HTML form for user input.
- `<label>`: Defines a label for an `<input>` element.
- `<input>`: Defines an input field.

## Attributes

- `class`: Specifies one or more classnames for an element (used by CSS and JavaScript).
- `id`: Specifies a unique id for an element.
- `src`: Specifies the source URL for media elements like `<img>`.
- `href`: Specifies the URL of a link.
- `alt`: Provides alternative text for an image.
- `style`: Specifies an inline CSS style for an element.

## Resources

- [MDN Web Docs: HTML](https://developer.mozilla.org/en-US/docs/Web/HTML)
- [W3Schools: HTML Tutorial](https://www.w3schools.com/html/)

This cheat sheet covers the basics of HTML. For comprehensive tutorials and more advanced topics, refer to the resources provided.
```

This cheat sheet covers the basic elements of HTML including structure, common tags, and attributes. You can expand it by adding more complex elements and attributes as needed to fit the needs of your repository's audience.
