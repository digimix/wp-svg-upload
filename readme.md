## Installation Instructions
Install with Composer
`composer require digimix/wp-svg-upload`

Install manually
1. Clone or copy the files into your WordPress plugins directory
2. Activate the plugin from the dashboard or using WP CLI

Once the plugin is activated, you're good to go. Your WordPress media library will support uploading SVG files. 


##Logic Breakdown
 * 1) We need the whole page, but only if we are in the backend (hence admin_init hook)
 * 2) We would like to grab all output (ob_start within admin_init as nothing should echo before that, we should not interfere with things that do)
 * 3) We want to grab the content on shutdown, concatenate all output buffers, then filter
 * 4) Search for placeholders which should exist and replace the text
 * Downsides
 * 1) Not permanent fix (for perma fix WP core would need to be editable or native filtering added)
 * 2) A bit resource munchy (it's locked to the admin side, so IMHO who cares)
 * 3) This is just to get SVG into WP core... Luckily the find replace is that simple in /wp-includes/media-template.php (Patch it Mullweng & Co!)
 
 ------
 
 ## Changes...
 * Re-factored function declaration and calls to make compatible with lesser PHP versions, despite believing anyone using such versions is dangerous
 * Added param for mime-types to filter_mimes function
 * Moved into a namespace and class to make the whole thing less hack-and-slash
 * Updated to use short-array syntax (Breaking change update your PHP or don't use)
 * Deleted some dead code I never noticed before
 
 ## Credits
 * Originally forked from https://gist.github.com/digimix/01a2e5b38596ea83369a, https://gist.github.com/Lewiscowles1986/44f059876ec205dd4d27
 * Maintained by Digimix 