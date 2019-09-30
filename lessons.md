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

- ## Sizing grid items

- If we want an item to span multiple columns we use `grid-column: span columns_number`.
- If an items spans more columns than the grid can fit from the starting position of the item, it will wrap the item to the start of the next row. This will leave the space the item would've taken in blank.
- We can also use `grid-row: span columns_number` to span multiple rows.
- If the single item is bigger than the actual grid can fit it will create implicit columns/rows to fit the item.