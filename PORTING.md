**~~This should be used for the FNF 0.2.8 update and engines that have this version of FNF~~**

<details>
  <summary>Windows Compile Instructions for Android</summary>

1. Download
* [JDK](https://www.azul.com/core-post-download/?endpoint=zulu&uuid=3c8a1a48-ccfa-4072-8b24-97883f2accd5) 8 (32 bit)
* [JDK](https://www.azul.com/core-post-download/?endpoint=zulu&uuid=9768f87c-594f-4d61-9255-4634e3fe4ad3) 8 (64 bit)
* [SDK](https://www.mediafire.com/file/nmk5g9bg58rmnpt/Sdk.7z/file) 29 (32/64 bit)
* [NDK](https://dl.google.com/android/repository/android-ndk-r15c-windows-x86.zip) r15c (32 bit)
* [NDK](https://dl.google.com/android/repository/android-ndk-r15c-windows-x86_64.zip) r15c (64 bit)

2. Extract them
	
3. Open CMD/Powershell and do these commands:
```sh
cd (path of sdk)/cmdline-tools/bin
./sdkmanager.bat --sdk_root=(path of sdk) --licenses
```
And accept all of the licenses

4. Run command `lime setup android` in CMD/PowerShell (You need to insert the program paths)

5. Open project in CMD/PowerShell `cd (path to fnf source)`
And run command `lime build android -final`
The apk will be generated in this path (path to source)`\export\release\android\bin\app\build\outputs\apk\debug`
</details>

<details>
	<summary>Android NDK and SDK for ARM64</summary>

* [JDK](https://www.mediafire.com/file/gw0cvq5u3jfnj4m/jdk11aarch64.tar.xz/file) 11
* [SDK + NDK](https://www.mediafire.com/file/ypvbco88dvrkqtk/sdk%252Bndkr21baarch64.tar.xz/file) r21b (Recommended)
* [SDK + NDK](https://www.mediafire.com/file/9q9m0il8vqu7qg6/sdk%252Bndkr17cfixaarch64.tar.xz/file) r17c fixed
</details>


## Instructions

1. You Need to install `extension-androidtools`

To Install it You Need To Open Command prompt/PowerShell And Type
```cmd
haxelib git extension-androidtools https://github.com/MAJigsaw77/extension-androidtools.git
```

2. Download the repository code and paste it in your source code folder

3. You Need to add these things in `Project.xml`

On This Line
```xml
	<!--Mobile-specific-->
	<window if="mobile" orientation="landscape" fullscreen="true" width="0" height="0" resizable="false" />
```

Replace It With
```xml
	<!--Mobile-specific-->
	<window if="mobile" orientation="landscape" fullscreen="true" width="1280" height="720" resizable="false"/>
```

Then, After the Libraries, or where the packeges are located add
```xml
	<haxelib name="extension-androidtools" if="android" />
```

Add
```xml
	<!-- Do whatever you want I'm tired uninstall and install everytime -->
	<certificate path="key.keystore" password="psychengine" alias="psychport" alias-password="psychengine" if="android" unless="debug" />
```

4. Setup Controls.hx

After these lines
```haxe
import flixel.input.gamepad.FlxGamepadInputID;
import flixel.input.keyboard.FlxKey;
```

Add
```haxe
#if mobile
import flixel.group.FlxGroup;
import mobile.flixel.FlxVirtualPad;
#end
```

Before these lines
```haxe
override function update()
{
	super.update();
}
```

Add
```haxe
	public var trackedInputsUI:Array<FlxActionInput> = [];
	public var trackedInputsNOTES:Array<FlxActionInput> = [];

	public function addButtonNOTES(action:FlxActionDigital, button:FlxButton, state:FlxInputState):Void
	{
		var input:FlxActionInputDigitalIFlxInput = new FlxActionInputDigitalIFlxInput(button, state);
		trackedInputsNOTES.push(input);
		action.add(input);
	}

	public function addButtonUI(action:FlxActionDigital, button:FlxButton, state:FlxInputState):Void
	{
		if (button == null)
			return;

		var input:FlxActionInputDigitalIFlxInput = new FlxActionInputDigitalIFlxInput(button, state);
		trackedInputsUI.push(input);
		action.add(input);
	}
	
	public function addHitboxNOTES(action:FlxActionDigital, button:FlxButton, state:FlxInputState)
	{
		var input = new FlxActionInputDigitalIFlxInput(button, state);
		trackedInputsNOTES.push(input);
		action.add(input);
	}

	public function setHitBox(hitbox:FlxHitbox) 
	{
		inline forEachBound(Control.NOTE_UP, (action, state) -> addHitboxNOTES(action, hitbox.buttonUp, state));
		inline forEachBound(Control.NOTE_DOWN, (action, state) -> addHitboxNOTES(action, hitbox.buttonDown, state));
		inline forEachBound(Control.NOTE_LEFT, (action, state) -> addHitboxNOTES(action, hitbox.buttonLeft, state));
		inline forEachBound(Control.NOTE_RIGHT, (action, state) -> addHitboxNOTES(action, hitbox.buttonRight, state));	
	}
	
	
	public function setNewHitBox(Hitbox:FlxNewHitbox)
	{
		inline forEachBound(Control.NOTE_UP, (action, state) -> addHitboxNOTES(action, Hitbox.buttonUp, state));
		inline forEachBound(Control.NOTE_DOWN, (action, state) -> addHitboxNOTES(action, Hitbox.buttonDown, state));
		inline forEachBound(Control.NOTE_LEFT, (action, state) -> addHitboxNOTES(action, Hitbox.buttonLeft, state));
		inline forEachBound(Control.NOTE_RIGHT, (action, state) -> addHitboxNOTES(action, Hitbox.buttonRight, state));
		//Extra Controls Later
		inline forEachBound(Control.NOTE_UP, (action, state) -> addHitboxNOTES(action, Hitbox.buttonExtra1, state));
		inline forEachBound(Control.NOTE_DOWN, (action, state) -> addHitboxNOTES(action, Hitbox.buttonExtra2, state));
		inline forEachBound(Control.NOTE_LEFT, (action, state) -> addHitboxNOTES(action, Hitbox.buttonExtra3, state));
		inline forEachBound(Control.NOTE_RIGHT, (action, state) -> addHitboxNOTES(action, Hitbox.buttonExtra4, state));
	}

	public function setVirtualPadUI(VirtualPad:FlxVirtualPad, DPad:FlxDPadMode, Action:FlxActionMode):Void
	{
		if (VirtualPad == null)
			return;

		switch (DPad)
		{
			case UP_DOWN | OptionsC:
				inline forEachBound(Control.UI_UP, (action, state) -> addButtonUI(action, VirtualPad.buttonUp, state));
				inline forEachBound(Control.UI_DOWN, (action, state) -> addButtonUI(action, VirtualPad.buttonDown, state));
			case LEFT_RIGHT:
				inline forEachBound(Control.UI_LEFT, (action, state) -> addButtonUI(action, VirtualPad.buttonLeft, state));
				inline forEachBound(Control.UI_RIGHT, (action, state) -> addButtonUI(action, VirtualPad.buttonRight, state));
			case UP_LEFT_RIGHT:
				inline forEachBound(Control.UI_UP, (action, state) -> addButtonUI(action, VirtualPad.buttonUp, state));
				inline forEachBound(Control.UI_LEFT, (action, state) -> addButtonUI(action, VirtualPad.buttonLeft, state));
				inline forEachBound(Control.UI_RIGHT, (action, state) -> addButtonUI(action, VirtualPad.buttonRight, state));
			case FULL | RIGHT_FULL | PAUSE | CHART_EDITOR | ALL:
				inline forEachBound(Control.UI_UP, (action, state) -> addButtonUI(action, VirtualPad.buttonUp, state));
				inline forEachBound(Control.UI_DOWN, (action, state) -> addButtonUI(action, VirtualPad.buttonDown, state));
				inline forEachBound(Control.UI_LEFT, (action, state) -> addButtonUI(action, VirtualPad.buttonLeft, state));
				inline forEachBound(Control.UI_RIGHT, (action, state) -> addButtonUI(action, VirtualPad.buttonRight, state));
			case DUO:
				inline forEachBound(Control.UI_UP, (action, state) -> addButtonUI(action, VirtualPad.buttonUp, state));
				inline forEachBound(Control.UI_DOWN, (action, state) -> addButtonUI(action, VirtualPad.buttonDown, state));
				inline forEachBound(Control.UI_LEFT, (action, state) -> addButtonUI(action, VirtualPad.buttonLeft, state));
				inline forEachBound(Control.UI_RIGHT, (action, state) -> addButtonUI(action, VirtualPad.buttonRight, state));
				inline forEachBound(Control.UI_UP, (action, state) -> addButtonUI(action, VirtualPad.buttonUp2, state));
				inline forEachBound(Control.UI_DOWN, (action, state) -> addButtonUI(action, VirtualPad.buttonDown2, state));
				inline forEachBound(Control.UI_LEFT, (action, state) -> addButtonUI(action, VirtualPad.buttonLeft2, state));
				inline forEachBound(Control.UI_RIGHT, (action, state) -> addButtonUI(action, VirtualPad.buttonRight2, state));
			case NONE: // do nothing
		}

		switch (Action)
		{
			case A | A_C | A_X_Y | ALL:
				inline forEachBound(Control.ACCEPT, (action, state) -> addButtonUI(action, VirtualPad.buttonA, state));
			case B | B_X_Y | B_E:
				inline forEachBound(Control.BACK, (action, state) -> addButtonUI(action, VirtualPad.buttonB, state));
			case P:
				inline forEachBound(Control.PAUSE, (action, state) -> addButtonUI(action, VirtualPad.buttonP, state));
			case A_B | A_B_C | A_B_E | A_B_E_C_M | A_B_X_Y | A_B_C_X_Y | A_B_C_X_Y_Z | FULL | CHART_EDITOR:
				inline forEachBound(Control.ACCEPT, (action, state) -> addButtonUI(action, VirtualPad.buttonA, state));
				inline forEachBound(Control.BACK, (action, state) -> addButtonUI(action, VirtualPad.buttonB, state));
			case OptionsC:
				inline forEachBound(Control.UI_LEFT, (action, state) -> addButtonUI(action, VirtualPad.buttonLeft, state));
				inline forEachBound(Control.UI_RIGHT, (action, state) -> addButtonUI(action, VirtualPad.buttonRight, state));
				inline forEachBound(Control.ACCEPT, (action, state) -> addButtonUI(action, VirtualPad.buttonA, state));
				inline forEachBound(Control.BACK, (action, state) -> addButtonUI(action, VirtualPad.buttonB, state));
			case NONE | E | controlExtend | D | X_Y: // do nothing
		}
	}

	public function setVirtualPadNOTES(VirtualPad:FlxVirtualPad, DPad:FlxDPadMode, Action:FlxActionMode):Void
	{
		if (VirtualPad == null)
			return;

		switch (DPad)
		{
			case UP_DOWN | OptionsC:
				inline forEachBound(Control.NOTE_UP, (action, state) -> addButtonNOTES(action, VirtualPad.buttonUp, state));
				inline forEachBound(Control.NOTE_DOWN, (action, state) -> addButtonNOTES(action, VirtualPad.buttonDown, state));
			case LEFT_RIGHT:
				inline forEachBound(Control.NOTE_LEFT, (action, state) -> addButtonNOTES(action, VirtualPad.buttonLeft, state));
				inline forEachBound(Control.NOTE_RIGHT, (action, state) -> addButtonNOTES(action, VirtualPad.buttonRight, state));
			case UP_LEFT_RIGHT:
				inline forEachBound(Control.NOTE_UP, (action, state) -> addButtonNOTES(action, VirtualPad.buttonUp, state));
				inline forEachBound(Control.NOTE_LEFT, (action, state) -> addButtonNOTES(action, VirtualPad.buttonLeft, state));
				inline forEachBound(Control.NOTE_RIGHT, (action, state) -> addButtonNOTES(action, VirtualPad.buttonRight, state));
			case FULL | RIGHT_FULL | PAUSE | CHART_EDITOR | ALL:
				inline forEachBound(Control.NOTE_UP, (action, state) -> addButtonNOTES(action, VirtualPad.buttonUp, state));
				inline forEachBound(Control.NOTE_DOWN, (action, state) -> addButtonNOTES(action, VirtualPad.buttonDown, state));
				inline forEachBound(Control.NOTE_LEFT, (action, state) -> addButtonNOTES(action, VirtualPad.buttonLeft, state));
				inline forEachBound(Control.NOTE_RIGHT, (action, state) -> addButtonNOTES(action, VirtualPad.buttonRight, state));
			case DUO:
				inline forEachBound(Control.NOTE_UP, (action, state) -> addButtonNOTES(action, VirtualPad.buttonUp, state));
				inline forEachBound(Control.NOTE_DOWN, (action, state) -> addButtonNOTES(action, VirtualPad.buttonDown, state));
				inline forEachBound(Control.NOTE_LEFT, (action, state) -> addButtonNOTES(action, VirtualPad.buttonLeft, state));
				inline forEachBound(Control.NOTE_RIGHT, (action, state) -> addButtonNOTES(action, VirtualPad.buttonRight, state));
				inline forEachBound(Control.NOTE_UP, (action, state) -> addButtonNOTES(action, VirtualPad.buttonUp2, state));
				inline forEachBound(Control.NOTE_DOWN, (action, state) -> addButtonNOTES(action, VirtualPad.buttonDown2, state));
				inline forEachBound(Control.NOTE_LEFT, (action, state) -> addButtonNOTES(action, VirtualPad.buttonLeft2, state));
				inline forEachBound(Control.NOTE_RIGHT, (action, state) -> addButtonNOTES(action, VirtualPad.buttonRight2, state));
			case NONE: // do nothing
		}

		switch (Action)
		{
			case A | A_C | A_X_Y | ALL:
				inline forEachBound(Control.ACCEPT, (action, state) -> addButtonNOTES(action, VirtualPad.buttonA, state));
			case B | B_X_Y | B_E:
				inline forEachBound(Control.BACK, (action, state) -> addButtonNOTES(action, VirtualPad.buttonB, state));
			case P:
				inline forEachBound(Control.PAUSE, (action, state) -> addButtonNOTES(action, VirtualPad.buttonP, state));
			case A_B | A_B_C | A_B_E | A_B_E_C_M | A_B_X_Y | A_B_C_X_Y | A_B_C_X_Y_Z | FULL | CHART_EDITOR:
				inline forEachBound(Control.ACCEPT, (action, state) -> addButtonNOTES(action, VirtualPad.buttonA, state));
				inline forEachBound(Control.BACK, (action, state) -> addButtonNOTES(action, VirtualPad.buttonB, state));
			case OptionsC:
				inline forEachBound(Control.ACCEPT, (action, state) -> addButtonNOTES(action, VirtualPad.buttonA, state));
				inline forEachBound(Control.BACK, (action, state) -> addButtonNOTES(action, VirtualPad.buttonB, state));
				inline forEachBound(Control.NOTE_LEFT, (action, state) -> addButtonNOTES(action, VirtualPad.buttonLeft, state));
				inline forEachBound(Control.NOTE_RIGHT, (action, state) -> addButtonNOTES(action, VirtualPad.buttonRight, state));
			case NONE | E | controlExtend | D | X_Y: // do nothing
		}
	}
	
	public function removeVirtualControlsInput(Tinputs:Array<FlxActionInput>):Void
	{
		for (action in this.digitalActions)
		{
			var i = action.inputs.length;
			while (i-- > 0)
			{
				var x = Tinputs.length;
				while (x-- > 0)
				{
					if (Tinputs[x] == action.inputs[i])
						action.remove(action.inputs[i]);
				}
			}
		}
	}	
```

5. Setup MusicBeatState.hx

In the lines you import things add
```haxe
import flixel.input.actions.FlxActionInput;
import mobile.flixel.FlxVirtualPad;
import flixel.util.FlxDestroyUtil;
```

After these lines
```haxe
inline function get_controls():Controls
	return PlayerSettings.player1.controls;
```

Add
```haxe
	public static var checkHitbox:Bool = false;
	
	var _virtualpad:FlxVirtualPad;
	public static var mobilec:MobileControls;
	
	var trackedinputsUI:Array<FlxActionInput> = [];
	var trackedinputsNOTES:Array<FlxActionInput> = [];

	public function addVirtualPad(?DPad:FlxDPadMode, ?Action:FlxActionMode) {		
		if (_virtualpad != null)
			removeVirtualPad();

		_virtualpad = new FlxVirtualPad(DPad, Action, 0.75, ClientPrefs.globalAntialiasing);
		add(_virtualpad);

		controls.setVirtualPadUI(_virtualpad, DPad, Action);
		trackedinputsUI = controls.trackedInputsUI;
		controls.trackedInputsUI = [];
	}
	
	public function removeVirtualPad() {
		if (trackedinputsUI.length > 0)
			controls.removeVirtualControlsInput(trackedinputsUI);

		if (_virtualpad != null)
			remove(_virtualpad);
	}
	
	public function removeMobileControls() {
		if (trackedinputsNOTES.length > 0)
			controls.removeVirtualControlsInput(trackedinputsNOTES);
			
		if (mobilec != null)
			remove(mobilec);
	}
	
	public function addMobileControls() {
		mobilec = new MobileControls();

		switch (mobilec.mode)
		{
			case VIRTUALPAD_RIGHT | VIRTUALPAD_LEFT | VIRTUALPAD_CUSTOM:
				controls.setVirtualPadNOTES(mobilec.vpad, FULL, NONE);
				MusicBeatState.checkHitbox = false;
			case DUO:
				controls.setVirtualPadNOTES(mobilec.vpad, DUO, NONE);
				MusicBeatState.checkHitbox = false;
			case HITBOX:
				if(ClientPrefs.hitboxmode != 'New')
				    controls.setHitBox(mobilec.hbox);
				else
				    controls.setNewHitBox(mobilec.newhbox);
				MusicBeatState.checkHitbox = true;
			default:
		}

		trackedinputsNOTES = controls.trackedInputsNOTES;
		controls.trackedInputsNOTES = [];

		var camcontrol = new flixel.FlxCamera();
		FlxG.cameras.add(camcontrol, false);
		camcontrol.bgColor.alpha = 0;
		mobilec.cameras = [camcontrol];

		add(mobilec);
	}
	
    public function addVirtualPadCamera() {
		var camcontrol = new flixel.FlxCamera();
		camcontrol.bgColor.alpha = 0;
		FlxG.cameras.add(camcontrol, false);
		_virtualpad.cameras = [camcontrol];
	}
	
	override function destroy() {
		if (trackedinputsNOTES.length > 0)
			controls.removeVirtualControlsInput(trackedinputsNOTES);

		if (trackedinputsUI.length > 0)
			controls.removeVirtualControlsInput(trackedinputsUI);

		super.destroy();

		if (_virtualpad != null)
			_virtualpad = FlxDestroyUtil.destroy(_virtualpad);

		if (mobilec != null)
			mobilec = FlxDestroyUtil.destroy(mobilec);
	}
```

6. Setup MusicBeatSubstate.hx

In the lines you import things add
```haxe
import flixel.input.actions.FlxActionInput;
import mobile.flixel.FlxVirtualPad;
```

After these lines
```haxe
inline function get_controls():Controls
	return PlayerSettings.player1.controls;
```

Add
```haxe
	var _virtualpad:FlxVirtualPad;
	var trackedinputsUI:Array<FlxActionInput> = [];
	var trackedinputsNOTES:Array<FlxActionInput> = [];
	
	public function addVirtualPad(?DPad:FlxDPadMode, ?Action:FlxActionMode) {
		_virtualpad = new FlxVirtualPad(DPad, Action, 0.75, ClientPrefs.globalAntialiasing);
		add(_virtualpad);
		controls.setVirtualPadUI(_virtualpad, DPad, Action);
		trackedinputsUI = controls.trackedInputsUI;
		controls.trackedInputsUI = [];
	}

	public function removeVirtualPad() {
		if (trackedinputsUI.length > 0)
			controls.removeVirtualControlsInput(trackedinputsUI);

		if (_virtualpad != null)
			remove(_virtualpad);
	}

	public function addVirtualPadCamera() {
		var camcontrol = new flixel.FlxCamera();
		camcontrol.bgColor.alpha = 0;
		FlxG.cameras.add(camcontrol, false);
		_virtualpad.cameras = [camcontrol];
	}
	
	override function destroy() {
		if (trackedinputsUI.length > 0)
			controls.removeVirtualControlsInput(trackedinputsUI);

		super.destroy();

		if (_virtualpad != null)
			_virtualpad = FlxDestroyUtil.destroy(_virtualpad);
	}
```

And somehow you finished adding the mobile controls to your mod now on every state/substate add
```haxe
addVirtualPad(LEFT_FULL, A_B);

//if you want to remove it at some moment use
removeVirtualPad();

//if you want it to have a camera
addVirtualPadCamera();
//in states, these need to be added before super.create();
//in substates, in fuction new at the last line add these

//on Playstate.hx after all of the
//obj.cameras = [...];
//things, add
addMobileControls();

//if you want to remove it at some moment use
removeMobileControls();

//to make the controls visible the code is
mobileControls.visible = true;

//to make the controls invisible the code is
mobileControls.visible = false;
```

7. Prevent the Android BACK Button

in TitleState.hx

After
```haxe
override public function create():Void
```

Add
```haxe
#if android
FlxG.android.preventDefaultKeys = [BACK];
#end
```

8. Set An action to the BACK Button

You can set one with
```haxe
#if android || FlxG.android.justReleased.BACK #end
```

9. On `sys.FileSystem`, `sys.io.File` Stuff

This will make the game use the phone storage but you will have to add one thing in your source

In main.hx after
```haxe
public function new()
```

Add
```haxe
            #if mobile
	    #if android
		SUtil.doPermissionsShit();
		if (!FileSystem.exists(SUtil.getStorageDirectory()))
			FileSystem.createDirectory(SUtil.getStorageDirectory());
		#end
		Sys.setCwd(SUtil.getStorageDirectory());
		#end
		
		#if android
		if (!FileSystem.exists(SUtil.getStorageDirectory()))
			FileSystem.createDirectory(SUtil.getStorageDirectory());
	    #end
```

This will check for android storage permisions and the `assets` or `mods` directories

10. On Crash Application Alert

On Main.hx after
```haxe
public function new()
```

Add
```haxe
SUtil.gameCrashCheck();
```

11. File Saver

This is a feature to save files with sys.io.File in phone storage in `saves` directory

```haxe
SUtil.saveContent("your file name.txt", "lololol");
```

12. Do an action when you press on the screen

```haxe
#if mobile
var justTouched:Bool = false;

for (touch in FlxG.touches.list)
	if (touch.justPressed)
		justTouched = true;

if (justTouched)
	//Your code
#end
```

13. Now we need to add more thing for Mobile Controls

On ClientPrefs.hx after
```haxe
public static var downScroll:Bool = false;
```

Add
```haxe
public static var extraKeys:Int = 2;
public static var hitboxLocation:String = 'Bottom';
public static var hitboxmode:String = 'New';
public static var hitboxtype:String = 'Gradient';
public static var storageType:String = 'EXTERNAL';
public static var hitboxhint:Bool = false;
public static var VirtualPadAlpha:Float = 0.75;
public static var hitboxalpha:Float = 0.7;
```

After
```haxe
FlxG.save.data.downScroll = downScroll;
```

Add
```haxe
FlxG.save.data.extraKeys = extraKeys;
FlxG.save.data.hitboxLocation = hitboxLocation;
FlxG.save.data.hitboxhint = hitboxhint;
FlxG.save.data.hitboxmode = hitboxmode;
FlxG.save.data.hitboxtype = hitboxtype;
FlxG.save.data.storageType = storageType;
FlxG.save.data.VirtualPadAlpha = VirtualPadAlpha;
FlxG.save.data.hitboxalpha = hitboxalpha;
```

After
```haxe
if(FlxG.save.data.downScroll != null) {
	downScroll = FlxG.save.data.downScroll;
}
```

Add
```haxe
if(FlxG.save.data.extraKeys != null) {
	extraKeys = FlxG.save.data.extraKeys;
}
if(FlxG.save.data.hitboxLocation != null) {
	hitboxLocation = FlxG.save.data.hitboxLocation;
}
if(FlxG.save.data.hitboxhint != null) {
	hitboxhint = FlxG.save.data.hitboxhint;
}
if(FlxG.save.data.hitboxmode != null) {
	hitboxmode = FlxG.save.data.hitboxmode;
}
if(FlxG.save.data.hitboxtype != null) {
	hitboxtype = FlxG.save.data.hitboxtype;
}
if(FlxG.save.data.storageType != null) {
	storageType = FlxG.save.data.storageType;
}
if(FlxG.save.data.VirtualPadAlpha != null) {
	VirtualPadAlpha = FlxG.save.data.VirtualPadAlpha;
}
if(FlxG.save.data.hitboxalpha != null) {
	hitboxalpha = FlxG.save.data.hitboxalpha;
}
```

14. CopyState (optional)

in Main.hx
On This Line
```haxe
	addChild(new FlxGame(game.width, game.height, game.initialState, #if (flixel < "5.0.0") game.zoom, #end game.framerate, game.framerate, game.skipSplash, game.startFullscreen));
```

Replace It With
```haxd
	addChild(new FlxGame(game.width, game.height, #if (mobile && MODS_ALLOWED) CopyState.checkExistingFiles() ? game.initialState : CopyState #else game.initialState #end, #if (flixel < "5.0.0") game.zoom, #end game.framerate, game.framerate, game.skipSplash, game.startFullscreen));
```
