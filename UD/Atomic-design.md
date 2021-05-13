# Atomic Design

Atomic Design is a methodology seeking to provide direction on building interface design systems, if you've created a website it is easy to create one or two pages because it is easy to adapt the components to the needs, but eventually we have to add more pages and the more components you use, the more complex will have a consistent UI or mix components.

This used to happen because our web components depends on from others to work or be styled, instead of each component works individually to can be used everywhere.

## What is Atomic Design

Atomic Design is a methodology created by Brad Frost focused to create products with the premise of everything is a component and everything have works individually and together.

Also, when we create the UI, we need to define how will look the buttons to avoid use buttons who don't match with "website voice" or avoid same component had different styles 👇

![Inconsistent design](https://firebasestorage.googleapis.com/v0/b/web-projects-50e7e.appspot.com/o/images%2Fv2%2Fblogs%2Fatomic%20design%2Finconsistent%20design.jpg?alt=media&token=65794355-4efd-49c9-9f0d-d59587acaa34)

To do this, Brad use 5 concepts to create components using physic, biology and chemistry analogies.

## Atoms

In the whole universe atoms are the minimum unity of material and all material is composed by atoms.

In Atomic Design, atoms are the HTML elements (img, button, anchor, inputs, etc.) because all websites are composed by these elements.

Any HTML element and his variations like color, behavior, size, Shapes, etc. is considered as an atom.

To have a guideline you can use the Periodic table of the elements.

![Periodic Table of HTML elements](https://firebasestorage.googleapis.com/v0/b/web-projects-50e7e.appspot.com/o/images%2Fv2%2Fblogs%2Fatomic%20design%2FAtoms.png?alt=media&token=44aa629c-ece8-402b-afde-5a3b2482623e)

Just remember, some HTML elements can't be atoms because are used to build more complex components, the header for example:

Header used to have links, images, navigation bars, search bars.

## Molecules

In chemistry molecules are the union of 2 or more atoms.

In Atomic Design when you put together 2 or more atoms you're building a molecule, sometimes **molecules** should have functionalities.

Examples of molecules:

- Formularies.
- A simple Search bar.
- A card with photo and description.
- An ordered or unordered list.

## Organisms

In biology an organism is a set of material composed by molecules, for example the cells or mushrooms are considered organisms.

In Atomic Design, organisms are the union of atoms, molecules and other organisms:

- A Header with a search bar, a list of links and an image
- A Footer with a logo and the contact info

## Templates

In this point we stop using analogies, there are not needed because is easy to understand "templates" and "pages":

The most easy way to understand templates are: "Templates are sections", each sections is composed by atoms, molecules, organisms and sometimes other templates but contains a lot of info or handle a specific user interaction.

Templates examples:

- A chat bar

- The comments section

- The blog entries

- The company experience

## Pages

The description of pages is "Pages are the full UI built" is one of the pages for our website, at this point each component should work individually from other components and works together.

Each page is composed by 1 or more templates (sections) or other components, for example:

- About

- Blog

- Terms of service

- User info

## Atomic Design advantages:

In my experience, atomic design is so useful to create websites, literally allows me to create a new page less 4 minutes 👉 [Gists page](https://ulisessg.com/gist), I just needed to request the info and put it in component props.

Also Atomic Design is very useful when you are refactoring components (specially if you combine them with typescript) because you don't have to worry so much about if your new code will break the app or if re-styling the component you only have to change component styles once time.

If you want to learn more about **atomic design** I'll recommend you [the author blog](https://atomicdesign.bradfrost.com/).
