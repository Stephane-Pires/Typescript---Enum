---
# try also 'default' to start simple
theme: unicorn
# random image from a curated Unsplash collection by Anthony
# like them? see https://unsplash.com/collections/94734566/slidev
background: https://source.unsplash.com/collection/94734566/1920x1080
# apply any windi css classes to the current slide
class: 'text-center'
# https://sli.dev/custom/highlighters.html
highlighter: shiki
# show line numbers in code blocks
lineNumbers: false
# some information about the slides, markdown enabled
info: |
  ## Slidev Starter Template
  Presentation slides for developers.

  Learn more at [Sli.dev](https://sli.dev)
# persist drawings in exports and build
drawings:
  persist: false
handle: 'Stéphane Pires'
# logoHeader: '/typescript-blue.png'
layout: intro
introImage: '/typescript-blue.png'
---

# Typescript - Enum

_What's the heck ?_

<div class="pt-12">
  <span @click="$slidev.nav.next" class="px-2 py-1 rounded cursor-pointer" hover="bg-white bg-opacity-10">
    Let's go <carbon:arrow-right class="inline"/>
  </span>
</div>

<div class="abs-br m-6 flex gap-2">
  <button @click="$slidev.nav.openInEditor()" title="Open in Editor" class="text-xl icon-btn opacity-50 !border-none !hover:text-white">
    <carbon:edit />
  </button>
  <a href="https://github.com/Stephane-Pires" target="_blank" alt="GitHub"
    class="text-xl icon-btn opacity-50 !border-none !hover:text-white">
    <carbon-logo-github />
  </a>
</div>

---
handle: 'Stéphane Pires'
logoHeader: '/typescript-blue.png'
layout: center
---

# What's the plan ?

Understand, why we are probably not going to use `enum` in Typescript to represent Enums 😅

---
handle: 'Stéphane Pires'
logoHeader: '/typescript-blue.png'
layout: center
---

# Represent the ingredients we have in a kitchen

---
handle: 'Stéphane Pires'
logoHeader: '/typescript-blue.png'
layout: center
---

# Default Enum

```ts {monaco}
enum Ingredients {
  Apple,
  Banana,
}

function sliceIngredients(ingredients: Ingredients) {
  return "Sliced It"
}

Ingredients[17] 
sliceIngredients(Ingredients.Banana)
sliceIngredients(12)
```

---
handle: 'Stéphane Pires'
logoHeader: '/typescript-blue.png'
layout: center
---

# Key takeaways

* Value inside the enum are "number" by default. 😕
* We can access value that doesn't exist and the typechecker doesn't complain 😡
* We can access enum value using two ways "string" value & "key" 😕


---
handle: Stéphane Pires
logoHeader: /typescript-blue.png
layout: center
---

# String Enum

```ts {monaco}
enum Ingredients {
  Apple = "Apple",
  Banana = "Banana",
}

function sliceIngredients(ingredients: Ingredients) {
  return "Sliced It"
}

Ingredients[17] 
sliceIngredients(Ingredients.Banana)
sliceIngredients('Apple')
```


---
handle: 'Stéphane Pires'
logoHeader: '/typescript-blue.png'
layout: center
---

# Key takeaways

* We get errors, when we try to access  key that doesn't belong to the enum. 😀
* End of the game, we won GG WP
* But... 

---
handle: 'Stéphane Pires'
logoHeader: '/typescript-blue.png'
layout: center
---

# Heterogenous Enum

```ts {monaco}
// Don't try this at home, it can be dangerous
enum Ingredients {
  Apple = "Apple",
  Banana = "Banana",
  Peach = 1,
}

function sliceIngredients(ingredients: Ingredients) {
  return "Sliced It"
}

Ingredients[17] 
sliceIngredients(Ingredients.Banana)
sliceIngredients(12)
// But there is worst...
```


---
handle: Stéphane Pires
logoHeader: /typescript-blue.png
layout: center
---

#  Heterogenous Enum (Iterable)

```ts {monaco}
enum Ingredients {
  Apple = "Apple",
  Banana = "Banana",
  Peach = 1,
}

// for (let ingredientString in IngredientString){
//   console.log('ingredientString', ingredientString)
// }
// Outputs =>
// Apple
// Banana

for (let ingredients in Ingredients){
  console.log('ingredients', ingredients)
// Outputs =>
// 1 😩
// Apple
// Banana
// Peach
```


---
handle: 'Stéphane Pires'
logoHeader: '/typescript-blue.png'
layout: center
---

# Key takeaways

* Adding a "number" value to the Enum fucked the whole enum 😡
* Typescript doesn't prevent heterogenous enum ?
* We can access value that doesn't exist and the typechecker doesn't complain 😡
* We can access enum value using two ways "string" value & "key" 😕

---
handle: Stéphane Pires
logoHeader: /typescript-blue.png
layout: center
---

# Const Heterogenous Enum

```ts {monaco}
const enum  Ingredients {
  Apple = "Apple",
  Banana = "Banana",
  Peach = 1,
}

function sliceIngredients(ingredients: Ingredients) {
  return "Sliced It"
}

Ingredients[17] 
sliceIngredients(Ingredients.Banana)
sliceIngredients(12)
```


---
handle: 'Stéphane Pires'
logoHeader: '/typescript-blue.png'
layout: center
---

# Key takeaways

* Still "broken" for functions relying on the Enums 😡
* We can't iterate on const Enums (Typescript does't create the javascript object due to an optimization) 😕


