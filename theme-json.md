# Global Styles - theme.json

A `theme.json` file is a manifest file for a WordPress theme. This file contains customizations that override the global style values from Core.

## Location

It is located in the root directory of a WordPress theme, example:

```
/wp-content/
	\- my-theme/
		|- functions.json
		|- ...
		|- style.css
		\- theme.json
```

## Global Styles "Opt-in"

For initial development, themes x Global Styles will rely on an opt-in mechanic. If a `theme.json` file is present, the theme has opted into the Global Styles system.

## Schema

The JSON Object shape in the `theme.json` represents the data structure the Global Style system uses internally. Values within a `theme.json` override core values by extension, not direct mutation.

An example of a theme.json may look like this:

```json
{
	"global": {
		"color": {
			"text": "black"
		}
	},
	"blocks": {
		"core/paragraph": {
			"color": {
				"text": "pink"
			}
		}
	}
}
```

In the example (above), there are 2 keys are the root level:

-   `global`
-   `blocks`

### `global`

The `global` key allows for the theme to customize **non-block specific** base global style values.

### `blocks`

The `blocks` key allows for the theme to customize **block specific** global style values.

The example (above) also demonstrates how a core block may be customized. In this case the `core/paragraph` block.

The `key` represents the unique namespace for a given Gutenberg block.

#### 3rd Party Blocks

This structure allows for a `theme.json` to provide values for 3rd party blocks as well. For example:

```json
{
	"global": {
		"color": {
			"text": "black"
		}
	},
	"blocks": {
		"core/paragraph": {
			"color": {
				"text": "pink"
			}
		},
		"my-custom-block-library/maps": {
			"color": {
				"title": "blue"
			}
		}
	}
}
```
