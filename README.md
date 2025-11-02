# TB3 UI Library
**Made by txid - Mobile & Desktop Optimized Roblox UI Library**

A powerful, feature-rich UI library for Roblox with full mobile support, smooth animations, and extensive customization options.

## 🚀 Quick Start

### Load the Library

```lua
local Library = loadstring(game:HttpGet("https://raw.githubusercontent.com/WeebsMain/txid-ui-library/refs/heads/main/UI.lua"))()
```

### Basic Example

```lua
-- Create a window
local Window = Library:Window({
    Name = "My Script",
    SubTitle = "v1.0",
    ExpiresIn = "Never"
})

-- Create a page
local MainPage = Window:Page({
    Name = "Main",
    Icon = "136879043989014"
})

-- Create a sub-page
local CombatSubPage = MainPage:SubPage({
    Name = "Combat",
    Columns = 2
})

-- Create a section
local AimbotSection = CombatSubPage:Section({
    Name = "Aimbot",
    Icon = "136879043989014",
    Side = 1
})

-- Add elements
local Toggle = AimbotSection:Toggle({
    Name = "Enabled",
    Default = false,
    Callback = function(Value)
        print("Aimbot:", Value)
    end
})
```

---

## 📚 API Documentation

### Library

#### `Library:Window(Data)`
Creates a new window.

**Parameters:**
- `Name` (string): Window title
- `SubTitle` (string): Window subtitle
- `ExpiresIn` (string): Expiration text

**Returns:** Window object

**Example:**
```lua
local Window = Library:Window({
    Name = "My Hub",
    SubTitle = "for Blade Ball",
    ExpiresIn = "Never"
})
```

---

#### `Library:Notification(Name, Duration, Icon)`
Shows a notification.

**Parameters:**
- `Name` (string): Notification text
- `Duration` (number): Duration in seconds
- `Icon` (string, optional): Asset ID for icon

**Example:**
```lua
Library:Notification("Script loaded!", 5)
Library:Notification("Welcome!", 3, "94627324690861")
```

---

#### `Library:CreateSettingsPage(Window)`
Creates a settings page with configs and theming.

**Parameters:**
- `Window` (Window): The window to add settings to

**Example:**
```lua
Library:CreateSettingsPage(Window)
```

---

### Window

#### `Window:Page(Data)`
Creates a new page in the window.

**Parameters:**
- `Name` (string): Page name
- `Icon` (string): Asset ID for page icon

**Returns:** Page object

**Example:**
```lua
local CombatPage = Window:Page({
    Name = "Combat",
    Icon = "136879043989014"
})
```

---

#### `Window:Category(Name)`
Creates a category separator in the page list.

**Parameters:**
- `Name` (string): Category name

**Example:**
```lua
Window:Category("Combat")
```

---

### Page

#### `Page:SubPage(Data)`
Creates a sub-page within a page.

**Parameters:**
- `Name` (string): Sub-page name
- `Columns` (number): Number of columns (1 or 2)

**Returns:** SubPage object

**Example:**
```lua
local MainSubPage = MyPage:SubPage({
    Name = "Main",
    Columns = 2
})
```

---

### SubPage

#### `SubPage:Section(Data)`
Creates a section in the sub-page.

**Parameters:**
- `Name` (string): Section name
- `Icon` (string): Asset ID for section icon
- `Side` (number): Column to place section (1 or 2)

**Returns:** Section object

**Example:**
```lua
local AimbotSection = SubPage:Section({
    Name = "Aimbot",
    Icon = "136879043989014",
    Side = 1
})
```

---

## 🎨 UI Elements

### Toggle

Creates a toggle switch.

**Parameters:**
- `Name` (string): Toggle label
- `Flag` (string, optional): Unique identifier
- `Default` (boolean): Default state
- `Callback` (function): Called when toggled

**Methods:**
- `:Set(Value)` - Set toggle state
- `:Get()` - Get current state
- `:SetVisibility(Bool)` - Show/hide toggle
- `:Colorpicker(Data)` - Add colorpicker
- `:Keybind(Data)` - Add keybind

