**USAGE**

Structure inputs:
<pre>
When writing an input, structure it like this in order for the script to detect it.

CHECKING INVENTORY:
(check/rummage through/open/look into) (your/a/the) (bag/inventory/pockets/pouch)

This will display your inventory, or you can alternatively check the inventory section in the menu.

ADDING ITEMS: 

(add/put/stash/add/store/pick up) (digit 0-9) OR (a/an/the/your) item(s) (put them into/in/into/inside/to a/an/the/your) (inventory/bag/backpack/pouch/pocket)

REMOVING ITEMS: 

(remove/take out/pull out/take) (digit 0-9) OR (a/an/the/your) item(s) (from/out of) (a/the/your) (inventory/bag/backpack/pouch/pocket)

item(s) can include multiple items if you simply add an 'and' between items,

It is recommended not to use plural when adding or removing items.
(See Stacking in TECHNICAL for more info) 

The quantity = (the digit infront of the name), must be a single digit, meaning it can be a maximum of 9 and a minimum of 1.

</pre>
**TECHNICAL**

Stacking
<pre>
This script uses stacking to keep things neater.

Plural Example:
If you add an item using the plural form
Ex. You add 2 cups of tea to your bag.

and then you try to take only one out later
Ex. You take a cup of tea out of your bag.

it will not work, because the items you stored where stored using a plural name.

Using this example it would work to say
Ex. You take a cups of tea out of your bag.

but that may sound to odd or be difficult to remember,
so it is best to simply not using plural when adding or removing items.

Non Plural Example:
Ex. You add 2 cup of tea to your bag.

Ex. You take a cup of tea out of your bag.

This will work just fine because each time the same name was used.

</pre>
Implementation
<pre>
To use this in your script:

1. Add the inventory class to shared library
2. Create a new object in input modifier that is the inventory class (see example file)
3. call the update method of that object and pass in the text in lowercase (see example file)

</pre>
Manualy Adding/Removing items in script
<pre>
bag.receiveString_add('item you want to add');

OR if you want to remove an item:

bag.receiveString_remove('item you want to remove');

Please note that if the item you are trying to remove is not in the inventory array, nothing will happen.

</pre>
Regular Expressions:
<pre>
ADDING

(in literal form) add_inventory_regex = /(?:add|put|stash|add|store|pick up)\s+(?:(\d)?|(?:a|an|the|your))\s+(.*)\s+(?:put them into|in|into|inside|to)\s*(?:a|an|the|your)\s+(.*\s+)?\s*(inventory|bag|backpack|pouch|pocket)/gim;

(in object form) add_item_regex = new RegExp('\\b(?:'+action_add+')\\s+(?:(\\d)|(?:'+article+'))\\s+(.*)\\s+(?:put them into|in|into|inside|to)\\s*(?:'+article+')\\s+(.*\\s+)?\\s*('+inventory_word+')\\b', 'gi');

REMOVING:

(in literal form) remove_inventory_regex = /(?:remove|take|take out|pull out|remove)\s+(?:(\d)?|(?:a|an|the|your))\s+(.*)\s+(?:from|out of)\s*(?:a|the|your)\s+(.*\s+)?\s*(inventory|bag|backpack|pouch|pocket)/gim;

(in object form) remove_item_regex = new RegExp('\\b(?:'+action_remove+')\\s+(?:(\\d)|(?:'+article+'))\\s+(.*)\\s+(?:from|out of)\\s*(?:'+article+')\\s+(.*\\s+)?\\s*('+inventory_word+')\\b');

</pre>

