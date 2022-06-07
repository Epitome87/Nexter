# Nexter Project

My main goal with this website clone project is to utilize CSS Grid wherever possible.

The design of this website is done by Jonas Schmedtmann, but I am developing the HTML, SASS, and JavaScript completely independently. I may change up the design here and there, or the theme of the site in general. However, I admire the original design quite a bit, so straying from it may not be the best decision! In order to help strengthen my knowledge of more advanced CSS concepts, I will be documenting any discoveries and pain-points along the way.

## Initial Observations

There are three entire sections that change locations at different screen sizes: Sidebar, Header, and Realtors sections. Because the Sidebar, on mobile, takes up the entire height of the page, each and every other section is impacted by it. Thus, it makes sense for us to create a Grid container that will treat each Section as a Grid item.

Since no content really lives outside of all these major sections, we can make the `body` element the Grid container! Or we could simply wrap the entire content of the site in a container div.

### 1. Header Section

This section consists of 6 main elements:

1. Image logo
2. Sub-header
3. Header
4. CTA Button to "View Our Properties"
5. "Seen-On" text
6. "Seen-On" list of logos

The layout of this section does not change in any significant want from mobile to desktop. It appears the height is in some sort of percentage or viewport-based value, as it shrinks and grows as the browser does horizontally. This is quite common for sections that are "above the fold".

### 2. Realtors Section

This section appears simple, but due to how the overall page layout makes this section change, and how the elements within this section also change in various different ways, it may be deceptively challenging.

Two main elements make up this section:

1. A heading
2. A list of Realtor Components

The heading is always on the top and centered. The list of Realtor Components is mostly in a single column layout, with one small range of screen size presenting the list as a single row.

As the section itself is a Grid item, it also changes depending on the screen width. On mobile sizes, this section is found underneath the Header Section (this is when the Realtor List is a single row). From ~800px and onward, the section takes on a more vertical orientation, to the right of the Header (this is when the Realtor List is a single column).

### 3. Features Section

This section is a series of 6 card-like components. On mobile, they are arranged in a single column. On large desktops, they are arranged in a 3 column by 2 row layout. Between these two sizes, we can probably arrange the cards in a 2x3 layout. This type of layout makes this section a great candidate for CSS Grid.

<!-- ![Features - Mobile](Github%20Assets/Features%20Section%20-%20Mobile.png 'Features - Mobile')
![Features - Desktop](Github%20Assets/Features%20Section%20-%20Desktop.png 'Features - Desktop') -->
<!-- <img src="Github Assets/Features Section - Mobile.png" height="400px">
<img src="Github Assets/Features Section - Desktop.png" height="400px" width="700px"> -->

**Features - Card Components**

The Feature Cards that the above layout holds are rather basic card-like components. They are made up of three elements:

1. An icon
2. Heading
3. Paragraph

Normally I would probably just use Flex for this type of layout. But Grid is a perfectly fine approach as well.

**Potential Plan**

1. Create a simple Grid layout, using filled-in div elements as the children rather than fully-developed Feature Cards
   - Ensure it's a single column on mobile
   - Ensure it reaches 3 columns on desktop
   - Ensure it adjusts appropriately between mobile and desktop
   - Ensure each grid item take up equal width and heights as one another
2. Slowly develop the complexity of each grid item
   - Make each card a Grid container, 2x2
   - Top left cell holds the icon. This grid item should not grow as the container does
   - Top right cell holds the heading. Should grow with the container
   - Bottom right cell holds the paragraph. Should grow with the container

### 4a. Story Section - Content

We can probably combine the content and image portions of the "Story" section into one. But to simplify the logic, I will treat each portion as its own section. Together, they lay vertically together on mobile sizes (with the content coming first), and eventually are displayed horizontally (with the images coming first).

The content portion of the Story section is made up of 4 main elements:

1. Sub-header
2. Header
3. Paragraph
4. CTA Button to "Find your own home"

### 4b. Story Section - Images

The image portion of the STory section is made up of 3 images. One image takes up the entire area, while the other two lay on top of it -- overlapping one another.

If it weren't for the challenge of using CSS Grid when possible, I would normally just slap a background image onto this section, and absolutely position two images on top of it. But that would be too easy, wouldn't it? So I will try to use the fact that multiple Grid items can occupy the same cell to my advantage!

**Challenges**

At larger sizes, one of the overlaid images should spill out of its own section and into the content section. I'm not quite sure how this will be achieved if the images are to be Grid items inside a container that does not extend out into the content section.

### 5. Homes Section