**Example:**
```lua
local Toggle = Section:Toggle({
    Name = "Enable ESP",
    Flag = "ESP_Enabled",
    Default = false,
    Callback = function(Value)
        print("ESP:", Value)
    end
})

-- Set the toggle
Toggle:Set(true)

-- Get the value
local isEnabled = Toggle:Get()

-- Add a colorpicker
Toggle:Colorpicker({
    Flag = "ESP_Color",
    Default = Color3.fromRGB(255, 0, 0),
    Callback = function(Color)
        print("Color:", Color)
    end
})

-- Add a keybind
Toggle:Keybind({
    Flag = "ESP_Keybind",
    Default = Enum.KeyCode.E,
    Mode = "Toggle",
    Callback = function(Toggled)
        print("Keybind toggled:", Toggled)
    end
})
```

---

### Button

Creates a clickable button.

**Parameters:**
- `Name` (string): Button text
- `Callback` (function): Called when clicked

**Methods:**
- `:Press()` - Programmatically press button
- `:SetVisibility(Bool)` - Show/hide button

**Example:**
```lua
local Button = Section:Button({
    Name = "Kill All",
    Callback = function()
        print("Killing all players...")
    end
})

-- Press the button
Button:Press()
```

---

### Slider

Creates a slider for numeric values.

**Parameters:**
- `Name` (string): Slider label
- `Flag` (string, optional): Unique identifier
- `Min` (number): Minimum value
- `Max` (number): Maximum value
- `Default` (number): Default value
- `Decimals` (number): Decimal precision
- `Suffix` (string): Text after value
- `Callback` (function): Called when changed

**Methods:**
- `:Set(Value)` - Set slider value
- `:Get()` - Get current value
- `:SetVisibility(Bool)` - Show/hide slider

**Example:**
```lua
local Slider = Section:Slider({
    Name = "FOV",
    Flag = "Aimbot_FOV",
    Min = 0,
    Max = 360,
    Default = 90,
    Decimals = 1,
    Suffix = "°",
    Callback = function(Value)
        print("FOV:", Value)
    end
})

-- Set the value
Slider:Set(120)

-- Get the value
local fov = Slider:Get()
```

---

### Dropdown

Creates a dropdown menu.

**Parameters:**
- `Name` (string): Dropdown label
- `Flag` (string, optional): Unique identifier
- `Items` (table): List of options
- `Default` (string/table): Default selection
- `Multi` (boolean): Allow multiple selections
- `Callback` (function): Called when selection changes

**Methods:**
- `:Set(Value)` - Set selected option(s)
- `:Get()` - Get current selection
- `:Add(Option)` - Add new option
- `:Remove(Option)` - Remove option
- `:Refresh(List)` - Replace all options
- `:SetVisibility(Bool)` - Show/hide dropdown

**Example:**
```lua
-- Single selection
local Dropdown = Section:Dropdown({
    Name = "Target Part",
    Flag = "Target_Part",
    Items = {"Head", "Torso", "HumanoidRootPart"},
    Default = "Head",
    Multi = false,
    Callback = function(Value)
        print("Selected:", Value)
    end
})

-- Multi selection
local MultiDropdown = Section:Dropdown({
    Name = "ESP Elements",
    Flag = "ESP_Elements",
    Items = {"Name", "Health", "Distance", "Box"},
    Default = {"Name", "Health"},
    Multi = true,
    Callback = function(Value)
        print("Selected:", table.concat(Value, ", "))
    end
})

-- Add option
Dropdown:Add("LeftArm")

-- Remove option
Dropdown:Remove("HumanoidRootPart")

-- Refresh with new list
Dropdown:Refresh({"Head", "Chest", "Legs"})
```

---

### Textbox

Creates a text input field.

**Parameters:**
- `Name` (string): Textbox label
- `Flag` (string, optional): Unique identifier
- `Default` (string): Default text
- `Placeholder` (string): Placeholder text
- `Numeric` (boolean): Only allow numbers
- `Finished` (boolean): Only callback on Enter press
- `Callback` (function): Called when text changes

**Methods:**
- `:Set(Value)` - Set text
- `:Get()` - Get current text
- `:SetVisibility(Bool)` - Show/hide textbox

