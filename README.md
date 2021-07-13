# Frontend Mentor - Calculator app solution

This is a solution to the [Calculator app challenge on Frontend Mentor](https://www.frontendmentor.io/challenges/calculator-app-9lteq5N29). 

## Table of contents

- [Overview](#overview)
  - [The challenge](#the-challenge)
  - [Links](#links)
- [My process](#my-process)
  - [Built with](#built-with)
  - [What I learned](#what-i-learned)
- [Author](#author)
- [Acknowledgments](#acknowledgments)

## Overview

### The challenge

Users should be able to:

- See the size of the elements adjust based on their device's screen size
- Perform mathmatical operations like addition, subtraction, multiplication, and division
- Adjust the color theme based on their preference
- **Bonus**: Have their initial theme preference checked using `prefers-color-scheme` and have any additional changes saved in the browser


### Links

- Solution URL: https://github.com/esralpay/Calculator
- Live Site URL: https://reverent-goldwasser-0fb98d.netlify.app/

## My process

### Built with

- Semantic HTML5 markup
- CSS custom properties
- Flexbox
- CSS Grid
- Svelte

### What I learned

Some of my major learnings while working through this project. 


```html
usage of template string in html to be able to use dynamic css to the change the template of app.

<div class={ `main main${themeValue}`}>

and also i learned ranger slider

<div class="slidecontainer">
		<input type="range" on:change={updateTheme} min="1" max="3" value="1" class={`slider slider${themeValue}`} id="myRange">						
</div>
```
```css
how to use ranger slider attributes

.slider {
		-webkit-appearance: none;
		width: 100%;		
		height: 26px;
		border-radius: 12px;
		border: none;
		background: #242D44;
		outline: none;
		opacity: 1;
		-webkit-transition: .2s;
		transition: opacity .2s;
	}

	.slider::-webkit-slider-thumb {
		-webkit-appearance: none;
		appearance: none;
		width: 16px;
		height: 16px;
		border-radius: 50%;
		background: #D03F2F;
		cursor: pointer;
	}
	

```

## Author

- Frontend Mentor - [@esralpay](https://www.frontendmentor.io/profile/esralpay)


## Acknowledgments

Thanks for help Erdem ALPAY