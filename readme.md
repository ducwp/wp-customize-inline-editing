<!-- DO NOT EDIT THIS FILE; it is auto-generated from readme.txt -->
# Customize Inline Editing

Demonstration of how inline editing can be implemented in the customizer.

**Contributors:** [xwp](https://profiles.wordpress.org/xwp), [westonruter](https://profiles.wordpress.org/westonruter)  
**Tags:** [customizer](https://wordpress.org/plugins/tags/customizer), [customize](https://wordpress.org/plugins/tags/customize), [inline](https://wordpress.org/plugins/tags/inline), [editing](https://wordpress.org/plugins/tags/editing)  
**Requires at least:** 4.7.0  
**Tested up to:** 4.8-alpha  
**Stable tag:** 0.2.0  
**License:** [GPLv2 or later](http://www.gnu.org/licenses/gpl-2.0.html)  

[![Build Status](https://travis-ci.org/xwp/wp-customize-inline-editing.svg?branch=master)](https://travis-ci.org/xwp/wp-customize-inline-editing) [![Built with Grunt](https://cdn.gruntjs.com/builtwith.svg)](http://gruntjs.com) 

## Description ##

In WordPress 4.5 the [selective refresh](https://make.wordpress.org/core/2016/02/16/selective-refresh-in-the-customizer/)
framework was introduced in core. One of the key concepts in this framework is the
“partial”, the region in a document which is selectively refreshed when a related
setting is modified. This means that one or more settings are linked with a given
element in the preview. When selective refresh was first was introduced it supported the ability
for a user to “shift click” on a partial to jump to and focus on the related control
in the pane. In WordPress 4.7 this was then enhanced with [visible edit shortcuts](https://make.wordpress.org/core/2016/11/10/visible-edit-shortcuts-in-the-customizer-preview/) so that
users could click (touch even) on the icon to be able to reveal the control in the pane.

The Customize Inline Editing plugin builds on edit shortcuts by allowing the setting
to be modified inline via direct manipulation in the preview without having focus
removed and placed on the controls pane. This is particularly useful on <em>mobile devices</em>
on small screens where a user cannot both see the controls and preview at the same time,
as can be compared here:

[![Play video on YouTube](https://i1.ytimg.com/vi/a_l0LAVUHlw/hqdefault.jpg)](https://www.youtube.com/watch?v=a_l0LAVUHlw)

Inline editing in this way is also helpful for <em>accessibility</em> since keyboard
focus remains in the preview at the element being edited, as can be seen in this demonstration
of inline editing on a desktop browser:

[![Play video on YouTube](https://i1.ytimg.com/vi/i7XNrXdiSCE/hqdefault.jpg)](https://www.youtube.com/watch?v=i7XNrXdiSCE)

This plugin provides one example implementation of inline editing this can be accomplished in the customizer.
Version 0.1 of this plugin from 2014 was a precursor in some ways to selective refresh, specifically in regards
to how CSS selectors are associated with customizer settings.

Themes can opt-in to support this plugin's inline editing within the customizer by assigning the appropriate type to the registered partials:

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
Eventually rich text formatting may be allowed, specifically for integrations with the Text widget (via [JS Widgets](https://github.com/xwp/wp-js-widgets)) or post content
(via [Customize Posts](https://github.com/xwp/wp-customize-posts)).

The [selective refresh](https://make.wordpress.org/core/2016/02/16/selective-refresh-in-the-customizer/) writeup from 4.5 concludes
with a section on a possible future for it and inline editing:

> If we can eliminate full-page refreshes from being the norm for the Customizer, we can start to introduce
> controls inline with the preview. If the entire preview does not reload, then the inline controls won’t get
> destroyed by the refresh with each change. For example, consider a widget control floating immediately next
> to the widget in the sidebar it is editing. With selective refresh, it will then also be possible to <em>eliminate
> the Customizer altogether</em>. The Customizer could be available to anyone who is logged in, with the controls
> being bootstrapped on demand when a user wants to edit a given element. There would be no need to navigate way
> from a page on the frontend to enter a unique Customizer state: the Customizer would come to the user. Any controls
> not relevant to being inline could remain in the Customizer pane, but it could slide in only as needed instead of
> appearing by default. That is to say, selective refresh makes the Customizer a much better framework for
> implementing <strong>frontend editing</strong>.

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


