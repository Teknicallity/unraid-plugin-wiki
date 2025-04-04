## Overview

This document covers the short description that accompanies a plugin in Unraid's *Plugin* tab.

Note that this is different than the description shown when searching and installing a plugin through the community applications, or *Apps* tab.

## Location

To fill the short description, Unraid looks for a readme file in the plugin source directory:

`/usr/local/emhttp/plugins/<plugin-name>/README.md`

## Creation

The two ways most plugins set up this file are as follows:

- Include the the `README.md` file in the source directory of the plugin repository.
- Create the file on plugin installation through the `.plg` file.

The primary reason for option 2 is to not clutter up the source directory with non-code files.

To make the readme file on installation, include this in your `.plg` file:

```xml
<FILE Name="/usr/local/emhttp/plugins/<plugin-name>/README.md">
<INLINE>
**Plugin**

Short description for ReadMe
</INLINE>
</FILE>
```
