
### Hooking into AutoCAD copy & paste via Ctrl-C and -V
https://keanw.com/2012/12/hooking-into-autocad-copy-paste-via-ctrl-c-and-v-using-net.html

Step 1: Replace Your C# Code
```
using Autodesk.AutoCAD.ApplicationServices.Core;
using Autodesk.AutoCAD.Runtime;
using System;

namespace AutoCADShortcutManager
{
    public class ShortcutModifierFinal : IExtensionApplication
    {
        // Persistent memory flag to track active shortcut state
        private static bool _useCustomTools = false;

        public void Initialize() { }

        public void Terminate() { }

        [CommandMethod("ppo")]
        public void RunPPO()
        {
            _useCustomTools = false;
            var doc = Application.DocumentManager.MdiActiveDocument;
            if (doc != null)
            {
                doc.Editor.WriteMessage("\n[PPO] Shortcuts swapped to native AutoCAD paste defaults.");
                
            }
        }

        [CommandMethod("ppn")]
        public void RunPPN()
        {
            _useCustomTools = true;
            var doc = Application.DocumentManager.MdiActiveDocument;
            if (doc != null)
            {
                doc.Editor.WriteMessage("\n[PPN] Shortcuts successfully swapped to custom tools.");
                
            }
        }

        [CommandMethod("MY_COPY_ROUTE")]
        public void MyCopyRoute()
        {
            var doc = Application.DocumentManager.MdiActiveDocument;
            if (doc == null) return;

            if (_useCustomTools)
            {
                doc.SendStringToExecute("._ccint ", true, false, false);
            }
            else
            {
                doc.SendStringToExecute("._copyclip ", true, false, false);
            }
        }

        [CommandMethod("MY_PASTE_ROUTE")]
        public void MyPasteRoute()
        {
            var doc = Application.DocumentManager.MdiActiveDocument;
            if (doc == null) return;

            if (_useCustomTools)
            {
                doc.SendStringToExecute("._pcint ", true, false, false);
            }
            else
            {
                doc.SendStringToExecute("._pasteclip ", true, false, false);
            }
        }
    }
}
```



Step 2: One-Time Manual Setup & Cleaning
```
To purge the existing duplicates and link the new, stable code:
1. Open AutoCAD, type CUI and press Enter.
2. In the Command List panel (bottom left), search for your ghost items (DynamicPaste, DynamicCopy, etc.). Right-click each duplicate entry and select Delete.
3. Click the Create a New Command button (star icon) to create two clean commands:
	• Name: Dynamic Route Paste | Macro: ^C^C_MY_PASTE_ROUTE;
	• Name: Dynamic Route Copy | Macro: ^C^C_MY_COPY_ROUTE;
4. In the upper-left tree view, expand Keyboard Shortcuts > Shortcut Keys.
5. Drag your newly created commands from the bottom list and drop them into the Shortcut Keys folder.
6. Select your new commands inside the folder, look at the Properties panel on the right, click Key(s), and assign CTRL+V and CTRL+C respectively.
7. Click Apply and OK.
```
