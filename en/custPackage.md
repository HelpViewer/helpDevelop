# 📥 Custom package

The **📥 Custom package** feature is available in the **helpHello** help.

The functionality is provided by the 🖥️ [puiButtonCustPackage][puiButtonCustPackage] plugin.

Details on configuring the plugin can be found in the following chapters.

## Overview

The configuration is divided between the following locations:

| File | Meaning |
| --- | --- |
| plugins-config/puiButtonCustPackage__tree.cfg | Dependency tree |
| plugins-config/puiButtonCustPackage_.cfg | Component data |
| puiButtonCustPackage/*/lstr.txt | 🌐 [Translations][ViewerNewLang] of internal component names for users. The asterisk represents the language abbreviation. |

Only by adding the necessary information to all these locations will you create a fully-fledged new component.

## Dependency tree

- The file **plugins-config/puiButtonCustPackage__tree.cfg** contains a [hierarchical tree][treedata] with only internal component names.
- Each space from the left indicates one level of nesting - a component is therefore subordinate to the one above it and has one less space.

## Translations

- The file **puiButtonCustPackage/(language-abbreviation)/lstr.txt** contains a translation key named after the component from the [dependency tree][treedep].
- The value of the key is the translation that is displayed to the user.
- Everything is described in more detail in the chapter 🌐 [New Language][ViewerNewLang].

## Component data

The file **plugins-config/puiButtonCustPackage_.cfg** contains the standard [configuration][cfgPlug] format for the plugin.

### Format rules

- ⚠️ This format is very strict, so please follow the rules exactly.
- Lists in this file do not end with semicolons.
- Individual items in lists in keys are separated by semicolons.
- Entire directories end with a slash **/**.
- Files and directories are listed in relative paths to the root of the package (**hvdata/data.zip**). They do not start with any prefix.  
  For example, **styles/** is a reference to the **styles** folder inside this zip file.

### Basic data

Each component defines three basic keys here:

- **I**-NAME - Component icon
- **P**-NAME - List of plugins (plugin) and plugin instances (plugin:id)
- **F**-NAME  
  List of files and directories in the entire package data that belong to the component. Files are listed in relative paths. Entire directories end with a slash **/**. A common directory with data for the plugin (./plugin-class-name is searched for automatically by puiButtonCustPackage).

NAME = component name from [dependency tree][treedep]

### Additional data

- **C**-NAME  
  The NAME component may depend on other components listed in the list. These dependent components are automatically added to the selection if the user selects the NAME component as part of the package. The purpose of this entry is to provide a parallel text definition to the [dependency tree][treedep] that better captures cases where a component depends on multiple other components at the same time. This key is optional and does not need to be specified.
- **DE**  
  List of plugins that are always removed from the resulting package prepared by this functionality for users.  
  For example, after executing this functionality, the user always receives a package that no longer supports the creation of another custom package.
- **DE-(plugin-class-name)**  
  List of plugins that are removed if the **(plugin-class-name)** plugin is completely removed from the package.  
  For example, **pIndexFile** and its support for **working with keywords and dictionary overview pages**.

[puiButtonCustPackage]: :_plg:puiButtonCustPackage.md "puiButtonCustPackage"
[ViewerNewLang]: newLangViewer.md#h-3-1 "New language for Viewer"
[treedata]: ?d=hlp-aguide/Help-__.zip&p=mdata%2Ftree.lst.md "Tree structure data format"
[cfgPlug]: pluginConfig.md "Plugin configuration"
[treedep]: #h-2-1 "Dependency tree"
