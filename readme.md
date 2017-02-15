<!-- DO NOT EDIT THIS FILE; it is auto-generated from readme.txt -->
# Customize Inline Editing

Demonstration of how inline editing can be added to the customizer.

**Contributors:** [xwp](https://profiles.wordpress.org/xwp), [westonruter](https://profiles.wordpress.org/westonruter)  
**Tags:** [customizer](https://wordpress.org/plugins/tags/customizer), [customize](https://wordpress.org/plugins/tags/customize), [inline](https://wordpress.org/plugins/tags/inline), [editing](https://wordpress.org/plugins/tags/editing)  
**Requires at least:** 4.7.0  
**Tested up to:** 4.8-alpha  
**License:** [GPLv2 or later](http://www.gnu.org/licenses/gpl-2.0.html)  

[![Build Status](https://travis-ci.org/xwp/wp-customize-inline-editing.svg?branch=master)](https://travis-ci.org/xwp/wp-customize-inline-editing) [![Built with Grunt](https://cdn.gruntjs.com/builtwith.svg)](http://gruntjs.com) 

## Description ##

It is surprisingly easy to add inline editing support to the customizer. With inline
editing, the user no longer has to open a control in the left customizer pane to edit
a setting. Instead, they can just click on the relevant element in the customizer preview
and edit the item inline. It could be said that adding inline-editing to the customizer
improves the UX so much over `postMessage` live editing, as `postMessage` is an improvement
over the `refresh` transport. There is no need to hunt for the right control,
and can actually edit with the customizer pane *collapsed!* Here is a demonstration:

[![Play video on YouTube](https://i1.ytimg.com/vi/1OA8MUI-364/hqdefault.jpg)](https://www.youtube.com/watch?v=1OA8MUI-364)

This plugin provides one example implementation of inline-editing this can be accomplished in the customizer.
Version 0.1 of this plugin from 2014 was a precursor in some ways to [selective refresh](https://make.wordpress.org/core/2016/02/16/selective-refresh-in-the-customizer/)
which was introduced in WordPress 4.5, specifically in regards to how CSS selectors are associated with
customizer settings. With selective refresh, the setting/selector association is formalized in the “Partial”
construct and this inline editing plugin can now build upon that.

Themes can opt-in to support such inline-editing within the customizer by assigning the appropriate type to the registered partials:

```php
add_action( 'customize_register', function( $wp_customize ) {
	$opt_in_partials = array_filter( array(
		$wp_customize->selective_refresh->get_partial( 'blogname' ),
		$wp_customize->selective_refresh->get_partial( 'blogdescription' )
	) );
	foreach ( $opt_in_partials as $partial ) {
		$partial->type = 'inline_editable';
	}
}, 100 );
```

Click on the edit shortcut to begin editing the element, with keyboard focus then given to the editable element.
If the value has a server-side rendered value (e.g. where PHP filters like `wptexturize` apply to improve typography),
the raw value will be supplied when editing starts. Editing can be completed by clicking out of the editable element,
tabbing out of the element (blurring it), or clicking the edit icon which then appears as a “done” checkmark icon. You may also
shift-click on an element to edit it.

Currently only basic text fields can currently be edited; styling and any tags added to `contentEditable` areas will be stripped out.
Eventually rich text formatting may be allowed, specifically for integrations with the Text widget (via JS Widgets) or post content
(via Customize Posts).

**Development of this plugin is done [on GitHub](https://github.com/xwp/wp-customize-inline-editing). Pull requests welcome. Please see [issues](https://github.com/xwp/wp-customize-inline-editing/issues) reported there before going to the [plugin forum](https://wordpress.org/support/plugin/customize-inline-editing).**

## Changelog ##

### 0.2.0 (2017-02-15) ###
* Refactor to make use of selective refresh partials.
* Integrate with edit shortcuts so that clicking the edit shortcut causes the text to be editable and turns into a checkmark icon while edit mode is enabled.

### 0.1.3 (2016-07-10) ###
Ensure that any selective refresh partials associated with the edited settings
will get re-rendered from the server once editing has finished. Refreshed partials
will ensure that the low-fidelity JS-supplied (raw) previews will be replaced with
the actual high-fidelity PHP-rendered preview from the server. See also [#33738](https://core.trac.wordpress.org/ticket/33738).

### 0.1.2 (2016-07-08) ###
Add support for Twenty Sixteen and ensure compat with WordPress 4.6-beta2

### 0.1.1 (2014-12-12) ###
Add support for Twenty Fifteen and ensure compat with WordPress 4.1

### 0.1.0 (2014-09-19) ###
First release.


