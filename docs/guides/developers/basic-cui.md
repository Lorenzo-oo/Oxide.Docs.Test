---
title: Basic CUI
after: coroutines
---
# Structure

UI element consists of its name, which should be a unique identifier (using duplicate names may cause issues), 
parent, which is the name of element parent (Example: Background is a parent of Table, and Table is a parent of cells), fade out time in seconds and components, 
which are the properties of your element.

## Components

There are multiple available components. Some are required, some are not. 
Rust client will use some default values when fields are needed but not defined by the UI

### `CuiRectTransformComponent`
Position of the element  

| Field | Type | Description |
| :---------- | :-------- | :-------------------------------------------------------- |  
| AnchorMin | String | The lower left corner, see [UI position](./basic-cui#ui-position) default: "0.0 0.0" |  
| AnchorMax | String | the upper right corner  default: "1.0 1.0"      |  
| OffsetMin | String | Lower left corner, in pixels, relative to AnchorMin. default: "0.0 0.0" |  
| OffsetMax | String | Upper right corner, in pixels, relative to AnchorMin. default: "0.0 0.0" |  
| ~~rotation~~ | String | rotation point angle. default to "0.0" |  
| ~~setParent~~ | string | if updateflag, define parent panel |
| ~~setTransformIndex~~ | int | if updateflag, define transform index |

```csharp
CuiRectTransformComponent { AnchorMin = "0.5 0.5",  AnchorMax = "0.5 0.5", OffsetMin="-100 -20", OffsetMax="100 20" }
```

### `CuiNeedsCursorComponent`
Show a cursor that will let you click buttons and such.  

```csharp
CuiNeedsCursorComponent()
```

### `CuiNeedsKeyboardComponent`
 Keyboard input is needed for this UI.  

```csharp
CuiNeedsKeyboardComponent()
```

### `CuiImageComponent` 
Image with a sprite, material, color and cache.  

| Field | Type | Description |
| :---------- | :-------- | :-------------------------------------------------------- |
| Color | String | Color Field in RGBA format see [colors](./basic-cui#colors)  |
| FadeIn | float | Fadein time in seconds  |
| ImageType | Image.Type | see [image-type](./basic-cui#image-type)  |
| ItemId | int | Item ID, see [RustHelp Item list](https://rusthelp.com/tools/admin/item-list) |
| Material | String | Material of background [Material](./basic-cui#material)  |
| Png | String | Png image  |
| SkinId | ulong | Skin ID  |
| Sprite | String | see [Image/Icon](https://github.com/OrangeWulf/Rust-Docs/blob/master/Extended/UI.md#imagesicons) |
| ~~FillCenter~~ | bool | If true, render the center of a Tiled or Sliced image. |

```csharp
CuiImageComponent 
{ 
	Color = "0.30 0.30 0.30 1.0", 
	FadeIn = 0.1f,	
	Material = "assets/content/ui/uibackgroundblur.mat" 
}
```

### `CuiRawImageComponent`
 Raw image with a sprite, material, color, URL and cache.  

| Field | Type | Description |
| :---------- | :-------- | :-------------------------------------------------------- |
| Color | String | Color Field in RGBA format see [colors](./basic-cui#colors)  |
| FadeIn | float | Fadein time in seconds  |
| Material | String | Material of background [Material](./basic-cui#material)  |
| Png | String | png image ID |
| Sprite | String | Sprite image  |
| SteamId | String | steam id of the avatar image  |
| Url | String | URL of the raw image  |

```csharp
CuiRawImageComponent 
{ 
	Color = "0.30 0.30 0.30 1.0", 
	FadeIn = 0.1f,
	Material = "assets/content/ui/uibackgroundblur.mat"
}
```

### `CuiButtonComponent` 
Button with command to execute, and other atttributes.  

| Field | Type | Description |
| :---------- | :-------- | :-------------------------------------------------------- |
| Close | String | UI name to close  |
| Color | String | Color Field in RGBA format see [colors](./basic-cui#colors)  |
| Command | String | Command to execute when button is pressed  |
| FadeIn | float | Fadein time in seconds  |
| ImageType | Image.Type | see [image-type](./basic-cui#image-type)  |
| Material | String | Material of background, see [Material](./basic-cui#material)  |
| Sprite | String | see [Image/Icon](https://github.com/OrangeWulf/Rust-Docs/blob/master/Extended/UI.md#imagesicons) |
| ~~normalColor~~ | String |  |
| ~~highlightedColor~~ | String |  |
| ~~pressedColor~~ | String |  |
| ~~selectedColor~~ | String |  |
| ~~disabledColor~~ | String |  |
| ~~colorMultiplier~~ | float |  |
| ~~fadeDuration~~ | float |  |


```csharp
CuiButtonComponent 
{
	Color = "0.20 0.30 0.40 1.0", 
	Command = "CommandName",
	Close = "UI.ClosePanelName",
	Material = "assets/icons/iconmaterial.mat"
}
```

### `CuiInputFieldComponent` 
Input field with default text attributes and command to run  

| Field | Type | Description |
| :---------- | :-------- | :-------------------------------------------------------- |
| Command | String | Command to execute when button is pressed  |
| Text | String |  current value of the input field  |
| Font | String | see [fonts](./basic-cui#fonts)  |
| FontSize | int | Size of font  |
| Color | String | Color Field in RGBA format see [colors](./basic-cui#colors)  |
| Align | TextAnchor | see [Align](./basic-cui#align)  |
| Autofocus | bool | true or false  |
| CharsLimit | int | maximum number of char, 0 = infinite  |
| HudMenuInput | bool | true or false  |
| IsPassword | bool | true or false  |
| placeholderId | string | Id to identify field and link to other element |
| LineType | InputField.LineType | see [InputField.LineType](./basic-cui#inputfield-linetype)  |
| NeedsKeyboard | bool | true or false  |
| ReadOnly | bool | Set the InputField to be read only |

#### `InputField.LineType`
* `TextAnchor.SingleLine`
* `TextAnchor.MultiLineSubmit`
* `TextAnchor.MultiLineNewline`

```csharp
CuiInputFieldComponent 
{
	Align = TextAnchor.MiddleCenter, 
	CharsLimit = 300, 
	Command = "CommandName", 
	FontSize = 20, 
	IsPassword = false, 
	Text = "Input field" 
}
```

### `CuiTextComponent` 
Text with value, font size, font, text align and color.  

| Field | Type | Description |
| :---------- | :-------- | :-------------------------------------------------------- |
| Text | String | Text to display  |
| Font | String |  see [fonts](./basic-cui#fonts) |
| FontSize | int | Size of font  |
| Color | String | Color Field in RGBA format see [colors](./basic-cui#colors)  |
| Align | TextAnchor | see [Align](./basic-cui#align)  |
| FadeIn | float | Fadein time in seconds  |
| VerticalOverflow | VerticalWrapMode | VerticalWrapMode.Truncate or VerticalWrapMode.Overflow  |

```csharp
CuiTextComponent 
{ 
	Text = "Workbench view", 
	FontSize = 24, 
	Align = TextAnchor.MiddleCenter, 
	Color ="1 0 0 1" 
}
```

### `CuiOutlineComponent` 
Outline for an element with parameters.  

| Field | Type | Description |
| :---------- | :-------- | :-------------------------------------------------------- |
| Color | String | Color Field in RGBA format see [colors](./basic-cui#colors)  |
| Distance | String | Number of pixels for outline size  |
| UseGraphicAlpha | bool | if present, use graphic alpha  |

```csharp
CuiOutlineComponent 
{ 
	Distance = "1.0 1.0", 
	Color = "1 1 1 1" 
}
```

### `CuiCountdownComponent` 
Countdown that send a command at the end of count  
&emsp;

| Field | Type | Description |
| :---------- | :-------- | :-------------------------------------------------------- |
| Command | String | Command to execute when countdown terminates |
| DestroyIfDone | bool |  |
| StartTime | float | Initial time of the counter |
| EndTime | float | End time of the countter |
| Step | float | Value to increase/decrement the counter  |
| FadeIn | float | Fadein time in seconds  |
| Interval | float | timer update interval. Min interval is 0.02 ( 50 times per sec ) |
| NumberFormat | String | format, default is "0.####"  |
| TimerFormat | TimerFormat | None(default), SecondsHundreth, MinutesSeconds, MinutesSecondsHundreth, HoursMinutes, HoursMinutesSeconds, HoursMinutesSecondsMilliseconds, HoursMinutesSecondsTenths, DaysHoursMinutes, DaysHoursMinutesSeconds |

```csharp
CuiCountdownComponent Countdown = new CuiCountdownComponent
{
	TimerFormat = TimerFormat.HoursMinutesSeconds,
	Step = 1, EndTime = 0f, StartTime = 100f, Interval = 1f, FadeIn=2.0f,
	Command = "Cmd.CountdownUi " + player.userID.ToString()
};

elements.Add(new CuiElement
{
	Name = "NameOfElement", 
	Parent = "NameOfPanel", 
	FadeOut = 1.0f
	Components =
	{
	new CuiTextComponent{Text="Time left : %TIME_LEFT%", FontSize=14, Font="RobotoCondensed-Bold.ttf", Align=TextAnchor.MiddleCenter, Color="1.0 1.0 1.0 1.0" },
	Countdown
	}
});
```
   
### `CuiScrollViewComponent`
Scroll component with parametrization  
&emsp;

| Field | Type | Description |
| :---- | :---- | :-------------------------------------------------------- |
| ContentTransform | CuiRectTransform | Rectangle definition of the window |
| DecelerationRate | float | Deceleration rate |
| Elasticity | float | Elasticity |
| Inertia | bool | Inertia |
| MovementType | ScrollRect. MovementType | Unrestricted, Elastic, Clamped |
| ScrollSensitivity | float | Scroll Sensitivity |
| Horizontal | bool | Enable horizontal scrollbar |
| Vertical | bool | Enable vertical scrollbar |
| HorizontalScrollbar | CuiScrollbar | Parameters to define the scrollbar [see CuiScrollbar](./basic-cui#cuiscrollbar) |
| VerticalScrollbar | CuiScrollbar | Parameters to define the scrollbar [see CuiScrollbar](./basic-cui#cuiscrollbar) |
| horizontalNormalizedPosition | float | horizontal scroll position as a value between 0.0 and 1.0, with 0 being at the left. |
| verticalNormalizedPosition | float | vertical scroll position as a value between 0.0 and 1.0, with 0 being at the bottom. |

```csharp
CuiElementContainer createScrollUI()
{
	CuiElementContainer elements = new CuiElementContainer();

	string mainpanel = elements.Add(new CuiPanel
	{
		Image = { Color = "0.3 0.3 0.6 0.8" },
		RectTransform = { AnchorMin = "0.5 0.5", AnchorMax = "0.5 0.5", OffsetMin = "-200 -300", OffsetMax = "200 300" },
	}, "Overlay", UIScrollName, UIScrollName);

	elements.Add(new CuiElement
	{
		Name = "panel1",
		Parent = UIScrollName,
		Components =
			{
				new CuiRawImageComponent { Sprite = "assets/content/effects/crossbreed/fx gradient skewed.png", Color = "0.1 0.1 0.1 1.0" },
				new CuiRectTransformComponent { AnchorMin = "0.015 0.015", AnchorMax = "0.985 0.985" }
			}
	});

	elements.Add(new CuiElement
	{
		Parent = "panel1",
		Components =
			{
				new CuiTextComponent { Text = "Scroll example", FontSize=12, Align=TextAnchor.MiddleCenter },
				new CuiRectTransformComponent { AnchorMin = "0 1", AnchorMax = "1 1", OffsetMin = "0 -50", OffsetMax = "0 0" }                    
			}
	});

	elements.Add(new CuiButton
	{
		Button = { Color = "0.8 0.2 0.2 0.8", Command = "closescroll" },
		RectTransform = { AnchorMin = "0.91 0.93", AnchorMax = "0.98 0.98" },
		Text = { Text = "Close", FontSize = 8, Align = TextAnchor.MiddleCenter }
	}, mainpanel);

	CuiScrollViewComponent scrollUI = new CuiScrollViewComponent
	{
		ContentTransform = new CuiRectTransform { AnchorMin = "0 0.9", AnchorMax = "1 0.9", OffsetMin = "0 -1200", OffsetMax = "0 0" },
		Vertical = true,
		Horizontal = false,
		MovementType = ScrollRect.MovementType.Clamped,
		Elasticity = 0.25f,
		Inertia = true,
		DecelerationRate = 0.3f,
		ScrollSensitivity = 24f,
		VerticalScrollbar = new CuiScrollbar { AutoHide = true, Size = 20 },
		HorizontalScrollbar = new CuiScrollbar { AutoHide = true, Size = 20 },
	};

	elements.Add(new CuiElement
	{
		Name = "Scroller",
		Parent = "panel1",
		Components =
			{
			new CuiRawImageComponent { Sprite = "assets/content/effects/crossbreed/fx gradient skewed.png", Color = "0.15 0.25 0.25 0.8" },
			scrollUI,
			new CuiRectTransformComponent {AnchorMin = "0 0", AnchorMax = "1 1", OffsetMax = "0 -50" },
			new CuiNeedsCursorComponent()
			}
		});

	int scrollSpacing = 28;
	int scrollSize = 24;
  
	for ( int i=0; i<40; i++) 
	{
		Puts($"OffsetMin =  {-i * scrollSpacing} /  OffsetMax =  {-i * scrollSpacing - scrollSize}");
		elements.Add(new CuiElement
		{
			Name = "Text_" + i,
			Parent = "Scroller",
			Components =
			{
			new CuiRawImageComponent { Color = "0.2 0.2 0.2 1.0", Sprite = "Assets/Content/UI/UI.Background.Tile.psd" },
			new CuiRectTransformComponent { AnchorMin = "0.03 0.97", AnchorMax = "0.75 0.97", OffsetMin = $"0 {-i*scrollSpacing-scrollSize}", OffsetMax = $"0 {-i*scrollSpacing}"},
			new CuiOutlineComponent { Distance= "2 2", Color= "0 0 0 0.06" },
			new CuiOutlineComponent { Distance= "4 4", Color= "0 0 0 0.025" },
			}
		});

		elements.Add(new CuiElement
		{
			Parent = "Text_" + i,
			Components =
			{
			new CuiTextComponent { Text = $"Item #{i+1}", Color = "0.95 0.95 0.95 1.0", FontSize = 10, Align = TextAnchor.MiddleLeft },          
			}
		});

		elements.Add(new CuiElement
		{
			Name = "Button_" + i,
			Parent = "Scroller",
			Components =
			{
			new CuiRawImageComponent { Color = "0.2 0.2 0.2 1.0", Sprite = "Assets/Content/UI/UI.Background.Tile.psd" },
			new CuiRectTransformComponent { AnchorMin = "0.77 0.97", AnchorMax = "0.97 0.97", OffsetMin = $"0 {-i*scrollSpacing-scrollSize}", OffsetMax = $"0 {-i*scrollSpacing}"},
			new CuiOutlineComponent { Distance= "2 2", Color= "0 0 0 0.06" }
			}
		});

		elements.Add(new CuiElement
		{
			Name = "ButtonText_" + i,
			Parent = "Button_" + i,
			Components =
			{
			new CuiTextComponent { Text = $"Button#{i+1}", Color = "0.95 0.95 0.95 1.0", FontSize = 10, Align = TextAnchor.MiddleCenter },
			new CuiRectTransformComponent { AnchorMin = "0.02 0.02", AnchorMax = "0.98 0.98"},
			}
		});

		elements.Add(new CuiElement
		{
			Name = "TheButton_" + i,
			Parent = "ButtonText_" + i,
			Components =
			{
				new CuiButtonComponent { Color = "0.8 0.2 0.2 0.8", Command = "ui.testscrollui "+ (i+1), ImageType= Image.Type.Tiled },
				new CuiRectTransformComponent { AnchorMin = "0.02 0.02", AnchorMax = "0.98 0.98" },
				new CuiOutlineComponent { Distance= "2 2", Color= "0 0 0 0.50" },
			}
		});

	}
	return elements;
}
```

### `CuiDraggableComponent`
To create a draggable object

| Field | Type | Description |
| :---------- | :-------- | :-------------------------------------------------------- |  
| limitToParent | bool | Limit the draggable to the parent  |
| maxDistance | float | How far can you drag the object from its parent |  
| allowSwapping | bool | if true the draggable can be swapped with other draggables if dragged ontop of eachother |  
| dropAnywhere | bool | if false, the draggable will return to its last valid position (its initial position by default) unless swapped or attached to a slot |
| dragAlpha | float | if the alpha of the draggable's graphics should be lowered while being dragged. |  
| parentLimitIndex | int | if limitToParent is true, this index allows you to specify how many non slot parents it should traverse before finding the limit. If the slot has no filter, any draggable can be inserted. if the slot has a filter it only allows Draggables with a matching filter property. |  
| filter | bool | the filter string this draggable should carry. |  
| parentPadding | String | if limitToParent is true, specifies additional padding that the draggable should be contained. can be negative to allow the draggable to slightly travel outside the parent |
| anchorOffset | String | offset from the draggable's initial position  |  
| keepOnTop | bool | if true the draggable will stay detached from its parent, reccomended for unrestricted draggables |  
| positionRPC | PositionSendType | how the position should be processed before being sent via RPCs. see [PositionSendType](./basic-cui#positionsendtype)|  
| moveToAnchor | bool | if field present, move to anchor  |  
| rebuildAnchor | bool | if field present, rebuild anchor |  

#### PositionSendType

| Enum | Description |
| :---------- | :-------------------------------------------------------- |  
| NormalizedScreen | the Position normalized to the Screen resolution |  
| NormalizedParent | the Position normalized to the panel's limitParent, even if the setting is not used |  
| Relative | the offset from the Draggable's last position |
| RelativeAnchor | the offset from the anchor  |

Note: There are two hooks related to DraggableComponents.  [**Placeholder DragRPC**](../../hooks/player/OnPlayerAttack) and [**Placeholder DropRPC**](../../hooks/player/OnPlayerAttack)

```csharp
CuiDraggableComponent 
{ 
	limitToParent = false, 
	maxDistance = -1f,
	allowSwapping = false,
	dropAnywhere = true,
	dragAlpha = 1f,
	parentLimitIndex = 1,
	filter = "filter string",
	parentPadding = "0 0",
	anchorOffset = "0 0",
	keepOnTop = false,
	positionRPC = null,
	moveToAnchor,
	rebuildAnchor
}
```


### `CuiSlotComponent`
To Define a filter component for the draggable objects

Slots use a filter system that allows to specify what draggables can be attached. 
* A slot with no filter allow any draggable to be inserted. 
* A slot with a filter only allows Draggables with a matching filter property.

| Field | Type | Description |
| :---------- | :-------- | :-------------------------------------------------------- |  
| filter | String | the filter string associated to this component. |   

```csharp
CuiSlotComponent 
{ 
	filter = "filter string",
}
```

### `CuiHorizontalLayoutGroupComponent`

| Field | Type | Description |
| :---------- | :-------- | :-------------------------------------------------------- |  
| spacing            | float | Distance between elements |
| childAlignment     | string | see [Align](./basic-cui#align) |
| childForceExpandWidth | bool | if true, force width expansion |
| childForceExpandHeight | bool | if true, force height expansion |
| childControlWidth  | bool | if true, child will control width of elements |
| childControlHeight | bool | if true, child will control height of elements |
| childScaleWidth    | bool | if true, scale width |
| childScaleHeight   | bool | if true, scale height |

```csharp
CuiHorizontalLayoutGroupComponent 
{ 
	spacing = 0f,
	childAlignment = "UpperLeft",
	childForceExpandWidth = true,
	childForceExpandHeight = true,
	childControlWidth = false,
	childControlHeight = false,
	childScaleWidth = false,
	childScaleHeight = false,
}
```

### `CuiVerticalLayoutGroupComponent`

| Field | Type | Description |
| :---------- | :-------- | :-------------------------------------------------------- |  
| spacing            | float | Distance between elements |
| childAlignment     | string | [see Align](./basic-cui#align) |
| childForceExpandWidth | bool | if true, force width expansion |
| childForceExpandHeight | bool | if true, force height expansion |
| childControlWidth  | bool | if true, child will control width of elements |
| childControlHeight | bool | if true, child will control height of elements |
| childScaleWidth    | bool | if true, scale width |
| childScaleHeight   | bool | if true, scale height |

```csharp
CuiVerticalLayoutGroupComponent 
{ 
	spacing = 0f,
	childAlignment = "UpperLeft",
	childForceExpandWidth = true,
	childForceExpandHeight = true,
	childControlWidth = false,
	childControlHeight = false,
	childScaleWidth = false,
	childScaleHeight = false,
}
```

### `CuiGridLayoutGroupComponent`

| Field | Type | Description |
| :---------- | :-------- | :-------------------------------------------------------- |  
| cellsize      | string | Size of the cell, default "100 100" |
| spacing       | string | spacing between cells, default "0 0" |
| startCorner   | string | see [Align](./basic-cui#align), default UpperLeft |
| startAxis     | string | see [Axis](./basic-cui#axis), default Horizontal |
| childAlignment | string | see [Align](./basic-cui#align), default UpperLeft |
| constraint     | string | see [Constraint](./basic-cui#constraint), default Flexible |
| constraintCount | int32 | number of constraint |

#### `Axis`
* `Horizontal`
* `Vertical`
			
#### `Constraint`
* `Flexible`
* `FixedColumnCount`
* `FixedRowCount`

```csharp
CuiGridLayoutGroupComponent 
{ 
	cellsize = "100 100",
	spacing = "0 0",
	startCorner = "UpperLeft",
	startAxis = "Horizontal",
	childAlignment = "UpperLeft",
	constraint = "Flexible",
	constraintCount = 1,	
}
```

### `CuiContentSizeFitterComponent`

| Field | Type | Description |
| :---------- | :-------- | :-------------------------------------------------------- |  
| horizontalFit | string | Fit mode, see [FitMode](./basic-cui#fitmode), default Unconstrained |
| verticalFit   | string | Fit mode, see [FitMode](./basic-cui#fitmode), default Unconstrained |

#### `FitMode`
* `Unconstrained`
* `MinSize`
* `PreferredSize`

```csharp
CuiContentSizeFitterComponent 
{ 
	horizontalFit = "Unconstrained",
	verticalFit = "Unconstrained",
}
```

### `CuiLayoutElementComponent`

| Field | Type | Description |
| :---------- | :-------- | :-------------------------------------------------------- |  
| minWidth       | float | Minimum required width |
| minHeight      | float | Minimum required height |
| preferredWidth  | float | preferred Width, if space is available |
| preferredHeight | float | preferred Height, if space is available |
| flexibleWidth  | float | additional horizontal space, if available, default 0.0 |
| flexibleHeight | float | additional height space, if available, default 0.0 |
| ignoreLayout   | bool | number of constraint |

```csharp
CuiLayoutElementComponent 
{ 
	minWidth = -1f,
	minHeight = -1f,
	preferredWidth = 0f,
	preferredHeight = 0f,
	flexibleWidth = 0f,
	flexibleHeight = 0f,
	ignoreLayout = false,	
}
```

## Element presets

Oxide provides you with a few presets for elements with predefined components, such as:

### `CuiElement`
CuiElement is an assembly of single or multiple components. The CuiElement member will be defined through the `elements.Add` member. 

| Field | Type | Description |
| :---------- | :-------- | :-------------------------------------------------------- |  
| Parent | String | Parent name of this element  |
| Components | List\<ICuiComponent\> | a list of components to define the element  |  
| Name | String | Name of the element.  |  
| FadeOut | float | Fade out time in seconds   |
| Update | bool | Update flag |
| DestroyUI | String | Name of the UI to auto destroy  |  
| ActivateSelf | bool | Flag to activate/deactivate this CuiElement without a complete resend |

```csharp
CuiElement
{
	Name = "NameOfElement",
	Parent = "NameOfParent",
	Components =
		{
		new CuiRectTransformComponent {AnchorMin = "0 0", AnchorMax = "1 1", OffsetMax = "0 -50" },
		new CuiNeedsCursorComponent(),
		...
	}
}
```

### `CuiPanel` 
to show images or draw a nice background.  

| Field | Type | Description |
| :---------- | :-------- | :-------------------------------------------------------- |
| Image | CuiImageComponent | Background image, required |
| RawImage | CuiRawImageComponent | Raw image |
| RectTransform | CuiRectTransformComponent | Rectangle for the panel, required |
| CursorEnabled | bool | Cursor enabled for this UI |
| KeyboardEnabled | bool | Keyboard input enabled for this UI |
| FadeOut | float | Fade out time in seconds  |

```csharp
CuiPanel
{
	Image = { Color = "0.3 0.3 0.3 0.8" },
	RectTransform = { AnchorMin = "0.5 0.5", AnchorMax = "0.5 0.5", OffsetMin = "-200 -300", OffsetMax = "200 300" },
}
```
		
### `CuiButton` 
to create a button.  

| Field | Type | Description |
| :---------- | :-------- | :-------------------------------------------------------- |
| Button | CuiButtonComponent | Button to execute command, required |
| Text | CuiTextComponent | Text to display on the button, required  |
| RectTransform | CuiRectTransformComponent | Rectangle for the button, required |
| FadeOut | float | Fade out time in seconds  |

```csharp
CuiButton
{
	Button = {  },
	Text = { },
	RectTransform = { AnchorMin = "0.5 0.5", AnchorMax = "0.5 0.5", OffsetMin = "-100 -100", OffsetMax = "100 100" },
	FadeOut = 1f
}
```

### `CuiLabel` 
to show text.  

| Field | Type | Description |
| :---------- | :-------- | :-------------------------------------------------------- |
| Text | CuiTextComponent | Text to display, required |
| RectTransform | CuiRectTransformComponent | Rectangle to display text, required |
| FadeOut | float | Fade out time in seconds  |

### `CuiRectTransform` 
to define a rectangle

| Field | Type | Description |
| :---------- | :-------- | :-------------------------------------------------------- |  
| AnchorMin | String | Lower left corner see [UI position](./basic-cui#ui-position)  |  
| AnchorMax | String | Upper right corner      |  
| OffsetMin | String | Lower left corner, in pixels, relative to AnchorMin |  
| OffsetMax | String | Upper right corner, in pixels, relative to AnchorMin | 
| pivot | String | Pivot point or local origin, only applicable to scrollView. default to "0.5 0.5" |  

### `CuiScrollbar`
To draw a scrollbar

| Field | Type | Description |
| :---------- | :-------- | :-------------------------------------------------------- |  
| HandleColor | String | Color of handle see [colors](./basic-cui#colors) |  
| HandleSprite | String | Sprite of handle  |  
| HighlightColor | String | Color when highlighted  |
| PressedColor | String | Color when pressed  |  
| TrackColor | String | color of the track background |
| TrackSprite | String | Sprite of the track background  |
| Size | float | size of the scrollbar  |  
| Invert | bool | Invert action of scroller  |  
| AutoHide | bool | Auto hides the scroller  |  

They can be used to have predefined fields in case you want to modify them without casting ICuiComponent to the needed type, and to simplify UI creation.

## CuiHelper

### Adding UI
You made a few buttons and a nice background. To send them you have to create a container first, which is CuiElementContainer:
```csharp
var container = new CuiElementContainer();
var NameOfElement = container.Add(myBackground, "Overlay", "NameOfElement");
container.Add(myCuiComponent);
```
There are multiple Add methods - one is for presets, which lets you set the parent and name. If you do not specify a name, a random GUID will be used. Name will also be returned. 
However, if you have a CuiElement, it works as just a `List<CuiElement>` so you have to manually specify parent and name.

In order to send UI to the player, use the AddUi method:
```csharp
CuiHelper.AddUi(basePlayer, container);
```
or
```csharp
CuiHelper.AddUi(basePlayer, jsonString);
```
where jsonString is the Json formatted string of the UI, generated by the Json conversion of the CuiElementContainer.

### Destroying UI
If you want to remove your UI, you should call DestroyUi and specify element ID (name) to remove like that :

```csharp
CuiHelper.DestroyUi(basePlayer, NameOfElement);
```

### GetColor
Convert a string formatted ICuiColor "R G B A", to a type Color RGBA ```{color.r, color.g, color.b, color.a}``` 

### SetColor
Convert a type Color RGBA to a string formatted ICuiColor "R G B A"

### GetGuid
Generate a new unique Guid string.

## CuiElementContainer
CuiElementContainer is the top object to create an UI. It will contain multiple elements
Once the container is created, we add a CuiPanel and a CuiElement with multiple component in the CuiElement
Finally, the CuiHelper.AddUi will send the UI to a player for display.

But in the following example, we use the `TechTree` layer so the UI will only be visible when opening workbench.
You can have a look at [layer visibility](./basic-cui#layers-visibility) for proper layer to use.

```csharp
private const string UI_WORKBENCHOVERLAY = "UI_WorkbenchOverlay";
private void WorkbenchUi(BasePlayer player)
{
 CuiElementContainer elements = new CuiElementContainer();
 
 string panel = elements.Add(new CuiPanel
 {
  Image = { Color = "0 0 0 0.63", Sprite = "assets/content/materials/highlight.png", Material = "assets/content/ui/uibackgroundblur-ingamemenu.mat" },
  RectTransform = { AnchorMin = "0.1 0.7", AnchorMax = "0.9 0.8" }
 }, "TechTree", UI_WORKBENCHOVERLAY);

 elements.Add(new CuiLabel
 {
  Text = {
  Text = "Message to overlay in workbench",
  FontSize = 14, Align = TextAnchor.MiddleCenter, Color = "1 1 1 1" },
  RectTransform = { AnchorMin = "0.02 0.5", AnchorMax = "0.98 0.98" }
 }, panel);

 elements.Add(new CuiElement
 {
  Parent = panel,
  Components =
  {
   new CuiTextComponent { Text = "Workbench view", FontSize = 24, Align = TextAnchor.MiddleCenter, Color ="1 0 0 1" },
   new CuiOutlineComponent { Distance = "0.5 0.5", Color = "1 1 1 1" },
   new CuiRectTransformComponent { AnchorMin = "0.02 0.02",  AnchorMax = "0.98 0.5" },
  }
 });
 CuiHelper.AddUi(player, elements);
}
```

## Cache

If you are using a URL, client will download the image from the link you specify every time, and its quality might be changed depending on the quality settings. To avoid both issues, you can use "cache" a.k.a. Png option.

Game provides you with a Png option for UI, which is the image ID on the server. You have to store the image server-side first, for example you could use Image Library. After doing so you provide your client with the ID of this image, and client will download it from the server and store in its cache.
## UI position

There are two types of positions - Anchor and Offset. Both have Min and Max. Min value is the bottom left corner position, and Max is the top right one. Both Min and Max have X and Y values and are such string: "X Y".

Anchors are numbers that represent width and height in percents (%) from 0.0 (0%) to 1.0 (100%).

Offsets are accurate values that are width and height, in pixels, relative to a 1280x720 resolution. Example: You made a 100x100 box for 1280x720 and if you switch to 2560x1440, it will be 200x200 pixels.

Anchors are applied before offsets. If you want offsets to be relative to the screen center, make all anchors 0.5 0.5 so that both corners are in the center. Then to make a 100x100 box you should use offsets -50 -50 for bottom left corner and 50 50 for top right one.
## Colors

Rust UI is using normalized RGBA colors. It means that this nice red color (R255 G102 B102 A255) would be 1.0 0.4 0.4 1.0.

The fourth and last number is Alpha (transparency), in the example above it is 100% (no transparency).
## Fonts

All available fonts are:
* `DroidSansMono.ttf`
* `PermanentMarker.ttf`
* `RobotoCondensed-Bold.ttf`(Default)
* `RobotoCondensed-Regular.ttf`

## Align

* `TextAnchor.UpperLeft`
* `TextAnchor.UpperCenter`
* `TextAnchor.UpperRight`
* `TextAnchor.MiddleLeft`
* `TextAnchor.MiddleCenter`
* `TextAnchor.MiddleRight`
* `TextAnchor.LowerLeft`
* `TextAnchor.LowerCenter`
* `TextAnchor.LowerRight`
 
## Material

* `assets/content/ui/ui.saturation.shader`  
* `assets/content/ui/ui.thresholdcolor.shader`  
* `assets/content/ui/uibackgroundblur-ingamemenu.mat`  
* `assets/content/ui/uibackgroundblur-mainmenu.mat`  
* `assets/content/ui/uibackgroundblur-notice.mat`  
* `assets/content/ui/uibackgroundblur.mat`  
* `assets/content/ui/uibackgroundblur.shader`  
* `assets/content/image effects/darkclamp/darknessclamp.mat`
* `assets/content/image effects/linear fog/linearfog.mat`
* `assets/content/image effects/scope/defaultscope.mat`
* `assets/content/materials/cable.mat`
* `assets/content/materials/collider_mesh.mat`
* `assets/content/materials/collider_mesh_convex.mat`
* `assets/content/materials/collider_trigger.mat`
* `assets/content/materials/deployable/deployable_acceptable.mat`
* `assets/content/materials/deployable/deployable_denied.mat`
* `assets/content/materials/displacement/foliagedisplace_circle.mat`
* `assets/content/materials/displacement/foliagedisplace_square.mat`
* `assets/content/materials/gradient.mat`
* `assets/content/materials/ground.mat`
* `assets/content/materials/guide_bad.mat`
* `assets/content/materials/guide_good.mat`
* `assets/content/materials/guide_highlight.mat`
* `assets/content/materials/guide_neutral.mat`
* `assets/content/materials/itemmaterial.mat`
* `assets/content/materials/male.material.mat`
* `assets/content/shaders/gl/gl opaque.mat`
* `assets/content/shaders/gl/gl transparent.mat`
* `assets/content/ui/binocular_overlay.mat`
* `assets/content/ui/goggle_overlay.mat`
* `assets/content/ui/helmet_slit_overlay.mat`
* `assets/content/ui/ingame/compass/compassstrip.mat`
* `assets/content/ui/namefontmaterial.mat`
* `assets/content/ui/playerpreviewglow.mat`
* `assets/content/ui/playerpreviewremovesegments.mat`
* `assets/content/ui/playerpreviewsegments.mat`
* `assets/content/ui/scope_1.mat`
* `assets/content/ui/scope_2.mat`
* `assets/content/ui/ui.maskclear.mat`
* `assets/content/ui/uibackgroundblur-ingamemenu.mat`
* `assets/content/ui/uibackgroundblur-notice.mat`
* `assets/content/ui/uibackgroundblur.mat`
* `assets/icons/fogofwar.mat`
* `assets/icons/greyout.mat`
* `assets/icons/iconmaterial.mat`  (Default)


## Image type

* `Simple`
* `Sliced`
* `Tiled`
* `Filled`
   
## Layers

You can use these specific "layers" as parents for your UI, because they are always present:

* `Overall` the top most layer in front of all of Rust's UI
* `Overlay` top layer in front of most of Rust's UI
* `OverlayNonScaled`  Like Overlay, scale to resolution but not to client UI scale setting
* `Hud.Menu` the layer where rust positions menus like your inventory
* `Hud` the layer where Rust stores most HUD elements like your status bar
* `Under` the lowermost layer, your UI will appear behind all of Rust's UI
* `UnderNonScaled` like Under, scale to resolution but not to client UI scale setting

For the other layers, UI will only be visible in the respective view.
* `Inventory`
* `Crafting`
* `Contacts`
* `Clans`
* `TechTree`
* `Map`

## Layers visibility

| Layer | Normal | Inventory | Crafting | Contacts | Clans | TechTree | Map |
| :------ | :-----: | :-----: | :-----: | :-----: | :-----: | :-----: | :-----:|
| Overall             | X | X | X | X  | X | X | X |
| Overlay             | X | X | X | X  | X | X | X |
| Overlay  Non  Scaled| X | X | X | X  | X | X | X |
| Hud.Menu            | X | X | X | X  | X | X | X |
| Hud                 | X | 1 | 1 | 1  | 1 | 1 | X |
| Under               | X | 1 | 1 | 1  | 1 | 1 |   |
| Under  Non  Scaled  | X | 1 | 1 | 1  | 1 | 1 |   |
| Inventory           |   | X |   |    |   |   |   |
| Crafting            |   |   | X |    |   |   |   |
| Contacts            |   |   |   | X  |   |   |   |
| Clans               |   |   |   |    | X |   |   |
| TechTree            |   |   |   |    |   | X |   |
| Map                 |   |   |   |    |   |   | X |

1.  Visible but blurred, under the view background.
