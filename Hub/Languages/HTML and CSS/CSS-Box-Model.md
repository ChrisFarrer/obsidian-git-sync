---
Title: CSS-Box-Model
Source: https://www.youtube.com/watch?v=G3e-cpL7ofc&t=1021s
Date: 2023-11-21
Created: 2023-11-21 20:54
tags:
  - CSS
  - HTML
  - CSS-Box-Model
---
# CSS Box Model

The CSS Box Model refers to the box that warps around every HTML element. It consists of content, padding, borders, and margins. Each of these play a fundamental role in the composition and spacing of websites. 

### Margin

- This adds spacing to the outside of our element
```
margin-right: 8px
```

We also touched on this topic in [[HTML-CSS-Basics]]

### Border

- Determines the size, shape, and style of the border between our element and the margin. 
```
border-style: dotted;
```

One common error is that after adding a border, an element might not align with those next to it. This is because the default border adds space to the outside of the element. To add an inner border, you can take advantage of the box-sizing property with an element that has it's height and width defined. 
```
    div {
        box-sizing: border-box;
        -moz-box-sizing: border-box;
        -webkit-box-sizing: border-box;
        width: 250px;
        height: 250px;
        border: 10px solid blue;
        background: yellow;
    }
```


### Padding

- Forms the spacing within our elements. Adding padding allows us to dynamically change the height and width of an element as the content changes size. Statically setting height and width without padding can result in content overflowing the element. 
```
padding-right: 30px;
```


## Graphics

![[box-model.png]]

