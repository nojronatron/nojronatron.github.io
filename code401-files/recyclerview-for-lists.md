# Read Class 28 Notes

Android Developers on [RecyclerView for Displaying Lists of Data](https://developer.android.com/guide/topics/ui/layout/recyclerview#java)

## Create Dynamic Lists with RecyclerView

A bunch of code is required to get RecyclerView elements to operate. Once you're done struggling to get all this wrapper and setup code implemented, they're pretty alright.

### Key Classes

Contain Views corresponding to your data.

Is a View in-and-of-itself.

Add RecyclerView to the Activity Layout as any other View element.

View Holder: Represent individual elements *within* the RecyclerView container element.

A View Holder must be created and the RecyclerView *binds its data* to the View Holder.

An Adapter is used by the RecyclerView to request View Holders and Bind its data to them.

Layout Manager is an abstract class that can be used to arrange how the data is displayed by the Recycler View.

*Note*: Custom Layouts can be defined by extending the abstract Layout Manager.

## Implement Recycler View

1. Decide what the list or grid will look like within the Recycler View.
1. Design *each element*'s look and behavior. Extend ViewHolder to implement these designs.
1. Define an Adapter that associates your data with the ViewHolder views.

ViewHolder is the wrapper around View that is managed by RecyclerView.

## Play The Layout

LinearLayoutManager: Single-dimensional list.

GridLayoutManager: Two-dimensional *grid* that can be horizontally or vertically arranged.

- Vertical Arrangement: Manages set columns *widths*.
- Horizontal Arrangement: Manages set rows *height*.

StaggeredGridLayoutManager: Similar to GridLayoutManager but *allows staggered row and column data layout*.

These settings must be made in order to desing the ViewHolder.

## Implement Adapter and View Holder

ViewHolder is wrapper around View which contains layout of an individual item in the list.

Adapter creates ViewHolder objects *as needed*, setting the data *for the Views*.

Requirements to defining the Adapter:

1. Override onCreateViewHolder(): Creates and inits ViewHolder and View (no data binding here).
1. Override onBindViewHolder(): Fetch and associate ViewHolder with fetched data.
1. Override getItemCount(): RecyclerView calls this to track size of dataset for determining "bottom" of the list.

Also:

- Implement an XML FrameLayout file e.g. 'text_row_item.xml' that defines width, height, margin, and gravity.
- Implement FameLayout.TextView xml with a unique ID, width, height, and text `@string/element_text`.
- Create a local private Field to store the dataset.
- Extend RecyclerView (detailed code [here](https://developer.android.com/guide/topics/ui/layout/recyclerview#java)).
- Create getTextView() method to review a TextView based on specific view R.id.textView tag.
- Initialize the Custom Adapter with the Dataset; CTOR sets dataset to local private dataset field.
- Implement `@Override` methods onCreateViewHolder, onBindViewHolder, and getItemCount.

## Footer

Return to [Root Readme](../README.html)
