# Wisdom nugs

## Fundamentals

- CSS Grid works in two dimensions (rows and columns), in contrast to flexbox that only works in one dimension (row or columns).
- With Grid we can explicitly define the number of columns and rows (collectively called `tracks`) and position the items across them.
- With `grid-template-columns` we can explicitly say how many columns we want by specifying each column size and the rows will be generated automatically depending of our grid items.
- The same applies to `grid-template-rows` with the exception that if we don't explicitly define columns it will only create one column.
- `grid-gap` allows us to create gaps between the columns and rows.
- When using `auto` as the size of a track it will automatically make the item as big as the available space and explicitly sized tracks allow.
- `tracks` are numbered by the lines that start and stop them, not by column/row itself.
- Refer to Line Meaning.png

## Implicit vs explicit tracks

- When we use `grid-template-columns` or `grid-template-rows` to create tracks they are called explicit, if not they are implicitly generated.
- When grid can't fit an item in explicit tracks it will generate as many implicit rows needed to fit these items.
- The items in explicit rows are sized by the values we defined but for the ones in implicit rows we can `grid-auto-rows: 100px` to set their size. We can even set the size of multiple implicit rows `grid-auto-rows: 100px 500px` and this will also repeat the pattern after every two implicit rows.

## grid-auto-flow

- When we explicitly create columns but not rows, grid will generate implicit rows to fit the items in.And by default grid will wrap items into rows.
- `grid-auto-flow` indicates weather items will be wrapped into rows or columns. By default `grid-auto-flow: row`.
- And just like with rows we can define the implicit columns size with `grid-auto-columns`.

## Sizing tracks

- We can use percentages in `grid-template-columns` but it becomes a little complicated (especially when we want them to add up to 100%) when we have to take into account the gap size and we'd have to substract it from each column size.
- Rather than using percentages, it is preferred to use the `fr`(fraction) unit. `fr` represent the amount of space left after all the elements with an explicit width/height are layed out.
- By default the height of a grid is how hight the content is and the same applies for the height of a grid-item. But the default width of a grid is how wide the viewport is.
- By using `auto` we're telling grid to fit the column to the size of the biggest content in that column.

## Repeat function

- `repeat(amount, pattern)` allows us to repeat a given pattern the specified amount of times. It can go anywhere in `grid-template-columns` or `grid-template-rows`, allowing us to mix and match them with other values.

## Sizing grid items

- If we want an item to span multiple columns we use `grid-column: span columns_number`.
- If an items spans more columns than the grid can fit from the starting position of the item, it will wrap the item to the start of the next row. This will leave the space the item would've taken in blank.
- We can also use `grid-row: span columns_number` to span multiple rows.
- If the single item is bigger than the actual grid can fit it will create implicit columns/rows to fit the item.

## Placing grid items

- `grid-column` is actually a shorthand for:
  - `grid-column-start`: specifies the item's start position by specifying a line track or span. By default `grid-column-start: auto`.
  - `grid-column-end`: specifies the item's end position by specifying a line track or span. By default `grid-column-end: auto`.
- They both can also start counting from the last track to the first by specifing a negative number of track, where the last track is `-1`. This will onlly work for explicit tracks.

## auto-fit and auto-fill

- `auto-fill` tells grid to automatically fit as many possible columns in the grid, this will end the explicit grid at the end of the last possible column and change as the viewport size changes.
- `auto-fit` the same as `auto-fill` but when there's free space available it will end the explicit grid at the end position of the last item.

## Responsive grids

- When we manually set the size along with `auto-fill` or `auto-fit` we might run into cases where the content starts to spill out of the item. To fix this we use `minmax(min, max)` and if we use `1fr` as our max value it will grow as big as the available free space if needed. This replaces several uses form media-queries.
- If we want a track to adjust to the content like `auto` but want to set a max-width/hight we can use `fit-content(100px)`.

## Grid template areas

