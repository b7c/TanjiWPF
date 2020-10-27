# TanjiWPF
A framework for building Tanji modules using WPF.

## Implementation

1. Create a .NET framework WPF application
2. Copy the TanjiWPF source files into the project
3. Set the output type to class library in the project properties
4. Delete `App.xaml` from the project
5. In the reference manager:
* under Assemblies, add references to `System.Windows.Forms` and `WindowsFormsIntegration`
* under Browse, add references to the `Sulakore`, `Tangine` and `Flazzy` DLLs that come with Tanji
6. In MainWindow.xaml, add the `xmlns:tanjiwpf="clr-namespace:TanjiWPF"` attribute to the root `Window` element
7. Then change the `Window` element to `tanjiwpf:ExtensionWindow`
```xaml
<tanjiwpf:ExtensionWindow x:Class="TanjiWpfExample.MainWindow"
        xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
        xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
        xmlns:d="http://schemas.microsoft.com/expression/blend/2008"
        xmlns:mc="http://schemas.openxmlformats.org/markup-compatibility/2006"
        xmlns:local="clr-namespace:TanjiWpfExample"
        xmlns:tanjiwpf="clr-namespace:TanjiWPF"
        mc:Ignorable="d"
        Title="TanjiWpf Example Module">
    <Grid>
    </Grid>
</tanjiwpf:ExtensionWindow>
```
8. In `MainWindow.xaml.cs`, inherit the `MainWindow` class from `TanjiWPF.ExtensionWindow`
```cs
using TanjiWPF;

namespace TanjiWpfExample
{
    public partial class MainWindow : ExtensionWindow
    {
        public MainWindow()
        {
            InitializeComponent();
        }
    }
}
```
9. Create a new class which will be the module entry point:
```cs
using TanjiWPF;
using Sulakore.Modules;

[Module("name", "description")]
[Author("author name")]
public class ModuleMain : WpfModuleLoader<MainWindow> { }
```
Tanji will then load this module and the `WpfModuleLoader` will create and display the WPF application window
