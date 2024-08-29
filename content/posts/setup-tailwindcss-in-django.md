---
title: 'Setup Tailwindcss in Django'
description: "How to setup tailwindcss with Django"
date: 2024-01-27T15:48:23+03:00
readTime: true
math: true
showTags: false
---
I recently was working with django and I kinda wanted to still use tailwind in the world of python.

Now I'd never setup a django project from scratch before, I usually picked up from someone else. But this time I wasn't so lucky.


## 1. Install tailwindcss,

```sh
# at the root of your project

npm install -D tailwindcss
npx tailwindcss init
```

## 2. Configuring TaiwindCSS

Configure the `tailwind.config.js` to capture all your files with tailwind classes.

```js
/** @type {import('tailwindcss').Config} */
module.exports = {
    content: ["./templates/*.html", "./**/templates/*.html"],
    theme: {
        extend: {},
    },
}
```



## 3. Add TailwindCSS base classes

Create a `static` directory at the root of your project. This will be where
the base tailwindcss classes and *generated tailwind classes will be.

```css
/* `static/input.css` */
@tailwind base;
@tailwind components;
@tailwind utilities;
```

## 4. Update your base template
Find your base template. usually `base.html` in the templates directory at the root of your project.
Link it to the final location of the generated css.
```html
<!-- styles will be the name you put as the output location when you run tailwind -->

<link href="{% static 'styles.css' %}" rel="stylesheet">
```

## 5. Update Django settings

This is the crucial part, here we tell django to serve our `static` directory.

In your settings.py add the following at the very bottom
```py
# settings.py

# update, this plays nice.
import os
SITE_ROOT = os.path.dirname(os.path.dirname(os.path.realpath(__file__)))
STATICFILES_DIRS = (
  os.path.join(SITE_ROOT, 'static/'),
)


```


## 6. Run tailwindcss

You can do this by running `npx tailwindcss -i ./static/input.css -o ./static/styles.css --watch` in the terminal,
or, or you can add it to your `package.json` and run it with `npm run tailwind`


```json
"scripts": {
    "tailwind": "npx tailwindcss -i ./static/input.css -o ./static/styles.css --watch --minify"
  },
```
> `--minify` removes all the extra whitespaces from the generated css


> You can call the command whatever you like it doesn't have to be tailwind

