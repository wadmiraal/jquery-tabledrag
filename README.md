jQuery (Drupal) Tabledrag plugin
================================

This is a fork of the [Drupal](http://www.drupal.org/project/drupal) Tabledrag Javascript component. It allows you to make tables orderable by drag and drop.

The plugin gracefully degrades when JS is not available by showing one or two select lists, allowing users to select a "weight" for each row (defining the *order*) as well as optionally a "parent" (defining a *hierarchy*).

It is based on the Drupal 7 version.


Use case
--------

This component is used throughout the Drupal backend, but most noticeably in the menu administration. It allows users to easily reorder and reorganize their site's menu items with a drag-n-drop interface.

It's designed to be used with forms. Order and hierarchy information are stored in form inputs (select lists, textfields or hidden inputs). This allows developpers to create an intuitive front-end interface, while still being able to use classic forms for sending data to the back-end. No AJAX is required.


Dependencies
------------

Currently requires the [jQuery Cookie](https://github.com/carhartl/jquery-cookie) plugin (as does the Drupal version).


Demo
====

[Click here](http://wadmiraal.github.com/jquery-tabledrag/)


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

  // The <tr> class indicating that it's draggable.
  draggableClass: 'draggable', 

  // The path for the cookie flag. A link is displayed which allows users
  // to switch between the drag and drop interface or the "plain" interface.
  cookiePath: '/',

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
  // To allow the child-parent relationship to function correctly, each row must contain an input 
  // with the class defined in sourceFieldClass wich represents the current row. 
  // This can be a hidden input.
  parent: {
    // The class of the field containing the "parent" id. Can be any form item.
    fieldClass: 'row-parent', 

    // The class of the field containing the current "row" id. Can be any form item.
    sourceFieldClass: 'person-id', 

    // Hides the parent <td> of the "parent" field for better usability.
    hidden: true 
  },

  // The group option allows elements to be dragged with their children as a whole. 
  // This is usually what you want.
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

Example markup:
```html
<table id="my-table">
  <thead>
    <tr>
      <th>Name</th>
      <th>Age</th>
      <th>Order</th>
      <th>Parent</th>
    </tr>
  </thead>
  <tbody>
    <tr class="draggable">
      <td>Alex 
        <input class="person-id" name="person-1-id" value="person-1" type="hidden" />
        <input class="row-depth" name="person-1-depth" value="1" type="hidden" />
      </td>
      <td>34</td>
      <td>
        <select class="row-weight" name="person-1-weight">
          <option selected value="1">1</option>
          <option value="2">2</option>
          <option value="3">3</option>
        </select>
      </td>
      <td>
        <select class="row-parent" name="person-1-parent">
          <option selected value="0">No one</option>
          <option value="person-2">Bob</option>
          <option value="person-3">Candice</option>
        </select>
      </td>
    </tr>
    <tr class="draggable">
      <td>Bob 
        <input class="person-id" name="person-2-id" value="person-2" type="hidden" />
        <input class="row-depth" name="person-2-depth" value="2"  type="hidden" />
      </td>
      <td>22</td>
      <td>
        <select class="row-weight" name="person-2-weight">
          <option selected value="1">1</option>
          <option value="2">2</option>
          <option value="3">3</option>
        </select>
      </td>
      <td>
        <select class="row-parent" name="person-2-parent">
          <option value="0">No one</option>
          <option selected value="person-1">Alex</option>
          <option value="person-3">Candice</option>
        </select>
      </td>
    </tr>
    <tr class="draggable">
      <td>Candice 
        <input class="person-id" name="person-3-id" value="person-3" type="hidden" />
        <input class="row-depth" name="person-3-depth" value="1" type="hidden" />
      </td>
      <td>24</td>
      <td>
        <select class="row-weight" name="person-3-weight">
          <option value="1">1</option>
          <option selected value="2">2</option>
          <option value="3">3</option>
        </select>
      </td>
      <td>
        <select class="row-parent" name="person-3-parent">
          <option selected value="0">No one</option>
          <option value="person-1">Alex</option>
          <option value="person-2">Bob</option>
        </select>
      </td>
    </tr>
  </tbody>
</table>
```


Events
======

Each event passes the entire TableDrag instance as a second parameter.

* `tabledrag:dragrow` is triggered when the row is starting to get dragged
* `tabledrag:droprow` is triggered when the row is droppen.


License
=======

Licensed under GPL V2.