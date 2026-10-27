## Step 1: Create the Folder Structure

```
C:\ProgramData\Autodesk\ApplicationPlugins\MyAutoCadPlugin.bundle\
├── PackageContents.xml
└── Contents\
    ├── YourMainPlugin.dll
    └── Blocks.dll
 ```   
## Step 2: Create the PackageContents.xml File

```
<?xml version="1.0" encoding="utf-8"?>
<ApplicationPackage SchemaVersion="1.0" AppVersion="1.0.0" Name="My AutoCAD Plugin" Description="Loads main plugin and Blocks dependency" ProductCode="{a1b2c3d4-e5f6-7a8b-9c0d-1e2f3a4b5c6d}">
  <Components>
    <!-- Target 64-bit Windows and all versions of AutoCAD -->
    <RuntimeRequirements OS="Win64" Platform="AutoCAD*" />
    
    <!-- Component Entry pointing to your startup class library -->
    <ComponentEntry AppName="MyAutoCadPlugin" 
                    ModuleName="Contents\YourMainPlugin.dll" 
                    AppDescription="Main entry point for the plugin" 
                    LoadOnAutoCADStartup="True">
    </ComponentEntry>
  </Components>
</ApplicationPackage>
```

<p>• ProductCode: Replace the dummy GUID inside the brackets {...} with a fresh, unique GUID. <br />You can generate one in Visual Studio by going to Tools > Create GUID (use the Registry format).<p>
<p>• ModuleName: Ensure this points accurately to your main startup DLL relative to the root <br />bundle folder. (Keep ./Contents/ at the beginning).<p>
<p>• LoadOnAutoCADStartup="True": This tells AutoCAD to automatically execute and load your <br />plugin as soon as the software opens.<p>

## Step 3: Copy Your Built DLLs

Build your solution in Visual Studio. Take your freshly compiled main plugin DLL and your<br /> Blocks.dll out of your Visual Studio bin/Debug or bin/Release folder, and paste them both directly into the Contents subfolder you created in Step 1.

## Step 4: Deploy and Test

To make AutoCAD instantly recognize your bundle package, move your entire MyAutoCadPlugin.bundle folder into one of AutoCAD's official auto-load paths:
• For All Users on the Machine (Recommended):
C:\ProgramData\Autodesk\ApplicationPlugins\
(Note: ProgramData is a hidden system folder by default).
• For Current User Only (No Admin Rights Required):
%AppData%\Autodesk\ApplicationPlugins\

## Step 5: Launch AutoCAD

Open AutoCAD. You will see a security prompt asking if you want to trust the application (since it is an unsigned custom binary). Click Always Load.

