# 🖼️ pTopicRenderer

## Purpose of the plugin

This plugin is suitable for managing simple, linear processes organized into phases.

## Implementation

The plugin is extensible like other objects, but only configuration definitions are recommended.

🖼️ [pTopicRenderer][pTopicRenderer]

## Configuration

| Name | Default value | Description |
|---|---|---|
| IDCONTENT | content | ID of the HTML element that will usually be the recipient of the plugin process output. |
| PHASELIST | triage;load;%%;... | List and order of phases to be performed within the process. |

## Functionality description

If the application is running in [debug mode][debug], the plugin logs its activity and individual intermediate steps of the phases.

1. The plugin receives the event ⚡ [ShowChapter][ShowChapter]
2. The plugin prepares the event object ⚡ [ShowChapterResolutions][ShowChapterResolutions] by providing:
   - a link to read the application data store
   - a link to read the help data store
   - a link to read the network location storage of the original GitHub repository, if the help data contains it
   - the path to the help file
   - a link to the HTML element into which the final formatted chapter output will be written
   - determines the data medium (local file, directory, zip file, network location)
   - specifies the chapter file type
3. Takes the value **PHASELIST**, where:
   - %% is always replaced with the first three characters of the input chapter file extension without the dot (md, htm).
   - it splits the names by semicolons
4. The **ShowChapterResolutions** object sends to the event system sequentially to groups of plugins by name: **(alias)-(phase)**. The alias here is the **id** of the plugin instance. Plugins receive this object for processing within a single phase in the order in which they are written in the [plugin list][plugList].  
It is recommended that each phase have at least one plugin defined. If a phase is not suitable for a given process, but you do not want to remove it, define the plugin instance 🖼️ [pTREmptyPlugin][pTREmptyPlugin].
5. After completing all steps (handled by descendants 🖼️ [pTRPhasePlugin][pTRPhasePlugin]), it sends the event ⚡ [ChapterShown][ChapterShown], which is usually received by the plugin 🧩 [pAppmainNext][pAppmainNext], which is the main plugin of the application and has a handler for this event.

## Implementation examples

- Listing the chapter content to the user
- Preparing a full-text dictionary if a pre-generated dictionary from the CI/CD script is not available in the help

[pTopicRenderer]: :_plg:pTopicRenderer.md "pTopicRenderer"
[pAppmainNext]: :_plg:pAppmainNext.md "pAppmainNext"
[ShowChapter]: :_evt:ShowChapter.md "ShowChapter"
[ChapterShown]: :_evt:ChapterShown.md "ChapterShown"
[ShowChapterResolutions]: :_evt:ShowChapterResolutions.md "ShowChapterResolutions"
[pTRPhasePlugin]: pTRPhasePlugin.md "pTRPhasePlugin"
[plugList]: plugins.lst.md "List of plugins"
[pTREmptyPlugin]: :_cpp:pTREmptyPlugin.md "Empty plugin"
[debug]: debug.md "Debug mode"
