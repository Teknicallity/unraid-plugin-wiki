## Overview

The structure of a plugin can vary, but there a few conventions that have formed in popular plugins that help organize them.

### Plugin Source Directory

Any `.page` files will always be in the plugin's source directory as is required by Unraid. From there, a few folders are common:

- `icons`: Small images that will be displayed within the plugin tab.
- `images`: Larger images that are used for the plugin launcher entry.
- `include`: Location for any other PHP code not contained in the `.page` files.
- `scripts`: A place for bash or PHP scripts that are executed from the shell.

A few plugins also have a folder, `pages`, which contains what otherwise would be placed in the `.page` files. This is optional, and simply to help with IDE syntax and highlighting, since the `.page` format is not not standardized.

Instead, the `.page` files contains just the header and a single line of PHP:

`include "/usr/local/emhttp/plugins/<plugin-name>/pages/<page-name>.php";`

This simply invokes the PHP code within the specified file.

### Version Control Repository

The `.plg` file for plugin installation should not be within the source code directory.

Since Unraid requires an archive or package of some type, there is often an `archive` directory or, if using Github, a releases section on the sidebar.
