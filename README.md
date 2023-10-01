# GoF_Abstract-Factory-Pattern (Creational Patterns)

https://refactoring.guru/design-patterns/abstract-factory

https://www.dotnettricks.com/learn/designpatterns/abstract-factory-design-pattern-dotnet

https://refactoring.guru/design-patterns/examples

Abstract Factory is a creational design pattern that lets you produce families of related objects without specifying their concrete classes.

![image](https://github.com/luiscoco/GoF_Csharp-3.Abstract-Factory-Pattern/assets/32194879/ff7111bc-2e29-4318-af3d-c2a831cb5040)

## Problem
Imagine that you’re creating a furniture shop simulator. Your code consists of classes that represent:

A family of related products, say: Chair + Sofa + CoffeeTable.

Several variants of this family. For example, products Chair + Sofa + CoffeeTable are available in these variants: Modern, Victorian, ArtDeco.

![image](https://github.com/luiscoco/GoF_Csharp-3.Abstract-Factory-Pattern/assets/32194879/432994bc-0dba-46ef-876a-63500b2256b0)

Also, you don’t want to change existing code when adding new products or families of products to the program. Furniture vendors update their catalogs very often, and you wouldn’t want to change the core code each time it happens.

## Solution
The first thing the Abstract Factory pattern suggests is to explicitly declare interfaces for each distinct product of the product family (e.g., chair, sofa or coffee table). Then you can make all variants of products follow those interfaces. For example, all chair variants can implement the Chair interface; all coffee table variants can implement the CoffeeTable interface, and so on.

![image](https://github.com/luiscoco/GoF_Csharp-3.Abstract-Factory-Pattern/assets/32194879/af2f8425-4888-45c9-aa9b-186c314f25f6)

All variants of the same object must be moved to a single class hierarchy.

The next move is to declare the Abstract Factory—an interface with a list of creation methods for all products that are part of the product family (for example, createChair, createSofa and createCoffeeTable). These methods must return abstract product types represented by the interfaces we extracted previously: Chair, Sofa, CoffeeTable and so on.

![image](https://github.com/luiscoco/GoF_Csharp-3.Abstract-Factory-Pattern/assets/32194879/e50f23cf-5152-4000-9c6c-78c26a731b34)

Each concrete factory corresponds to a specific product variant.

Now, how about the product variants? For each variant of a product family, we create a separate factory class based on the AbstractFactory interface. A factory is a class that returns products of a particular kind. For example, the ModernFurnitureFactory can only create ModernChair, ModernSofa and ModernCoffeeTable objects.

The client code has to work with both factories and products via their respective abstract interfaces. This lets you change the type of a factory that you pass to the client code, as well as the product variant that the client code receives, without breaking the actual client code.

![image](https://github.com/luiscoco/GoF_Csharp-3.Abstract-Factory-Pattern/assets/32194879/a8ff8c12-14ba-4b4f-8634-8bcb5d088167)

## Abstract Factory Pattern

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

## How to setup Github actions

![Csharp Github actions](https://github.com/luiscoco/GoF_Csharp-3.Abstract-Factory-Pattern/assets/32194879/0acf4913-fad4-4fcf-a4ed-91c3d201d173)












