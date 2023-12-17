---
Title: Text-Styles
Source: https://www.youtube.com/watch?v=G3e-cpL7ofc&t=1021s
Date: 2023-11-22
Created: 2023-11-22 12:07
tags:
  - CSS
  - HTML
  - Text
---
# Changing Text with CSS

Many of us are familiar with Google Docs or Microsoft Word. When writing a paper, we often have to change the default font, size, style, alignment, or even color of our text. We can also change all of these attributes for text on a website using CSS. 

### Common Text Style Attributes

- font family
```
font-family: Arial;
```

- font size
```
font-size: 30px
```

- font weight
```
font-weight: bold;
```

- font style
```
font-style: italic;
```

- text alignment
```
text-align: center;
```

- line height - adjusts the vertical space between lines of text
```
line-height: 
```



### Special Characters

We can write out special characters by creating what's called an HTML Entity. The most common way of looking them up is simply googling their name followed by "HTML Entity", and copying and pasting the HTML code. 

For example, for a middle dot to appear in HTML, it looks like:
```html
<p>
This right here: &#183; is a middle dot;
</p>
```

### Paragraph Elements

Paragraph elements are one of the most commonly used HTML elements for adding body text to a website. By default text in them appears in Time New Roman font, and they come with margin as well. 


### Text Elements

Text elements allow us to change the style of text that's already inside of a paragraph or header element. For example, to bold just a portion of text, you can wrap it in a "strong" element such as:
```
This is some <strong>STRONG</strong> text
```

- strong - bolds a portion of text
```
<strong>bold text</strong>
```

- underline
```
<u>underlined text</u>
```

- span - doesn't include any default styles, most commonly used when adding a class as well.

```html
<p>
	Some cool awesome text with a <span class="link-text">link</span>
</p>
```

### CSS Specificity

CSS specificity is the algorithm used by browsers to determine which CSS declaration is most relevant to an element, which determines which property values are applied to the element. 

For example, if you set a style element for paragraphs elements such as:
```html
<style>
	p {
		margin-top: 0px;
		margin-bottom: 0px;
	}

	.body-text {
		margin-top: 10px;
		margin-bottom: 0px;
	}
</style>

<p class="body-text">
	Hello World!
</p>
```

The question is, which margin properties are applied to "Hello World"?
In this case, the class selector is more specific than the paragraph selector, thus the browser chooses to apply the class properties, and the text would receive 10px of margin on the top. 

### Special Cases

- Syntax vs Text Confusion
	- Lets say you want to add "<" or ">" into your HTML text. Sometimes, a browser might mistake these as HTML tags. In this case, you can use the HTML entity values instead to avoid browser confusion.
- 
