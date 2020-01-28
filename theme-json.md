# Global Styles - theme.json

A theme.json file is a manifest file for a WordPress theme. This file contains customizations that override the global style values from Core.

Global style values may include:

-   Core global styles
-   Core block styles

An example of a theme.json may look like this:

```json
{
	"global": {
		"color": {
			"text": "black"
		}
	},
	"blocks: {
		"core/paragraph": {
			"color": {
				"text": "pink"
			}
		}
	}
}
```

## 3rd Party Blocks

## Custom Values

A theme.json may also register unique custom values.
