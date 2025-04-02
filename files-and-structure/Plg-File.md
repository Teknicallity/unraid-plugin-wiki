## Overview

The `.plg` file is used by Unraid to install the plugin. Each plugin has its own `.plg` file which  contains the plugin details, install scripts, and removal scripts.

## Location

The location of the plg file matters less since it is only used for the installation of a plugin, rather than used in the plugin. Most plugins store it in the root of their plugin repository, next to the source code folder.

Once it is installed, the `.plg` file is stored in `/boot/config/plugins`.

## Format

The file is in an xml format, with some Unraid customization. The file is referenced by [an XML template](/files-and-structure/XML-Unraid-Template.md) to install the plugin.
