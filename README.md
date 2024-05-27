# ModBootstrap
 Basic mod loader for Friday Night Funkin'

In order to make your mod compatible you will need to add this somewhere in your _polymod_meta.json
``` json
"dependencies": {
    "modbootstrap": "*"
},
```
And then add a Module .hxc script with a unique sounding name of your choice.

``` hx
import funkin.modding.module.Module;
import funkin.modding.module.ModuleHandler;

class ExampleModBind extends Module {
  var loadedGame:Bool = false;

  public function new() {
      super("ExampleModBind");
  }
  public function onCreate(event:ScriptEvent):Void {
    this.active = false;

    ModuleHandler.getModule("BootStrapBinds").scriptCall("bind", [{
        name: "My Mod", // mod name
        description: "I ate your wife", // mod description
        target: "BaseTitleState", // target state
        bg: '', // if the bg is set to nothing, it will use the default bg
        icon: 'fnficon32', // path to icon (32x32)
        author: "the elusive my mod team", // name of the people who made the mod
        logo: '', // big logo for the mod.
        color: 0xFFB00B69, // color for the selection tab thingies
        bg_group: (group) -> { // for dynamic bgs, to add stuff you must do "group.add(myVar)"
          return; // do nothing.
        },
        disclaimer: "This mod contains flashing lights." // disclaimer, add anything you want here.
    }]);
  }
}
```
