﻿[logo]: https://raw.githubusercontent.com/Geeksltd/Zebble.ItemPicker/master/icon.png "Zebble.ItemPicker"


## Zebble.ItemPicker

![logo]

A Zebble plugin that allows the user to select one or more items from a pre-defined list.


[![NuGet](https://img.shields.io/nuget/v/Zebble.ItemPicker.svg?label=NuGet)](https://www.nuget.org/packages/Zebble.ItemPicker/)

> It's similar to the drop down list, or collapsible Checkboxes control in the web world. You can set MultiSelect (bool) property to true to allow multiple items' selection.
If there are more than 8 items in the list it will automatically show a search box to the user to make it easier to find items from long lists.

<br>


### Setup
* Available on NuGet: [https://www.nuget.org/packages/Zebble.ItemPicker/](https://www.nuget.org/packages/Zebble.ItemPicker/)
* Install in your platform client projects.
* Available for iOS, Android and UWP.
<br>


### Api Usage

#### Basic usage

```xml
<ItemPicker Id="MyItemPicker" MultiSelect="true" Searchable="true"></ItemPicker>
```
```csharp
new ItemPicker { Id = "MyItemPicker", MultiSelect = true, Searchable = true };
```
#### After Click

When you clicked on the ItemPicker object, you can search and select one item:

#### After Select
When you selected an item, you can see that only.

#### Data source
If you want to assign a list to an item picker to show them, you should use DataSource. Any IEnumerable object could be used for this.
```csharp
MyItemPicker.DataSource = new List<Customer>();
```
#### Customising items
Internally, ItemPicker will show an OptionsList control in a pop-up. So you have the same control over its settings as you have with an OptionsList control. To gain access to the options list you can use the DialogOpenning event which is raised after the dialog is created and before it's shown in a pop-up:
```csharp
myPicker.DialogOpenning.Handle(CustomizeDialog);

Task CustomizeDialog(ItemPicker.Dialog dialog)
{
    var optionsList = dialog.List;
    /* TODO: Customise it.... /* 
}
```
##### MarkUp:
```xml
<ItemPicker Id="MyItemPicker" DataSource="Items"
MultiSelect="true" Searchable="true"></ItemPicker>
```
##### C#:
```csharp
partial class ItemPickerPage
{
    public List<Contact> Items;
    public override async Task OnInitializing()
    {
        Items = GetSource().ToList();
        await base.OnInitializing();
        await InitializeComponents();            
    }
    IEnumerable<Contact> GetSource() => Database.GetList<Contact>();
}
```

#### MultiSelect
If MultiSelect property is set to true, the user can choose one or more items from list. The default value is false that means user can select one item.

#### Searchable
Searchable property determines user can search or not.  It's recommended to always set it to true.
```xml
<ItemPicker Searchable ="true"   />
```
#### SelectedValue
By setting the SelectedValue, ItemPicker will find and pre-select an item matching that value. Each item in ItemPicker list is a pair of Value and Text. It's better to distinguish your items using their value, because there might be items with a same text but with different values.
```xml
<ItemPicker SelectedValue="34"   />
```
#### SelectedText
By setting SelectedText, ItemPicker will show the value in its Label. For empty or null values, ItemPicker will shows its Placeholder.
```xml
<ItemPicker   SelectedText="John"  />
```


### Properties
| Property     | Type         | Android | iOS | Windows |
| :----------- | :----------- | :------ | :-- | :------ |
| ButtonsAtTop            | bool           | x       | x   | x       |
| Searchable            | bool?           | x       | x   | x       |
| SearchCharacterCount            | int           | x       | x   | x       |
| SelectedValue            | object           | x       | x   | x       |
| SelectedItem            | IEnumerable<OptionsDataSource.DataItem&gt;           | x       | x   | x       |
| DataSource            | IEnumerable<object&gt;           | x       | x   | x       |
| MultiSelect            | bool           | x       | x   | x       |

### Events
| Event             | Type                                          | Android | iOS | Windows |
| :-----------      | :-----------                                  | :------ | :-- | :------ |
| SelectionChanged               | AsyncEvent    | x       | x   | x       |
| DialogOpenning              | AsyncEvent<Dialog&gt;    | x       | x   | x       |
