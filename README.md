jQuery (Drupal) Tablesort plugin
================================

This is a fork of the [Drupal](http://www.drupal.org/project/drupal) Tablesort Javascrtip component. It allows you to make tables sortable by drag and drop.

The plugin gracefully degrades when JS is not available by showing one or two select lists, allowing users to select a "weight" for each row (defining the *order*) as well as optionally a "parent" (defining a *hierarchy*).

It is based on the Drupal 7 version.


Use case
--------

This component is used throughout the Drupal backend, but most noticeably in the menu administration. It allows users to easily reorder and reorganize their site's menu items with a drag-n-drop interface.

It's designed to be used with forms. Order and hierarchy information are stored in form inputs (select lists, textfields or hidden inputs). This allows developpers to create an intuitive front-end interface, while still being able to use classic forms for sending data to the back-end. No AJAX is required.


Demo
====

Coming soon...


Documentation
=============

Enabling a table is easy:
```javascript
$('#my-table').tableDrag();
```

Now, each `tr` in this table that has a class of `draggable` (or any other you specify) will be treated as a draggable, orderable row.
Note the `weight` and `parent` input fields should be inside their own `td`, as the plugin can hide entire columns for better usability (more below).

The following options can be passed as a hash to the `tableDrag()` function. Comments explain what they mean. These are the defaults:

```javascript
{
  // General options.
  draggableClass: 'draggable', // The <tr> class indicating that it's draggable.

  // Specific options.

  // The weight option allows elements to be sorted. 
  // Pass a "falsy" value to fieldClass to deactivate (false, null, undefined, etc).
  weight: {
    // The class of the <select> list. Weights will be deduced by the <option>s in this list. 
    // <option> values should be integers.
    fieldClass: 'row-weight', 

    // Hides the <select>s parent <td> for better usability.
    hidden: true 
  },

  // The parent option allows elements to be children of one another.
  // Pass a "falsy" value to fieldClass to deactivate.
  // To allow the child-parent relationship to function correctly, each row must contain an input with the class defined in
  // sourceFieldClass wich represents the current row. This can be a hidden input.
  parent: {
    // The class of the field containing the "parent" id. Can be any form item.
    fieldClass: 'row-parent', 

    // The class of the field containing the current "row" id. Can be any form item.
    sourceFieldClass: 'person-id', 

    // Hides the parent <td> of the "parent" field for better usability.
    hidden: true 
  },

  // The group option allows elements to be dragged with their children as a whole. This is usually what you want.
  // It's related to parent and can only function with it.
  // Pass a "falsy" value to fieldClass to deactivate.
  group: {
    // The class of the field containing the row "depth". Can be any form item.
    fieldClass: 'row-depth', 

    // The depth limit to which items can be nested and dragged as a group.
    depthLimit: 3 
  },
}
```


License
=======

Licensed under GPL V2.