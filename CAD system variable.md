
## CAD system variable

**TILEMODE** and **CVPORT** work together to determine exactly where you are standing<br/> inside an AutoCAD drawing.<br/>
While TILEMODE toggles the global environment between Model Space and Paper Space<br/> (Layouts), CVPORT pinpoints the exact viewport number you are currently actively working inside.
<br/>
| TILEMODE<br/> Value  | Environment | CVPORT<br/> Value | What it means |
| ------------- |:-------------:|:-------------:|:-------------:|
|   1 (On)      | Model Tab     | 2 or higher     | You are in the main Model space. (Value 1 is <br/> reserved/not used here; viewports are tiled).     |
|  0 (Off)      | Layout Tab     | 1	     | You are in Paper Space. You are drawing directly on <br/> the sheet (title blocks, annotations).     |
|  0 (Off)      | Layout Tab     | 2 or higher    | You are in Model Space through a Layout <br/>Viewport. (You double-clicked inside a floating <br/>layout window).     |

* db.TileMode = true; is the exact programmatic equivalent of typing TILEMODE = 1 <br/>into the AutoCAD command line (forces the environment into Model Space).
* db.TileMode = false; is the exact programmatic equivalent of typing TILEMODE = 0 <br/>into the AutoCAD command line (switches the environment to the last active Layout tab)