This section is very similar to the Features section. It consists of a series of 6 card-like components. On mobile, they are arranged in a single column. On large desktops, they are arranged in a 3 column by 2 row layout. Between the two sizes, we can probably arrange the cards in a 2x3 layout. This type of layout, again, makes this section a great candidate for CSS Grid!

**Homes - Card Components**

The Home Cards are much more complex than the Feature Cards. They appear to consist of 4 main elements and some sub-elements:

1. An image of the house being advertised
2. A label with a descriptive house title
3. An area to display 4 properties of the house:
   - 3a: Location, consisting of a pin icon and location text
   - 3b: Rooms, consisting of a person icon and a number of rooms text
   - 3c: Size, consisting of some icon and a size (in m^2) text
   - 3d: Price, consisting of a key icon and an amount of money text
4. CTA Button to "Contact Realtor"

**Potential Plan**

### 6. Gallery Section

This section is a collection of 14 images presented in a rather nice, masonry layout. There are no holes between each element -- only equal horizontal and vertical gutters. In terms of layout changes, there are none: The images simply shrink and grow with the viewport. Personally, I am not too fond with how small the images are on mobile devices, so I may design this Grid layout differently.

### 7. Footer Section

The footer is probably the simplest of the sections. It consists of 6 navigational elements that serve as links (but no real target) and your standard copyright sentence. The 6 anchor elements have a very simplistic design with some padding and change of background color when they are hovered over.

For the layout, the 6 anchor elements are arranged in a single column at mobile sizes, and the number of columns increases by 1 when appropriate as the viewport width increases. Between each column change, the width of the elements is allowed to shrink and grow within a range. The copyright sentence is not part of the Grid, and is a basic centered, contained body of text.

Personally, I am not a fan of the way the layout shifts at certain sizes. For example, at a 4-column layout 4 anchors are on the first row and two are on the second row, which looks a rather unpleasant. The same is true at a 5-column layout, with 5 anchors up top and one on the bottom. However, this type of layout is a great candidate for `auto-fit`, and `minmin()` features of CSS Grid, so I'll probably keep it.

## Implementation

**Design System / Project Architecture**

To begin, I should note any similarities between all the elements on the page and begin to think of a design system. With a design system in place, I can share classes and styles across multiple components, keeping the code as DRY as possible. I should also think of a way to architect my SCSS files. Although it doesn't appear to be the most professional of approaches, I like creating an individual SCSS file for each major section of the site, along with a file for global styles, and a file for variables / mixins.

Things I should keep in mind for this step:

- SCSS import statements are being deprecated soon. I need to use...well, `@use` instead, along with `@forward`. This will namespace the imports, so I will have to be mindful I cannot, for example, simply call a variable with `$variableName`, and instead may have to call it with `vars.$variableName`.

**Overall Grid Layout**

I think it makes the most sense to ensure the overall page layout itself is fully responsive and accurate before moving onto developing an individual section. So I will begin with defining a Grid container for the overall page.

**Individual Sections' Grid Layout**

Next, I will ensure each Section (which are Grid containers of their own) behave in their respective responsive manners, with only a single, plain div to serve as their Grid children.

## Insights

- While developing the overall Grid container for the entire page, I realized a value of -1 for row-end only brings a grid item to the end of the _explicit grid_, not the overall grid

- Having the overall body be a Grid container is proving a little difficult. If just one section doesn't shrink and contain itself properly, it causes the entire outer Grid column to not behave properly. For example, the Gallery section is not shrinking properly below 700px, and it causes the other sections to be misaligned. To remedy this, I had to redo my outer container to not use 1fr for its column width, but a minmax between 310px and 1fr. 310px seemed to be the sweet-spot before overflow occured at 325px viewport size (the smallest size I support -- iphone SE).

- When I accidentally wrote `::hover` instead of `:hover`, adding a `pointer: cursor` property worked, but adding a `background-color` did not!

- To easily add a transparent tint to an element's background-image, you specify a linear-gradient before the image value in `background-color`. Note that it must be a linear-gradient -- a simple color value will not work! But we don't want an actual gradient for this particular tint. So we just specify the same value as both the starting and ending color in the gradient:

```css
background-image: linear-gradient(rgba(0, 0, 255, 0.5), rgba(0, 0, 0, 255, 0.5)) url(img/someImg.jpeg);
```

- For the Header section, I do not understand why it is going to a 3-column layout despite me explicitly telling it to use one column of size 1fr!!!
  - Update: Oops! Due to a lack of specificity, one of the h2 tags in Header was being told to span 3 columns, because I wrote `h2: {}` instead of `.realtor h2 {}` in the realtor styles.
