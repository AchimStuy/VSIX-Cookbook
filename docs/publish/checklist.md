---
title: Best practices checklist
description: This is a checklist to ensure your extension follows best practices before you publish it.
date: 2021-5-25
---

Here is a list of things to make sure to remember before publishing your Visual Studio extension.

## Adhere to threading rules
Add the [Microsoft.VisualStudio.SDK.Analyzers](https://www.nuget.org/packages/Microsoft.VisualStudio.SDK.Analyzers/) NuGet package to your VSIX project, which will help you discover and fix common violations of best practices regarding threading.

## Add high-quality icon
All extensions should have an icon associated with it. Make sure the icon is a high-quality .png file with the size **90x90** pixels in 96 DPI or more. After adding the icon to your VSIX project, register it in the .vsixmanifest file as both the Icon and Preview image.

## Name and description
Studies show that extensions with a short and descriptive name and an accurate description are more likely to be installed by users. Make sure the name reflects the essense of what the extension does. The short description in the .vsixmanifest file should set expectations as to what the extension does. So a brief mention of what problems it solves and what main features it has are key.

## Write good Marketplace description
This is one of the most important things you should do to make your extension successful. A good description consist of:

* Screenshots/animated GIFs of the UI added by the extension
* Detailed description of the individual features
* Links to more details if applicable

## Add license
This license will be shown on the Marketplace, in the VSIX installer and in the Extensions and Updates... dialog. One should always be specified to set the expectations for the users. Use [choosealicense.com](https://choosealicense.com/) to help find the right license for you. The reason it is important is to remove any questions and ambiguity which is important for many Visual Studio users.

## Add privacy notice
If the extension collects data such as telemetry or in any other way communicates with a remote endpoint, add a note about it in the description.

## Use KnownMonikers when possible
Visual Studio ships with thousands of icons which are available in the [KnownMonikers](https://msdn.microsoft.com/en-US/library/mt628927.aspx) collection. When adding icons to command buttons, see if you can use the existing KnownMonikers icons since they are part of a design language familiar to the Visual Studio users. Here's a full [list of KnownMonikers](http://glyphlist.azurewebsites.net/knownmonikers/) and grab the [KnownMonikers Explorer](https://marketplace.visualstudio.com/items?itemName=MadsKristensen.knownmonikersexplorer) extension to find the right one for your scenarios.

## Make it feel native to VS
Follow the same design patterns and principles that Visual Studio itself uses. This makes the extension feel natural to the users. It also reduces distractions caused by poorly designed UI. Make sure that all buttons, menus, toolbars and tool windows are only visible by default when the user is in the right context to use them. There are some rules of thumb to follow:

* Don't ever add a new top level menu (next to File, Edit, etc.)
* No buttons, menus and toolbars should be visible in contexts they don't apply to
* If [auto load](https://github.com/microsoft/VSSDK-Extensibility-Samples/tree/master/AsyncPackageMigration) is necessary (it probably isn't), do it as late as possible.
* Use [VisibilityConstraints](https://github.com/Microsoft/VSSDK-Extensibility-Samples/tree/master/VisibilityConstraints) to toggle visibility of commands instead of relying on auto load

## Use proper version ranges
It can be tempting to support versions of Visual Studio all the way back to Visual Studio 2010 to ensure that everyone can use your new extension. The problem with that is that by doing so, it is no longer possible to use any APIs introduced later than that minimum version the extension supports. Often, those new APIs are important and help improve performance and reliability of both your extension as well as Visual Studio itself.

Here are our recommendations for deciding what versions of Visual Studio to support:

* Support only the previous and current version of Visual Studio - don't support older versions if possible
* Don't specify an open ended version range. E.g. `[16.0,)`. Learn more about [version ranges](https://devblogs.microsoft.com/visualstudio/visual-studio-extensions-and-version-ranges-demystified/).