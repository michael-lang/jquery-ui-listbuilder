The official development and planning wiki for this project:
http://wiki.jqueryui.com/w/page/12137993/ListBuilder


1 - Description:
================
 
This widget provides a well-constrained way to let users build a list of items. Common applications include the Facebook-style list builder for message recipients (F6) which provides a textarea with an auto-complete function and the ability to re-order and delete recipients. The Apple Mail style builder (F7) adds an action menu next for each item that can be used to offering multiple actions. This should support re-ordering via drag and drop, plus keyboard shortcuts to select and delete items.
 
The autocompletion is optional, when enabled, it needs the Autocomplete as a dependency.
The default is to be disabled: .listbilder({ autocomplete: false })

2 - Visual Design
=================
See: http://wiki.jqueryui.com/w/page/12137993/ListBuilder

3 - Functional Specifications/Requirements:
===========================================
 
Options:
--------
* delimeter (string, default: ",") 
A text delimeter used to parse the original values at creation time and then to write list items back into the original text input each time an item is added, removed, or sorted to a new position.
* duplicates (boolean, default: false) 
 Specifies if more than one item of the same text value can be added.
* sortable (boolean, default: false)
Specifies if the list of items can be sorted.  Details of the sort are not customizable.
* autocomplete (boolean, object, default: false) 
 - If false then the list builder does not auto-suggest value from an autocomplete
 - To enable autocomplete pass in the options to be passed into the autocomplete exactly as normally supported by the autocomplete widget.
 - If the select event is not specified on the autocomplete options then a default implementation is added to put the selected value in the list builder and then clears the token editor
 - If the select event is specified on the autocomplete options, then that method must use the add method of listbuilder to put the selected value into the list.
 
Methods:
--------
* add (string)
Adds a new item to the list and to the underlying linked text input or textarea
* remove (list item element)
Removes the specified list item from the list and then updates the underlying text input or text area from remaining items.
* editItem (list item element)
Takes the text of the list item on puts it in the editable area, and then removes that list item from the list.  When done editing the newly changed value becomes a new list item.
* selectedItem
Getter for the currently selected list item
* listblur
Removes focus from this input element.  Blurs the text input or text area and removes any selected styles from list items.  
 
Events:
-------
* select
 - Triggered when the user clicks on one of the items in the list (sets originalEvent to 'click')
 - Triggered when the user hovers of one of the items in the list (sets orginalEvent to 'mouseenter')
 - Triggered when the user uses arrow keys to navigate to an item in the list (sets originalEvent to ?) (not yet implemented)
 - ui.item refers to the selected list item
 
Keyboard Navigation:
--------------------
* up / left 
 - navigates to previous list item
 - if cursor is in token editor and there is a text value do not change selected item.  leave focus in the textbox
 - if cursor is in token editor and there is no text value, then select the last item.
* right / down
 - navigates to next list item
 - if cursor is in the token editor do not navigate
* delete
 - deletes current list item and highlights next item (or last item if last was deleted)
 - if cursor is in the token editor do not navigate.  Instead edit text as normal.
* backspace
 - deletes current list item and highlights previous item (or first item if first was deleted)
 - if cursor is in the token editor do not navigate.  Instead edit text as normal.
* any other character
 - put the typed value in the token editor and deselect any selected item.  Show autocomplete if appropriate.
* If autocomplete is visible disable keyboard navigation of list items since it should then navigate the autocomplete list