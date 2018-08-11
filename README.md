# Custom Project Settings
Enables custom scriptable settings for the Unity Editor, accessible in builds

## What does this do?
This small set of code allows you to create a `ScriptableObject` that is saved outside of the _Assets_ folder in your project, that can then be edited in the Inspector in the Unity Editor.

## Where are the files stored?
The settings files are stored as .json files, in a folder called _CustomSettings_, a sibling folder of _Assets_ and _ProjectSettings_

These settings files are automatically copied to the folder _Resources/CustomSettings_ at build time and removed on completion of the build.

## How to create your own settings file
Here's a sample for creating a settings file class:

```c#
using CustomProjectSettings;

public class ExampleSetting : CustomSettings<ExampleSetting>
{
    public bool DemoValue;

    public override void OnWillSave() { }
    protected override void OnInitialise() { }
}
```

## How to access the settings
To access the settings file, you just need to create a method hooked up to a MenuItem, then call `MySettings.Select()` on the class:
**Ensure to place this script inside and _Editor/_ folder, or use _#if UNITY_EDITOR_**
```c#
using UnityEditor;

public class SettingsDemoMenu
{
    [MenuItem("Edit/Custom Project Settings/Example Settings")]
    public static void ShowInspector()
    {
        ExampleSetting.Select();
    }
}
```

## Want custom inspector control?
You can! Inspectors are not overridden in my code.
