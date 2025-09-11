# 🔎 HelpViewer Project

## Organization

Organization [HelpViewer][HelpViewer] contains 2 basic types of repositories:

- Basic project repositories - Viewer, translations, another service repositories
- Help files repositories (**help\***)

## Basic repositories

| Repository | Content |
|---|---|
| [HelpViewer][RHelpViewer] | Base repository of project - help files viewer. |
| [Translations][RTranslations] | Language translation strings for UI of HelpViewer. Repository is inserted to **HelpViewer** as a Git submodule. It is also one of the sources of language list which is offered to user for language selection of UI and help file version. |
| [.github][R.github] | Base repository of organization with operational information. |
| [helpviewer.github.io][RWebHello] | GitHub Pages project for web presentation. [CI deployment script][RWebHelloDeploy] will do page content update with defined version number to deploy. |
| [fulltextSearchDBBuilder][FTSIndexBuilder] | Full text index generator logic. This Bash script is used by CI scripts which handles publishing of help files in case there is required to create full text index. |
| [helpTemplate][RhelpTemplate] | Template for help file project. It is intended for help authors as a basic blank project. |
| [prism][RPrism] | PrismJS library mixed-customized release. Repository is inserted to **HelpViewer** as a Git submodule. |

## Help files repositories

Repository names are starting with **help\***. Due to the naming of the project, there are exceptions as described above.

| Repository | Content |
|---|---|
| [helpHello][RhelpHello] | Project hello help file for public web presentation. |
| [helpUser][RhelpUser] | Help file with starting instruction, UI description for HelpViewer users. It describes basic work with Viewer. |
| [helpAuthorsGuide][RhelpAuthorsGuide] | (This) Help file (pages) for help file authors. Describes all necessary steps for creation and publishing of your own help file. |

## Version publishing

- Versions are released irregularly
- The version number is always the date of the release in yearmonthday format (for example: 20250621)
- If more than one version is released on a given day, then the first version has the format yearmonth and each subsequent version has the suffix **-number** starting from 1 with step 1, for example: 20250606-1, 20250606-2
- The data for describing version changes is obtained from **CHANGELOG.md** in the root of the repository. The description for the latest version is always appended to the beginning of the file. The oldest versions tend to be lowest in the listing. Do not change or remove the last section with “**File introduced**” - it is also for your information
- This procedure applies to **HelpViewer** as well as other tools and issued help
- The same procedure is also recommended for authors of help files, although they are free to decide this point on their own

[HelpViewer]: https://github.com/HelpViewer "HelpViewer"
[RHelpViewer]: https://github.com/HelpViewer/HelpViewer "HelpViewer"
[RTranslations]: https://github.com/HelpViewer/Translations "Translation"
[RWebHello]: https://github.com/HelpViewer/helpviewer.github.io "Project web presentation"
[RWebHelloDeploy]: https://github.com/HelpViewer/helpviewer.github.io/actions/workflows/toPages.yml "Project web presentation - deployment"
[FTSIndexBuilder]: https://github.com/HelpViewer/fulltextSearchDBBuilder "Full text index builder"
[RhelpTemplate]: https://github.com/HelpViewer/helpTemplate "Help file project template"
[RhelpHello]: https://github.com/HelpViewer/helpHello
[RhelpUser]: https://github.com/HelpViewer/helpUser
[RhelpAuthorsGuide]: https://github.com/HelpViewer/helpAuthorsGuide
[R.github]: https://github.com/HelpViewer/.github "Repository with basic information"
[RPrism]: https://github.com/HelpViewer/prism
