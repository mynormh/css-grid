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