- Another way to place and size the items in a grid is by giving specific names to areas of the grid with `grid-template-areas: ""` giving each area where the tracks intersect a name and then assigning a grid-item to an area with `grid-area`.
- If we want an area to not be named we can use `"."`.
- With this we can simply redefine our template areas in a media query to have a responsive design.

## Area line names

- When we create template areas we also create line names, which means we can simply use the line names and append `-start` or `-end` to define a start and end for the items, without needing to use line numbers.

## Naming lines

- To name a line we use `[]` when defining the tracks and we can use this names to size and position the items with `grid-column` and `grid-row`.
- One line can have multiple names defined inside the `[]`.

## Dense

- By default when we have more items that can fit into the grid it will automatically wrap them to the next implicit row (`grid-auto-flow: row`), we can also set it so it creates implicit columns (`grid-auto-flow: column`) instead.
- A third option is `grid-auto-flow: dense`, where if an item can't fit in the current row then it will still wrap it onto the next row but the blank space left by that item will be filled by items that can fit in that space.
- This is not a perfect masonry since there will be times there are some blank spaces still left because it couldn't fit any items.

## Aligning and Centering

- Just like in flexbox, we can move items along the axises in grid but unlike flexbox the axises don't switch:
  - `justify-*` is row axis.
  - `align-*` is column axis.
- In grid we have the following properties;
  - `justify-items`: Controls how wide the elements themselves are. By default `justify-items: stretch`.
  - `align-items`: Controls how high the elements themselves are, it won't work without explicit rows. By default `align-items: stretch`.
  - `justify-content`: If the grid is not as wide as it could be (grid is by default the width of the viewport), it controls what to do with the extra space available in the row axis. By default `justify-content: start`
  - `align-content`: Same as `justify-content` but in the column axis, it will only work in a container with a fixed height which is not too common. By default `align-content: start`.
  - `justify-self`: Is defined in the grid-item itself and overrides the value of `justify-content`.
  - `align-self`: Is defined in the grid-item itself and overrides the value of `align-content`.
- The `place-items` property is a shorthand for `justify-items` and `align-items`.

Useful to look up [A Complete Guide to Grid](https://css-tricks.com/snippets/css/complete-guide-grid/)

## Ordering items

- We can specify the order of the items for the layout with `order: number`.

## Album layout

- By using a combination of `aut-fit` and `minmax()` we tell the grid to fit as many columns possible with a set min-width and when it has extra space to give each item `1fr`.
- Similar to flexbox we can also nest grids by making a grid-item a grid-container too.
- We use the `width: 100%` in the images so they adapt to the size of the grid column and don't spill out of it.

## Image Gallery

- The grid will always be `100px`x`100px` and each image has a random size between 1-4 tracks (both columns and rows). We generate the random sizes with JS.
- With JS we generate the actual HTML elements that will go in the grid and to the `<img>` element we assign a class of the random height and width generated. The image we select for each grid-item is also random and we also choose it with JS.
- With `Array.from()` we can specify the length of the array and also pass it a callback function that will fill the array.
- Since the columns have a fixed width of `100px` (instead of `fr`s) the images can spill out of the column, to fix this we apply `overflow: hidden` to the images.
- `grid-auto-flow: dense` will fill the blank spaces left in the grid where it couldn't fit the next image.
- We concat a ton of 1x1 images to make sure the little 1x1 grid tracks have enough images to be filled with.
- To make the image fit exactly the grid we make the images `width: 100%` and `heght: 100%`, we also use `object-fit: cover` so the aspect-ratio of the image doesn't look distorted.
- To avoid having to make the items `position: absolute` so we can display the overlay, we instead make the grid-item also a grid-container and let the images span the entire track.
- If we place two or more items in the same row and column they will just overlap each other, so we use this to get the overlay effect along with `position: relative`. Note: Since the `<img>` element is before the `.item__overlay` element in our HTML, we don't need to specify a `z-index` when using `position: relative`.
- We also make the `.item__overlay` a grid-container so we can center the button.
- We handle the entire overlay image view with JS, by getting the image of the clicked item and setting it as the `src` of the image in the `.overlay` element.
