---
Title: HTML-CSS-Basics
Source: https://www.youtube.com/watch?v=G3e-cpL7ofc&t=3s
Date: 2023-11-20
Created: 2023-11-20 16:53
Modified: 2023-11-20 16:53
tags:
  - "#HTML"
  - CSS
---
# HTML & CSS Basics

A quick walkthrough of the very basics of HTML and CSS elements and attributes. Some additional basic topics such as hover effects, transitions, and shadows can be found at [[Hovers-Transitions-Shadows]]. 
## What is HTML?

- HTML stands for Hypertext Markup Language
- Gives instructions to a computer to create a website

### HTML Elements

- Buttons:
```html
<button>Hello</button>
```

- Paragraph:
```html
<p>some cool text</p>
```

- Anchor element:
```html
<a href="https://www.google.com">Link to Website</a>
```


### HTML Attributes

- href - Adds a destination or link to a website
```
href="https://www.google.com">Link to Website
```

- target - Changes where a link will be opened. By default it opens in the same page
```
target="\_blank" <! opens link in new tab>
```

- class - Lets us label HTML elements
```
class="subscribe-button"
```

When defining the style attributes for a class, you use a dot or period and then the class name, such as:
```html
.subscribe-button {
	background-color: red;
	color: white;
	cursor: pointer;
}
```


### Terminology

- Opening tags determine the type of element, and they're paired with a closing tag that starts with a slash.
	- For example, \<button> is an opening tag, and \</button> is a closing tag.
- HTML attributes modify how an element behaves
	- For example, for \<a href="google.com"> Link \</a>
		- The attribute name is "href"
		- The attribute value is "google.com"
	- You can add multiple elements to the same element. 
- Typically the spacing conventions look like:
```html
<button>
  Hello <! Indents are 2 spaces >
</button>
```
- Comments, as seen above, use \<! Comment \> 

## What is CSS?

CSS stands for Cascading Style Sheets
It's used to change the appearance of HTML elements

### CSS Basics

- In order to write CSS code in a HTML file, you must first create a style element
```html
<style>
  button {
	  background-color: red;
  }
</style>
```
- In this example, we specify which html element we want to modify, and which attribute we which to change. CSS comes with built-in basic colors such as "red"
	- The "button" specification is called a CSS Selector, which tell the computer which elements we're targeting
	- The "background-color" portion is called a CSS Property
	- Finally, the "red" is considered a CSS Value
- Similar to Java, CSS requires semi-colons to denote the end of code
- Pixels are a common measurement to denote how big to make elements

### CSS Properties

- Background color
```
background-color: red;
```

- Text color
```
color: white;
```

- Border
```
border: none;
```

- Height
```
height: 50px;
```

- Width
```
width: 100px
```

- Rounded corners
```
border-radius: 2px;
```

- Cursor options
```
cursor: pointer;
```

- Border style
```
border-style: solid;
```

- Border width
```
border-width: 1px;
```

- Margin
```
margin-direction
```
Margin is the space outside of the element. For example, margin-right: 10px; would allocate 10 pixels of space to the right of the element. 

- Bold font
```
font-weight: bold;
```
