# WebBrowserComponentTS

[🧪Experimental] Extend juce::BrowserComponent for stronger TypeScript support

## ✨ Features

- Output detailed type file
  - [x] `withNativeFunction` (id only)
- JSON-based type definitions for parameters and other events (no yet)

## ⛳ Examples

Source/PluginEditor.h

```cpp
    WebBrowserComponentTS webComponent{
        WebBrowserComponentTS::getSourcePath("../webview/src/types").getFullPathName(),
        "juce.d.ts",
        "juce-framework-frontend-mirror",
        juce::WebBrowserComponent::Options{}
        .withBackend(juce::WebBrowserComponent::Options::Backend::webview2)
        .withWinWebView2Options(
            juce::WebBrowserComponent::Options::WinWebView2{}
            .withUserDataFolder(juce::File::getSpecialLocation(
                juce::File::SpecialLocationType::tempDirectory))
            )
            .withOptionsFrom(gainRelay)
            .withOptionsFrom(controlParameterIndexReceiver)
            .withInitialisationData("name", juce::var{ "mimoz" })
            .withNativeFunction ("sayHello",
                [](auto& var, auto complete)
                {
                    complete ("Hello " + var[0].toString());
                }
            )
    };
```

webview/tsconfig.json
```json
{
  "compilerOptions": {
    // ...
    "types": [
      "src/types/juce.d.ts"
    ],
  }
}

```
