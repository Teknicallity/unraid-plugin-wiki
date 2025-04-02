## Overview

Page files define the user interface and functionality of any Unraid page.

## Page File Location

Plugin page files must be placed in the following directory:

`/usr/local/emhttp/plugins/<plugin-name>/`

## Defining the Plugin Entrypoint

Each plugin requires an entrypoint page, which must be referenced in the [`.plg` file](/files-and-structure/Plg-File.md) using the `<PLUGIN launch=[url path]>` tag. The specified URL path determines how the page is accessed in the browser.

The page file's name must be unique, or else it could override another page. For example, if you name a file `Settings.page`, it may remove the Unraid settings tab unless the plugin is removed.

A common convention is to put your main page file under the Unraid tab url where it will be located. For example:

- The Appdata Backup plugin appears under the Settings tab with the URL path: `Settings/AB.Main`
- Here, AB.Main serves as the entrypoint page file.

## Plugin Entrypoint

Plugins often include multiple pages accessible via tabs. A common approach is to create a dummy page as the main entrypoint, directing users to the first available tab.

### Example Dummy Page

`HelloWorld.page`

```php
Menu="Utilities"
Type="xmenu"
Title="Hello World"
Icon="myimage.png"
Tabs="true"
---
```

### Field Descriptions

- `Menu`: Defines where the plugin’s launcher icon appears.

  - OtherSettings – System Settings
  - NetworkServices – Network Services
  - UserPreferences – User Preferences
  - Utilities – User Utilities (most common)

- `Type`:

  - `menu` – Creates a new section (rarely used)
  - `xmenu` – Default type, adds a launcher icon entry for the plugin

- `Title`: Label displayed under the plugin icon.
- `Icon`: What will be displayed as the icon for the launcher entry.

  - References an image in: `/usr/local/emhttp/plugins/<plugin-name>/images/myimage.png`
  - Or a [Font Awesome 4 icon](https://fontawesome.com/v4/icons/) icon can be used.

## Plugin Tab Pages

If you want to have tabs in your plugin, each tab must have its own `.page` file.

The header should look like the following:

### Example Tab Page

`HW.Settings.page`

```php
Menu="HelloWorld:1"
Title="Settings"
Tag="myicon.png"
---
<?php

?>
```

### Field Descriptions

- `Menu`: Required when using a separate entrypoint. It references the entrypoint page file (HelloWorld) and optionally assigns a tab position (1 indicates first tab).
- `Title`: Displays as the user friendly name in the plugin interface as a tab or primary title bar.
- `Tag`: Functions similarly to `Icon` but applies to within the plugin page.

  - References an image in: `/usr/local/emhttp/plugins/<plugin-name>/icons/myicon.png`
  - Or a [Font Awesome 4 icon](https://fontawesome.com/v4/icons/) icon can be used.

### Tab Ordering

Tabs are ordered by filename, not title. To explicitly define the order, append a number to the Menu field:

`Menu="HelloWorld:3"`

This ensures the tab appears third in sequence.
