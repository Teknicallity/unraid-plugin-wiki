## Overview

This document shows how to build and install an Unraid plugin from source using either a tarball or a Slackware .txz package.

## Archive Naming

Plugin archives should follow the naming format:

`<plugin-name>-<YYYY.MM.DD>[version-character]`

Example:

`hello.world-1970.01.01c`

## Method 1: General Linux Installation (Tarball)

This method uses a compressed tarball (.tar.gz or .tgz) to install your plugin.

### Requirements

- Any common linux based distro

### Step-by-Step

1. Create a tarball from the source code directory

    From within the plugin's source directory, run:

    ```bash
    tar -czvf ../[archive-dir/]<plugin-name>-<date>[version-character].tgz .
    ```

2. Transfer the tarball to Unraid.

    Copy the tarball to yuor Unraid servet at: `/boot/config/plugins/<plugin-name>/`

    Suggested tools (require SSH access):
    - Rsync:

      ```bash
      rsync "<tarball>" "[root@]<unraid-ip>:/boot/config/plugins/<plugin-name>/"
      ```

    - SCP:

      ```bash
      scp "<tarball>" [root@]<unraid-ip>:/boot/config/plugins/<plugin-name>/
      ```

3. Add install script logic to your `.plg` file
    ```xml
    <FILE Run="/bin/bash">
    <INLINE>
    tar -xf /boot/config/plugins/<!--plugin name-->/<!--tarball--> -C /usr/local/emhttp/plugins/<!--plugin name-->/ 2&gt;/dev/null
    </INLINE>
    </FILE>
    ```

4. Transfer the .plg file to Unraid under `/boot`

5. Install the plugin in Unraid
    1. Go to the **Plugins** tab
    2. Navigate to the **Install Plugin** sub-tab
    3. Scroll down if needed, click your `.plg` file, and press **Install**

## Method 2: Slackware Installation (Slackware TXZ Package)

Slackware-compatible packages are suitable for systems like Unraid, which is based on Slackware. This method uses .txz archives.

### Requirements

You will need some a slackware based installation to complete this method. One of the following are suitable:

- [WSL2 Slackware](https://apps.microsoft.com/detail/9N8WPJWZ4JX7)
- Virtual machine running slackware
- Other methods I don't know about, just anything with Slackware's `slackpkg` suite.

### Step-by-Step

1. Prepare a temporary staging directory

    In the project root:

    ```bash
    mkdir tmp
    ```

2. Create the plugin directory structure

    ```bash
    mkdir -p ./tmp/usr/local/emhttp/plugins/<plugin-name>
    ```

3. Copy plugin files into the staging area

    From within the plugin's source directory:

    ```bash
    cp --parents -f $(find . -type f) ../tmp/usr/local/emhttp/plugins/<plugin-name>
    ```

4. Build the `.txz` package

    Change into the staging directory:

    ```bash
    cd ../tmp
    makepkg --linkadd y --chown y ../[archive-dir/]<plugin-name>-<date>[version-character].txz
    ```

5. Generate MD5 hash

    ```bash
    cd ..
    md5sum "<package>" | awk '{print $1}'
    ```

6. Transfer the package to Unraid

    Copy the `.txz` archive to:

    ```bash
    /boot/config/plugins/<plugin-name>/
    ```

    Suggested tools (require SSH access):
    - Rsync:

      ```bash
      rsync "<tarball>" "[root@]<unraid-ip>:/boot/config/plugins/<plugin-name>/"
      ```

    - SCP:

      ```bash
      scp "<tarball>" [root@]<unraid-ip>:/boot/config/plugins/<plugin-name>/
      ```

7. Add install script logic to your `.plg` file

    ```bash
    <FILE Name="/boot/config/plugins/&pluginName;/&pluginName;-&version;.txz" Run="upgradepkg --install-new">
      <MD5><!--md5 hash--></MD5>
    </FILE>
    ```

8. Transfer the .plg file to Unraid under `/boot`

9. Install the plugin in Unraid
    1. Go to the **Plugins** tab
    2. Navigate to the **Install Plugin** sub-tab
    3. Scroll down if needed, click your `.plg` file, and press **Install**
