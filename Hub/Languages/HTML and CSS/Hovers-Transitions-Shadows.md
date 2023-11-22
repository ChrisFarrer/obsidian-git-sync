---
Title: Hovers-Transitions-Shadows
Source: https://www.youtube.com/watch?v=G3e-cpL7ofc&t=1021s
Created: 2023-11-21 13:05
Modified: 2023-11-21 13:05
tags:
  - CSS
  - HTML
---
# Hovers, Transitions, Shadows

Having elements change upon hovering over them is a very common decorative effect used in professional websites. Below we'll illustrate how to create them with HTML/CSS code, building off of what we covered in [[HTML-CSS-Basics]].

## Hover Effects

In order to designate how an element reacts while being hovered over, you have to designate a separate block of CSS code. For example:
```
.subscribe-button:hover {
	CSS Code
}
```
In this case, the ":hover" after the class name is called a CSS Pseudo Class

### Common CSS Hover Properties

- Opacity
```
opacity: 0.7; <! Viewed as a percent out of 1, 70% opaque>
```



## Transitions

In order to smoothly transition between different pseudo classes and effects, we can use the transition CSS property.

```
transition: opacity 1s;
```

This takes in two values, the first being the attribute we want to transition, with the second being how long we want the transition to take. 

You can also add transitions to multiple properties in the same line separated by a comma:
```
transtion: opacity 0.2s, background-color 0.2s, color 0.2s;
```



## Shadows

Another effect is shadows. We can achieve a shadow effect using:
```
box-shadow: 0px 8px 10px rgba(0, 40, 67, 0.3)
```

This takes if four arguments:
1) The horizontal position of the shadow (negative values --> left | positive values --> right)
2) The vertical position of the shadow
	1) Unlike the first argument, where the pixel values treat the element as if moving about the origin, positive values indicate how far down you want the shadow.
3) Amount of blur 
4) The color of the shadow
	1) In this example we're using rgba, which is the same as rgb but with an additional indicator for opacity

## Common CSS Pseudo Classes

- hover
	- Changes the properties upon being hovered over
- active
	- Changes the properties upon being clicked on or "activated"





