# GoF_Abstract-Factory-Pattern


Provides an interface for creating families of related or dependent objects without specifying their concrete classes.

The Abstract Factory Pattern is a creational design pattern that provides an interface for creating families of related objects without specifying their concrete classes directly. It allows you to create objects that follow a specific theme or variation. Let's create a simple C# sample for the Abstract Factory Pattern:

In this example, we'll create a simple UI component factory that can generate buttons and checkboxes for both Windows and macOS operating systems.

```csharp
using System;

// Client Code
class Program
{
    static void Main(string[] args)
    {
        // Depending on the operating system, create the appropriate factory
        IUIComponentFactory uiFactory;

        if (IsWindows())
        {
            uiFactory = new WindowsUIComponentFactory();
        }
        else
        {
            uiFactory = new MacOSUIComponentFactory();
        }

        // Create UI components using the factory
        IButton button = uiFactory.CreateButton();
        ICheckbox checkbox = uiFactory.CreateCheckbox();

        // Render the UI components
        button.Render();
        checkbox.Render();
    }

    // A simple method to determine the operating system (for demonstration purposes)
    static bool IsWindows()
    {
        return Environment.OSVersion.Platform == PlatformID.Win32NT;
    }
}

// Abstract Product: Button
interface IButton
{
    void Render();
}

// Concrete Product: Windows Button
class WindowsButton : IButton
{
    public void Render()
    {
        Console.WriteLine("Rendering a Windows button.");
    }
}

// Concrete Product: macOS Button
class MacOSButton : IButton
{
    public void Render()
    {
        Console.WriteLine("Rendering a macOS button.");
    }
}

// Abstract Product: Checkbox
interface ICheckbox
{
    void Render();
}

// Concrete Product: Windows Checkbox
class WindowsCheckbox : ICheckbox
{
    public void Render()
    {
        Console.WriteLine("Rendering a Windows checkbox.");
    }
}

// Concrete Product: macOS Checkbox
class MacOSCheckbox : ICheckbox
{
    public void Render()
    {
        Console.WriteLine("Rendering a macOS checkbox.");
    }
}

// Abstract Factory
interface IUIComponentFactory
{
    IButton CreateButton();
    ICheckbox CreateCheckbox();
}

// Concrete Factory for Windows
class WindowsUIComponentFactory : IUIComponentFactory
{
    public IButton CreateButton()
    {
        return new WindowsButton();
    }

    public ICheckbox CreateCheckbox()
    {
        return new WindowsCheckbox();
    }
}

// Concrete Factory for macOS
class MacOSUIComponentFactory : IUIComponentFactory
{
    public IButton CreateButton()
    {
        return new MacOSButton();
    }

    public ICheckbox CreateCheckbox()
    {
        return new MacOSCheckbox();
    }
}
```