---
handle: Stéphane Pires
logoHeader: /typescript-blue.png
layout: center
---

# const "Enum" object as const

```ts {monaco}
const INGREDIENTS =  {
  Apple: "Apple",
  Banana: "Banana",
  Peach: 1
} as const // Uniquement "Valeur"

type TypeIngredients = typeof INGREDIENTS[keyof typeof INGREDIENTS]; // Uniquement "Type"

function sliceIngredients(ingredients: TypeIngredients) {
  return "Sliced It"
}

INGREDIENTS.Apple 
INGREDIENTS['ToupiMagique']
INGREDIENTS[17]

sliceIngredients(INGREDIENTS.Apple)
sliceIngredients(42)

```

<!--
// Voir pour brander les enums
-->

---
handle: Stéphane Pires
logoHeader: /typescript-blue.png
layout: center
---

# const "Enum" object as const (Iterable)

```ts {monaco}
const INGREDIENTS =  {
  Apple: "Apple",
  Banana: "Banana",
  Peach: 1
} as const 


for (let ingredient in INGREDIENTS){  
  console.log('ingredient', ingredient)
}
// Outputs =>
// Apple
// Banana
// Peach
```


---
handle: Stéphane Pires
logoHeader: /typescript-blue.png
layout: center
---

# Key takeaways

* `const MY_ENUM = {//...} as const` saved the game 😀
* But we have to  use a "weird" trick `type MyEnum = typeof MY_ENUM[keyof typeof MY_ENUM ]` 😕


---
handle: 'Stéphane Pires'
logoHeader: '/typescript-blue.png'
layout: center
---

# Make a choice !!

 String Enum (at your own risk) VS Magic Poney Trick `typeof X[keyof typeof X]` ?


---
handle: Stéphane Pires
logoHeader: /typescript-blue.png
layout: center
---

# Conclusion

* Use `const MY_ENUM = {//...} as const` to declare an Enum
* Use `type MyEnum = typeof MY_ENUM[keyof typeof MY_ENUM ]` to declare the type 
* By convention `MY_ENUM` is "Upper case"
* By convention `MyEnum` is "Capital camel case"
* Eslint (enum rules ?)


---
handle: Stéphane Pires
logoHeader: /typescript-blue.png
layout: center
---

# Next Step

* When to use [Branding](https://basarat.gitbook.io/typescript/main-1/nominaltyping#using-interfaces) & [Branding (TS Team)](https://github.com/Microsoft/TypeScript/blob/7b48a182c05ea4dea81bab73ecbbe9e013a79e99/src/compiler/types.ts#L693-L698)
* When to use CreateXXX ?
* How do we organize declaration of types ?
* Architecture of types ?


---
handle: 'Stéphane Pires'
logoHeader: '/typescript-blue.png'
layout: center
---

# Thanks you 

This presentation used : 

* [Slidev v0.33.0 (BETA)](https://sli.dev)
* [Unicorn Theme](https://github.com/dawntraoz/slidev-theme-unicorn)

___
