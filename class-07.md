# Notes from Duckett HTML and JS Books

Notes taken from Ducketts HTML book chapter 6 and JavaScript book Chapter 3.

[HTML Chapter 6 Tables](#html-book-chapter-6-tables)
[JS Chapter 5 Document Object Model](#js-book-chapter-5-functions-objects-and-methods)

## HTML Book Chapter 6: Tables

Tables are useful for arranging data in a display: Schedules, sports statistics and scores, etc.

### Basic Table Structure

Tables are made of Headings, Rows, Cells, and an optional Footer.

Table Rows and Cells are stored within the Table Body (much like an HTML Document).

Table Data is tabular data stored within one or more columns in a table row.

A simple table:

```html
<table>
  <thead>
  <tr>
    <th></th>
    <th scope="col">Column1</th>
    <th scope="col">Column2</th>
  </tr>
  </thead>
  <tbody>
  <tr>
    <th scope="row">Row1</th>
    <td>R1C1 Data</td>
    <td>R1C2 Data</td>
  </tr>
  <tr>
    <th scope="row">Row2</th>
    <td>R2C1 Data</td>
    <td>R2C2 Data</td>
  </tr>
  </tbody>
  <tfoot>
    <tr>
      <td span="3">This Is The Footer</td>
    </tr>
  </tfoot>
</table>
```

Items of Note:

- TH attribute "scope": Defines a heading for the "row" or "col".  
- TD attribute "colspan": Used to merge cells within a row.  
- TD attribute "rowspan": Used to merge cells *across rows*.  
  - Be *careful* with 'rowspan': It is easy to lose track of which rows are spanned.  

  The following elements help the browser to keep the Header and Footer in-view while scrolling:

- THEAD: Should contain all top-of-table header content. Use for long tables and for accessibility.  
- TBODY: Should contain all tabular data cells below the header. Use for long tables and for accessibility.  
- TFOOT: Should contain only the bottom section of the table (usually one row, sometimes more).
  - Use for long tables and for accessibility.  

### OLD CODE

Avoid using the following due to browser compatibility issues, instead use the suggestions that follow:  

- Width: Use CSS 'padding'  
- Spacing: Use CSS 'padding'  
- Border: Use CSS 'border'  
- BGColor: Use CSS 'background'  

*Note*: Use CSS style properties whenever possible instead of html attributes for styling.  

## JS Book Chapter 5: Functions Objects and Methods

See [Class-06: JS Chapter 3 and JS Chapter 5](class-06.html)