**Example:**
```lua
local Textbox = Section:Textbox({
    Flag = "Player_Name",
    Placeholder = "Enter player name...",
    Default = "",
    Numeric = false,
    Finished = true,
    Callback = function(Value)
        print("Player:", Value)
    end
})

-- Numeric only textbox
local NumberBox = Section:Textbox({
    Flag = "Walk_Speed",
    Placeholder = "Speed...",
    Default = "16",
    Numeric = true,
    Finished = false,
    Callback = function(Value)
        local speed = tonumber(Value)
        if speed then
            print("Speed:", speed)
        end
    end
})
```

---

### Label

Creates a text label.

**Parameters:**
- `Name` (string): Label text

**Methods:**
- `:SetText(Text)` - Update label text
- `:SetVisibility(Bool)` - Show/hide label
- `:Colorpicker(Data)` - Add colorpicker
- `:Keybind(Data)` - Add keybind

**Example:**
```lua
local Label = Section:Label("Status: Ready")

-- Update text
Label:SetText("Status: Running")

-- Add colorpicker
Label:Colorpicker({
    Flag = "Label_Color",
    Default = Color3.fromRGB(255, 255, 255),
    Callback = function(Color)
        print("Color:", Color)
    end
})
```

---

### Colorpicker

Creates a color picker (usually attached to toggle/label).

**Parameters:**
- `Flag` (string, optional): Unique identifier
- `Default` (Color3): Default color
- `Callback` (function): Called when color changes

**Methods:**
- `:Set(Color, Alpha)` - Set color
- `:Get()` - Get current color
- `:SetVisibility(Bool)` - Show/hide colorpicker

**Example:**
```lua
local Colorpicker = Label:Colorpicker({
    Flag = "ESP_Color",
    Default = Color3.fromRGB(255, 0, 0),
    Callback = function(Color, Alpha)
        print("Color:", Color)
        print("Alpha:", Alpha)
    end
})

-- Set color
Colorpicker:Set(Color3.fromRGB(0, 255, 0))

-- Set with hex
Colorpicker:Set("#FF00FF")

-- Get color
local color = Colorpicker:Get()
```

---

### Keybind

Creates a keybind selector (usually attached to toggle/label).

**Parameters:**
- `Flag` (string, optional): Unique identifier
- `Default` (KeyCode): Default key
- `Mode` (string): "Toggle", "Hold", or "Always"
- `Callback` (function): Called when activated

**Methods:**
- `:Set(Key)` - Set keybind
- `:Get()` - Get current key and mode
- `:Press(Bool)` - Programmatically trigger keybind

**Example:**
```lua
local Keybind = Toggle:Keybind({
    Flag = "Aimbot_Key",
    Default = Enum.KeyCode.E,
    Mode = "Toggle",
    Callback = function(Toggled)
        print("Aimbot toggled via keybind:", Toggled)
    end
})

-- Change keybind
Keybind:Set({
    Key = Enum.KeyCode.Q,
    Mode = "Hold"
})

-- Get keybind info
local key, mode, toggled = Keybind:Get()
print("Key:", key, "Mode:", mode, "Active:", toggled)
```

---

## 💾 Flags & Config System

### Using Flags

Flags allow you to access element values globally:

```lua
local Toggle = Section:Toggle({
    Name = "ESP",
    Flag = "ESP_Enabled",
    Default = false
})

-- Access the value anywhere in your script
print(Library.Flags["ESP_Enabled"]) -- true/false

-- Set the value
Library.SetFlags["ESP_Enabled"](true)
```

---

### Save & Load Configs

```lua
-- Save current config
local configData = Library:GetConfig()
writefile("myconfig.json", configData)

-- Load config
local configData = readfile("myconfig.json")
Library:LoadConfig(configData)

-- Delete config
Library:DeleteConfig("myconfig.json")
```

---

## 🎨 Theming

Change UI colors:

```lua
-- Change individual theme colors
Library:ChangeTheme("Accent", Color3.fromRGB(255, 100, 100))
Library:ChangeTheme("Background", Color3.fromRGB(20, 20, 20))

-- Available theme options:
-- "Background" - Main background color
-- "Inline" - Secondary background
-- "Element" - Button/element background
-- "Accent" - Highlight color
-- "Border" - Primary border color
-- "Border 2" - Secondary border color
```

---

