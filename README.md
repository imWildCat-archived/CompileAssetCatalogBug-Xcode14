# CompileAssetCatalogBug

Xcode Version 14.0 beta (14A5228q) has a bug which prevents some SVG images from building into apps.

## Repro Steps

1. Clone this project
2. Open this project using Xcode 14.0 beta
3. Build the app

If you cannot repro, you can try different simulator targets.

A second build may succeeds.

## Potential Reason

Per my quick investigation, it might be related to svg `filter`:

```svg
<svg width="230" height="120" xmlns="http://www.w3.org/2000/svg">
  <filter id="blurMe">
    <feGaussianBlur stdDeviation="5" />
  </filter>
  <circle cx="60" cy="60" r="50" fill="green" />
  <circle cx="170" cy="60" r="50" fill="green" filter="url(#blurMe)" />
</svg>
```

```shell
CompileAssetCatalog /Users/[username]/Developer/xcode_projects/demos/CompileAssetCatalogBug/DerivedData/CompileAssetCatalogBug/Build/Products/Debug-iphonesimulator/CompileAssetCatalogBug.app /Users/[username]/Developer/xcode_projects/demos/CompileAssetCatalogBug/CompileAssetCatalogBug/Assets.xcassets (in target 'CompileAssetCatalogBug' from project 'CompileAssetCatalogBug')
    cd /Users/[username]/Developer/xcode_projects/demos/CompileAssetCatalogBug
    /Applications/Xcode-beta.app/Contents/Developer/usr/bin/actool --output-format human-readable-text --notices --warnings --export-dependency-info /Users/[username]/Developer/xcode_projects/demos/CompileAssetCatalogBug/DerivedData/CompileAssetCatalogBug/Build/Intermediates.noindex/CompileAssetCatalogBug.build/Debug-iphonesimulator/CompileAssetCatalogBug.build/assetcatalog_dependencies --output-partial-info-plist /Users/[username]/Developer/xcode_projects/demos/CompileAssetCatalogBug/DerivedData/CompileAssetCatalogBug/Build/Intermediates.noindex/CompileAssetCatalogBug.build/Debug-iphonesimulator/CompileAssetCatalogBug.build/assetcatalog_generated_info.plist --app-icon AppIcon --accent-color AccentColor --compress-pngs --enable-on-demand-resources YES --filter-for-device-model iPhone12,1 --filter-for-device-os-version 16.0 --development-region en --target-device iphone --target-device ipad --minimum-deployment-target 16.0 --platform iphonesimulator --compile /Users/[username]/Developer/xcode_projects/demos/CompileAssetCatalogBug/DerivedData/CompileAssetCatalogBug/Build/Products/Debug-iphonesimulator/CompileAssetCatalogBug.app /Users/[username]/Developer/xcode_projects/demos/CompileAssetCatalogBug/CompileAssetCatalogBug/Assets.xcassets

'cyclone' is not a recognized processor for this target (ignoring processor)
'cyclone' is not a recognized processor for this target (ignoring processor)
'cyclone' is not a recognized processor for this target (ignoring processor)
'cyclone' is not a recognized processor for this target (ignoring processor)
'cyclone' is not a recognized processor for this target (ignoring processor)
'cyclone' is not a recognized processor for this target (ignoring processor)
'cyclone' is not a recognized processor for this target (ignoring processor)
'cyclone' is not a recognized processor for this target (ignoring processor)
'cyclone' is not a recognized processor for this target (ignoring processor)
'cyclone' is not a recognized processor for this target (ignoring processor)
'cyclone' is not a recognized processor for this target (ignoring processor)
'cyclone' is not a recognized processor for this target (ignoring processor)
'cyclone' is not a recognized processor for this target (ignoring processor)
'cyclone' is not a recognized processor for this target (ignoring processor)
'cyclone' is not a recognized processor for this target (ignoring processor)
'cyclone' is not a recognized processor for this target (ignoring processor)
'cyclone' is not a recognized processor for this target (ignoring processor)
'cyclone' is not a recognized processor for this target (ignoring processor)
'cyclone' is not a recognized processor for this target (ignoring processor)
'cyclone' is not a recognized processor for this target (ignoring processor)
'cyclone' is not a recognized processor for this target (ignoring processor)
'cyclone' is not a recognized processor for this target (ignoring processor)
'cyclone' is not a recognized processor for this target (ignoring processor)
'cyclone' is not a recognized processor for this target (ignoring processor)
'cyclone' is not a recognized processor for this target (ignoring processor)
'cyclone' is not a recognized processor for this target (ignoring processor)
'cyclone' is not a recognized processor for this target (ignoring processor)
'cyclone' is not a recognized processor for this target (ignoring processor)
'cyclone' is not a recognized processor for this target (ignoring processor)
'cyclone' is not a recognized processor for this target (ignoring processor)
'cyclone' is not a recognized processor for this target (ignoring processor)
'cyclone' is not a recognized processor for this target (ignoring processor)
'cyclone' is not a recognized processor for this target (ignoring processor)
'cyclone' is not a recognized processor for this target (ignoring processor)
'cyclone' is not a recognized processor for this target (ignoring processor)
'cyclone' is not a recognized processor for this target (ignoring processor)
'cyclone' is not a recognized processor for this target (ignoring processor)
'cyclone' is not a recognized processor for this target (ignoring processor)
'cyclone' is not a recognized processor for this target (ignoring processor)
'cyclone' is not a recognized processor for this target (ignoring processor)
'cyclone' is not a recognized processor for this target (ignoring processor)
'cyclone' is not a recognized processor for this target (ignoring processor)
Command CompileAssetCatalog failed with a nonzero exit code
```
