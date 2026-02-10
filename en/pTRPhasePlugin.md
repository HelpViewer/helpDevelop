# 🖼️ pTRPhasePlugin

## Purpose of the plugin

The plugin receives the ⚡ [ShowChapterResolutions][ShowChapterResolutions] event from the 🖼️ [pTopicRenderer][cpTopicRenderer] and performs a single step of process processing. The pTopicRenderer plugin has a list of process phases defined in its configuration and ensures that individual messages go through the entire process.

## Implementation

1. In the **plugins.lst** file, add the following line:
pConvertSysEventToEvent:[instanceid]
2. Prepare the following code in the **plugins/[plugin name].js** file, for example:

```javascript
class pTRNewPlugin extends pTRPhasePlugin {
  onETShowChapterResolutions(r) {
  }
}

Plugins.catalogize(pTRNewPlugin);
```

onETShowChapterResolutions is responsible for performing the process step. The parameter r is the event ⚡ [ShowChapterResolutions][ShowChapterResolutions]. The event itself contains all supporting objects and methods for loading, preparing, or executing the text listing into the output HTML element for the chapter. 

### ShowChapterResolutions - selected properties

| Property | Description |
|---|---|
| doc | Link to the specific HTML element that will receive the listing output |
| getStorageData | Link to the function for reading the source specified by the plugin 🖼️ [pTRTriage][pTRTriage] based on chapter URI patterns and other data. |
| tokens | Tokens (strings) collected during previous processing steps. It is possible to create a token in one step and process it in another step and perform additional logic. |
| onTokenDo | Tests whether the specified token exists. If so, it removes it and performs the embedded function. |
| preventDefault | Allows you to call preventDefault on a JavaScript system event. The call is irreversible according to the standard. |
| stopAllPhases | Setting this to **true** will interrupt further processing of the process. Combine with **stop = true**. |

> [!WARNING] Asynchronicity is used within the process. Always call it as follows:  
r.result = r.result.then(() => ...);  
so that the individual steps follow each other.  
You can also attach multiple events to the same result object, but it is recommended to sequence the steps one after the other.

## Implementation examples

- 🖼️ [pTREmptyPlugin][pTREmptyPlugin]
- 🖼️ [pTRParseMd][pTRParseMd]
- 🖼️ [pTRLoadData][pTRLoadData]

## Another plugins

- 🖼️ [pTopicRenderer][pTopicRenderer]

[pTRTriage]: :inst:pTRTriage:-triage.md "pTRTriage"
[pTREmptyPlugin]: :inst:pTREmptyPlugin:-htm.md "pTREmptyPlugin"
[ShowChapterResolutions]: :_evt:ShowChapterResolutions.md "ShowChapterResolutions"
[cpTopicRenderer]: pTopicRenderer.md "pTopicRenderer"
[pTopicRenderer]: :_plg:pTopicRenderer.md "pTopicRenderer"
[pTRParseMd]: :_plg:pTRParseMd.md "pTRParseMd"
[pTRLoadData]: :_plg:pTRLoadData.md "pTRLoadData"
