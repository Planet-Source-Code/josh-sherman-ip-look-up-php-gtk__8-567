<div align="center">

## IP Look\-up \(PHP\-GTK\)


</div>

### Description

Looks up the IP address for a domain. DON'T FORGET TO RATE MY CODE!
 
### More Info
 
Usage: php -q ip_lookup.php


<span>             |<span>
---                |---
**Submitted On**   |
**By**             |[Josh Sherman](https://github.com/Planet-Source-Code/PSCIndex/blob/master/ByAuthor/josh-sherman.md)
**Level**          |Intermediate
**User Rating**    |4.0 (28 globes from 7 users)
**Compatibility**  |PHP 4\.0
**Category**       |[Internet/ Browsers/ HTML](https://github.com/Planet-Source-Code/PSCIndex/blob/master/ByCategory/internet-browsers-html__8-9.md)
**World**          |[PHP](https://github.com/Planet-Source-Code/PSCIndex/blob/master/ByWorld/php.md)
**Archive File**   |[](https://github.com/Planet-Source-Code/josh-sherman-ip-look-up-php-gtk__8-567/archive/master.zip)





### Source Code

```
<?
/*
 * ip_lookup.php - My first attempt at PHP-GTK.
 *
 * Author: Josh Sherman
 * Purpose: Looks up the IP address for a domain.
 * Usage: php -q ip_lookup.php
 *
 */
// Check to see if the PHP-GTK extension is available.
if (!class_exists('gtk')) {
	if (strtoupper(substr(PHP_OS, 0, 3)) == 'WIN')
		dl('php_gtk.dll');
	else
		dl('php_gtk.so');
}
// Called when delete-event takes place, tells it to proceed.
function delete_event()
{
	return false;
}
// Called when the window is being destroyed, tells it to quit the main loop.
function destroy()
{
	Gtk::main_quit();
}
// Called when the button is clicked, looks up the IP and places it in the
// entry box.
function get_ip()
{
	global 	$text;
	global	$domain;
	global	$window;
	global	$ip_address;
	$domain = $text->get_text();
	$ip_address = gethostbyname($domain);
	$text->set_text($ip_address);
}
// Creates a new top-level window and connect the signals to the appropriate
// functions.
$window = &new GtkWindow();
$window->connect('destroy', 'destroy');
$window->connect('delete-event', 'delete_event');
$window->set_border_width(5);
$window->set_title('IP Look-up');
$window->set_policy(false, false, false);
// Creates a table to place the widgets in, and adds it to the window.
$grid = &new GtkTable(2, 2);
$grid->set_row_spacings(4);
$grid->set_col_spacings(4);
$window->add($grid);
// Creates a label to describe the entry field and adds it to the table.
$label = &new GtkLabel();
$label->set_text("Domain:");
$grid->attach($label, 0, 1, 0, 1);
// Creates an entry field and adds it to the table.
$text = &new GtkEntry();
$text->set_editable(true);
$text->set_max_length(256);
$grid->attach($text, 1, 2, 0, 1);
// Creates tooltips object for the entry field.
$ttentry = &new GtkTooltips();
$ttentry->set_delay(200);
$ttentry->set_tip($text, 'Type the domain you want to look up here.', '');
$ttentry->enable();
// Creates a button, connects its clicked signal to the get_ip() function and
// adds the button to the window.
$button = &new GtkButton('Get IP');
$button->connect('clicked', 'get_ip');
$grid->attach($button, 0, 2, 1, 2);
// Creates tooltips object for the button.
$ttbutton = &new GtkTooltips();
$ttbutton->set_delay(200);
$ttbutton->set_tip($button, 'Looks up the IP', '');
$ttbutton->enable();
// Show the window and all of it's child widgets.
$window->show_all();
// Set focus to the entry field.
$window->set_focus($text);
// Run the main loop.
Gtk::main();
?>
```