## 📱 Mobile Support

The library automatically detects mobile devices and:
- Reduces UI size to 600x450 (from 798x599)
- Adds a mobile toggle button (☰/✕) in top-left
- Optimizes font sizes and element spacing
- Supports touch input for all elements

**Mobile Toggle Button:**
- Tap to open/close the UI
- Automatically appears only on mobile devices
- Persistent - stays visible when UI is closed

---

## 🔧 Advanced Usage

### Complete Script Example

```lua
-- Load library
local Library = loadstring(game:HttpGet("YOUR_URL_HERE"))()

-- Create window
local Window = Library:Window({
    Name = "Ultimate Hub",
    SubTitle = "v2.0 Beta",
    ExpiresIn = "30d"
})

-- Create pages
local CombatPage = Window:Page({Name = "Combat", Icon = "136879043989014"})
local VisualsPage = Window:Page({Name = "Visuals", Icon = "136879043989014"})
local MiscPage = Window:Page({Name = "Misc", Icon = "136879043989014"})

-- Create sub-pages
local AimbotSubPage = CombatPage:SubPage({Name = "Aimbot", Columns = 2})
local ESPSubPage = VisualsPage:SubPage({Name = "ESP", Columns = 2})

-- Create sections
local MainAimbot = AimbotSubPage:Section({
    Name = "Main",
    Icon = "136879043989014",
    Side = 1
})

local Settings = AimbotSubPage:Section({
    Name = "Settings",
    Icon = "72732892493295",
    Side = 2
})

-- Add elements
local AimbotToggle = MainAimbot:Toggle({
    Name = "Enable Aimbot",
    Flag = "Aimbot_Enabled",
    Default = false,
    Callback = function(Value)
        -- Your aimbot code here
        print("Aimbot:", Value)
    end
})

AimbotToggle:Colorpicker({
    Flag = "Aimbot_FOV_Color",
    Default = Color3.fromRGB(255, 255, 255),
    Callback = function(Color)
        print("FOV Color:", Color)
    end
})

AimbotToggle:Keybind({
    Flag = "Aimbot_Keybind",
    Default = Enum.KeyCode.E,
    Mode = "Toggle"
})

Settings:Slider({
    Name = "FOV",
    Flag = "Aimbot_FOV",
    Min = 0,
    Max = 360,
    Default = 90,
    Decimals = 1,
    Suffix = "°",
    Callback = function(Value)
        print("FOV:", Value)
    end
})

Settings:Dropdown({
    Name = "Target Part",
    Flag = "Aimbot_Part",
    Items = {"Head", "Torso", "HumanoidRootPart"},
    Default = "Head",
    Multi = false,
    Callback = function(Value)
        print("Target:", Value)
    end
})

-- Add settings page
Library:CreateSettingsPage(Window)

-- Show notifications
Library:Notification("Script loaded successfully!", 5, "94627324690861")
```

---

## 🎯 Tips & Best Practices

1. **Use Flags:** Always use unique flags for elements you need to access later
2. **Organize Pages:** Use categories and sub-pages to keep UI organized
3. **Mobile Testing:** Test your script on mobile to ensure proper functionality
4. **Callbacks:** Keep callback functions efficient to avoid lag
5. **Error Handling:** The library uses `SafeCall` internally for error handling

---

## 🆘 Troubleshooting

**Toggle buttons not working on mobile?**
- This is now fixed! Make sure you're using the latest version.

**Dropdown closes immediately on mobile?**
- Fixed in latest version - uses `InputBegan` with touch support.

**UI too large on mobile?**
- The library auto-detects mobile and adjusts size automatically.

**Elements overlapping?**
- Try using 2 columns in your sub-pages for better organization.

---

## 📝 Credits

**Made by KM**

This is a mobile-optimized UI library for Roblox with full touch support and responsive design.

---

## 📜 License

Free to use for personal and commercial projects. Please credit KM if you use this library.

---

## 🔗 Links

- **GitHub:** https://github.com/WeebsMain/txid-ui-library/
- **Discord:** https://discord.gg/8MunY7FtfY
- **Support:** https://discord.gg/8MunY7FtfY

---

**Last Updated:** November 1, 2025
**Version:** 1.0.0
