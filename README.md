# ModBootstrap
 Basic mod loader for Friday Night Funkin'
![image](https://github.com/Burgerballs/ModBootstrap/assets/107233412/2323253b-c726-4504-be14-1ca1bcfad314)

> [!TIP]
> If you wish to make your mod compatible with both Cyn's ModLauncher and ModBootstrap, check [here](https://github.com/cyn0x8/ModLauncher?tab=readme-ov-file#compatibility).

In order to make your mod compatible with ModBootstrap, add a .hxc script with a unique sounding name of your choice.

``` hx
import funkin.modding.module.Module;
import funkin.modding.module.ModuleHandler;

class ExampleModBind extends Module { // Replace the class name with a unique name of your choice
  public function new() {
      super("ExampleModBind"); // Replace the string with a unique name of your choice
  }
  public function onCreate(event:ScriptEvent):Void {
    this.active = false;
    if ((launcher = ModuleHandler.getModule("BootStrapBinds")) != null) {
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
    } else {
     // place failsafe code here.
    }
  }
}
```

If you need to check if the current mod being played is your's, use ``Save.instance.modOptions.get("ModBootstrapV2").selected_mod``.

Make sure to also add some stuff to your title screen to allow the player to go back to the bootstrap menu by pressing TAB, like so:
```hx
if (FlxG.keys.justPressed.TAB && (launcher = ModuleHandler.getModule("BootStrapBinds")) != null) {
 FlxG.switchState(ScriptedMusicBeatState.init("BootStrapState"));
}
```
