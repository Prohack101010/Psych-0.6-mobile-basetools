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

-1. Before the start, you need to add a few things for Mobile Controls

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
public static var storageType:String = 'EXTERNAL_DATA';
public static var hitboxhint:Bool = false;
public static var VirtualPadAlpha:Float = 0.75;
public static var hitboxalpha:Float = 0.7;
public static var extraKeyReturn1:String = 'SHIFT';
public static var extraKeyReturn2:String = 'SPACE';
public static var extraKeyReturn3:String = 'Q';
public static var extraKeyReturn4:String = 'E';
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
FlxG.save.data.extraKeyReturn1 = extraKeyReturn1;
FlxG.save.data.extraKeyReturn2 = extraKeyReturn2;
FlxG.save.data.extraKeyReturn3 = extraKeyReturn3;
FlxG.save.data.extraKeyReturn4 = extraKeyReturn4;
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
if(FlxG.save.data.extraKeyReturn1 != null) {
	extraKeyReturn1 = FlxG.save.data.extraKeyReturn1;
}
if(FlxG.save.data.extraKeyReturn2 != null) {
	extraKeyReturn2 = FlxG.save.data.extraKeyReturn2;
}
if(FlxG.save.data.extraKeyReturn3 != null) {
	extraKeyReturn3 = FlxG.save.data.extraKeyReturn3;
}
if(FlxG.save.data.extraKeyReturn4 != null) {
	extraKeyReturn4 = FlxG.save.data.extraKeyReturn4;
}
```

1. You Need to install spesific `extension-androidtools` version for 0.6.3

To Install it You Need To Open Command prompt/PowerShell And Type
```cmd
haxelib git extension-androidtools https://github.com/MAJigsaw77/extension-androidtools.git 727693f0a76c6e396df675bb0ed95d7639a4db01
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
        #if mobile
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
		inline forEachBound(Control.EXTRA1, (action, state) -> addHitboxNOTES(action, Hitbox.buttonExtra1, state));
		inline forEachBound(Control.EXTRA2, (action, state) -> addHitboxNOTES(action, Hitbox.buttonExtra2, state));
		inline forEachBound(Control.EXTRA3, (action, state) -> addHitboxNOTES(action, Hitbox.buttonExtra3, state));
		inline forEachBound(Control.EXTRA4, (action, state) -> addHitboxNOTES(action, Hitbox.buttonExtra4, state));
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
        #end	
```

After
```haxe
var RESET = "reset";
```

Add
```haxe
        #if mobile
	var EXTRA1 = 'extra1';
	var EXTRA1_P = 'extra1-press';
	var EXTRA1_R = 'extra1-release';
	var EXTRA2 = 'extra2';
	var EXTRA2_P = 'extra2-press';
	var EXTRA2_R = 'extra2-release';
	var EXTRA3 = 'extra3';
	var EXTRA3_P = 'extra3-press';
	var EXTRA3_R = 'extra3-release';
	var EXTRA4 = 'extra4';
	var EXTRA4_P = 'extra4-press';
	var EXTRA4_R = 'extra4-release';
        #end
```

After these lines
```haxe
	ACCEPT;
	BACK;
	PAUSE;
```

Add
```haxe
        #if mobile
	EXTRA1;
	EXTRA2;
	EXTRA3;
	EXTRA4;
        #end
```

After
```haxe
var _reset = new FlxActionDigital(Action.RESET);
```

Add
```haxe
        #if mobile
	var _extra1 = new FlxActionDigital(Action.EXTRA1);
	var _extra1P = new FlxActionDigital(Action.EXTRA1_P);
	var _extra1R = new FlxActionDigital(Action.EXTRA1_R);
	var _extra2 = new FlxActionDigital(Action.EXTRA2);
	var _extra2P = new FlxActionDigital(Action.EXTRA2_P);
	var _extra2R = new FlxActionDigital(Action.EXTRA2_R);
	var _extra3 = new FlxActionDigital(Action.EXTRA3);
	var _extra3P = new FlxActionDigital(Action.EXTRA3_P);
	var _extra3R = new FlxActionDigital(Action.EXTRA3_R);
	var _extra4 = new FlxActionDigital(Action.EXTRA4);
	var _extra4P = new FlxActionDigital(Action.EXTRA4_P);
	var _extra4R = new FlxActionDigital(Action.EXTRA4_R);
        #end
```

After these lines
```haxe
	public var RESET(get, never):Bool;

	inline function get_RESET()
		return _reset.check();
```

Add
```haxe
        #if mobile
	public var EXTRA1(get, never):Bool;

	inline function get_EXTRA1()
		return _extra1.check();		
	
	public var EXTRA1_R(get, never):Bool;

	inline function get_EXTRA1_R()
		return _extra1R.check();		
		
	public var EXTRA1_P(get, never):Bool;

	inline function get_EXTRA1_P()
		return _extra1P.check();
	
	public var EXTRA2(get, never):Bool;

	inline function get_EXTRA2()
		return _extra2.check();		
	
	public var EXTRA2_R(get, never):Bool;

	inline function get_EXTRA2_R()
		return _extra2R.check();		
		
	public var EXTRA2_P(get, never):Bool;

	inline function get_EXTRA2_P()
		return _extra2P.check();			

	public var EXTRA3(get, never):Bool;

	inline function get_EXTRA3()
		return _extra3.check();		
	
	public var EXTRA3_R(get, never):Bool;

	inline function get_EXTRA3_R()
		return _extra3R.check();		
		
	public var EXTRA3_P(get, never):Bool;

	inline function get_EXTRA3_P()
		return _extra3P.check();

	public var EXTRA4(get, never):Bool;

	inline function get_EXTRA4()
		return _extra4.check();		
	
	public var EXTRA4_R(get, never):Bool;

	inline function get_EXTRA4_R()
		return _extra4R.check();		
		
	public var EXTRA4_P(get, never):Bool;

	inline function get_EXTRA4_P()
		return _extra4P.check();
        #end
```

After these lines
```haxe
		add(_back);
		add(_pause);
		add(_reset);
```

Add
```haxe
                #if mobile
		add(_extra1);
		add(_extra1P);
		add(_extra1R);
		add(_extra2);
		add(_extra2P);
		add(_extra2R);
		add(_extra3);
		add(_extra3P);
		add(_extra3R);
		add(_extra4);
		add(_extra4P);
		add(_extra4R);
                #end
```

After
```haxe
case RESET: _reset;
```

Add
```haxe
			#if mobile
			case EXTRA1: _extra1;
			case EXTRA2: _extra2;		
			case EXTRA3: _extra3;
			case EXTRA4: _extra4;
			#end
```

After these lines
```haxe
			case RESET:
				func(_reset, JUST_PRESSED);
```

Add
```haxe
			#if mobile
			case EXTRA1:
				func(_extra1, PRESSED);
				func(_extra1P, JUST_PRESSED);
				func(_extra1R, JUST_RELEASED);
			case EXTRA2:
				func(_extra2, PRESSED);
				func(_extra2P, JUST_PRESSED);
				func(_extra2R, JUST_RELEASED);
			case EXTRA3:
				func(_extra3, PRESSED);
				func(_extra3P, JUST_PRESSED);
				func(_extra3R, JUST_RELEASED);
			case EXTRA4:
				func(_extra4, PRESSED);
				func(_extra4P, JUST_PRESSED);
				func(_extra4R, JUST_RELEASED);
			#end
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
	#if mobile
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
	#end
```

6. Setup MusicBeatSubstate.hx

In the lines you import things add
```haxe
#if mobile
import flixel.input.actions.FlxActionInput;
import mobile.flixel.FlxVirtualPad;
#end
```

After these lines
```haxe
inline function get_controls():Controls
	return PlayerSettings.player1.controls;
```

Add
```haxe
	#if mobile
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
	#end
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
#if mobile
SUtil.gameCrashCheck();
#end
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

13. Finish Extra Controls

in FunkinLua.hx after these lines
```haxe
    	public var camTarget:FlxCamera;
	public var scriptName:String = '';
	public var closed:Bool = false;
```

Add
```haxe
	#if mobile
    	public var extra1:String = ClientPrefs.extraKeyReturn1.toUpperCase();
	public var extra2:String = ClientPrefs.extraKeyReturn2.toUpperCase();
	public var extra3:String = ClientPrefs.extraKeyReturn3.toUpperCase();
	public var extra4:String = ClientPrefs.extraKeyReturn4.toUpperCase();
	#end
```

On This Line
```haxe
	    	Lua_helper.add_callback(lua, "keyboardJustPressed", function(name:String)
		{
			return Reflect.getProperty(FlxG.keys.justPressed, name);
		});
		Lua_helper.add_callback(lua, "keyboardPressed", function(name:String)
		{
			return Reflect.getProperty(FlxG.keys.pressed, name);
		});
		Lua_helper.add_callback(lua, "keyboardReleased", function(name:String)
		{
			return Reflect.getProperty(FlxG.keys.justReleased, name);
		});
```

Replace It With
```haxe
	    	Lua_helper.add_callback(lua, "keyboardJustPressed", function(name:String)
		{
			#if mobile
            if (MusicBeatState.mobilec.newhbox != null && ClientPrefs.extraKeys != 0){
                if (name == extra1 && MusicBeatState.mobilec.newhbox.buttonExtra1.justPressed)
    			    return true;
			    if (name == extra2 && MusicBeatState.mobilec.newhbox.buttonExtra2.justPressed)
    			    return true;
                if (name == extra3 && MusicBeatState.mobilec.newhbox.buttonExtra3.justPressed)
    			    return true;
                if (name == extra4 && MusicBeatState.mobilec.newhbox.buttonExtra4.justPressed)
    			    return true;
            }
            
            if (MusicBeatState.mobilec.vpad != null && ClientPrefs.extraKeys != 0){
                if (name == extra1 && MusicBeatState.mobilec.vpad.buttonExtra1.justPressed)
    			    return true;
			    if (name == extra2 && MusicBeatState.mobilec.vpad.buttonExtra2.justPressed)
    			    return true;
                if (name == extra3 && MusicBeatState.mobilec.vpad.buttonExtra3.justPressed)
    			    return true;
                if (name == extra4 && MusicBeatState.mobilec.vpad.buttonExtra4.justPressed)
    			    return true;
            }
            #end
			return Reflect.getProperty(FlxG.keys.justPressed, name);
		});
		Lua_helper.add_callback(lua, "keyboardPressed", function(name:String)
		{
		     #if mobile
           if (MusicBeatState.mobilec.newhbox != null && ClientPrefs.extraKeys != 0){
			    if (name == extra1 && MusicBeatState.mobilec.newhbox.buttonExtra1.pressed)
    			    return true;
                if (name == extra2 && MusicBeatState.mobilec.newhbox.buttonExtra2.pressed)
    			    return true;
                if (name == extra3 && MusicBeatState.mobilec.newhbox.buttonExtra3.pressed)
    			    return true;
                if (name == extra4 && MusicBeatState.mobilec.newhbox.buttonExtra4.pressed)
    			    return true;
           }
           if (MusicBeatState.mobilec.vpad != null && ClientPrefs.extraKeys != 0){
                if (name == extra4 && MusicBeatState.mobilec.vpad.buttonExtra4.pressed)
    			    return true;
                if (name == extra3 && MusicBeatState.mobilec.vpad.buttonExtra3.pressed)
    			    return true;
			    if (name == extra2 && MusicBeatState.mobilec.vpad.buttonExtra2.pressed)
    			    return true;                          
                if (name == extra1 && MusicBeatState.mobilec.vpad.buttonExtra1.pressed)
    			    return true;
           }
           #end
			return Reflect.getProperty(FlxG.keys.pressed, name);
		});
		Lua_helper.add_callback(lua, "keyboardReleased", function(name:String)
		{
		    #if mobile
           if (MusicBeatState.mobilec.newhbox != null && ClientPrefs.extraKeys != 0){
                if (name == extra1 && MusicBeatState.mobilec.newhbox.buttonExtra1.justReleased)
    			    return true;
			    if (name == extra2 && MusicBeatState.mobilec.newhbox.buttonExtra2.justReleased)
    			    return true;
                if (name == extra3 && MusicBeatState.mobilec.newhbox.buttonExtra3.justReleased)
    			    return true;
                if (name == extra4 && MusicBeatState.mobilec.newhbox.buttonExtra4.justReleased)
    			    return true;
           }
           if (MusicBeatState.mobilec.vpad != null && ClientPrefs.extraKeys != 0){
                if (name == extra1 && MusicBeatState.mobilec.vpad.buttonExtra1.justReleased)
    			    return true;
			    if (name == extra2 && MusicBeatState.mobilec.vpad.buttonExtra2.justReleased)
    			    return true;
                if (name == extra3 && MusicBeatState.mobilec.vpad.buttonExtra3.justReleased)
    			    return true;
                if (name == extra4 && MusicBeatState.mobilec.vpad.buttonExtra4.justReleased)
    			    return true;
           }
           #end
			return Reflect.getProperty(FlxG.keys.justReleased, name);
		});
```

On This Line
```haxe
	    	Lua_helper.add_callback(lua, "keyJustPressed", function(name:String) {
			var key:Bool = false;
			switch(name) {
				case 'left': key = PlayState.instance.getControl('NOTE_LEFT_P');
				case 'down': key = PlayState.instance.getControl('NOTE_DOWN_P');
				case 'up': key = PlayState.instance.getControl('NOTE_UP_P');
				case 'right': key = PlayState.instance.getControl('NOTE_RIGHT_P');
				case 'accept': key = PlayState.instance.getControl('ACCEPT');
				case 'back': key = PlayState.instance.getControl('BACK');
				case 'pause': key = PlayState.instance.getControl('PAUSE');
				case 'reset': key = PlayState.instance.getControl('RESET');
				case 'space': key = FlxG.keys.justPressed.SPACE;//an extra key for convinience
			}
			return key;
		});
		Lua_helper.add_callback(lua, "keyPressed", function(name:String) {
			var key:Bool = false;
			switch(name) {
				case 'left': key = PlayState.instance.getControl('NOTE_LEFT');
				case 'down': key = PlayState.instance.getControl('NOTE_DOWN');
				case 'up': key = PlayState.instance.getControl('NOTE_UP');
				case 'right': key = PlayState.instance.getControl('NOTE_RIGHT');
				case 'space': key = FlxG.keys.pressed.SPACE;//an extra key for convinience
			}
			return key;
		});
		Lua_helper.add_callback(lua, "keyReleased", function(name:String) {
			var key:Bool = false;
			switch(name) {
				case 'left': key = PlayState.instance.getControl('NOTE_LEFT_R');
				case 'down': key = PlayState.instance.getControl('NOTE_DOWN_R');
				case 'up': key = PlayState.instance.getControl('NOTE_UP_R');
				case 'right': key = PlayState.instance.getControl('NOTE_RIGHT_R');
				case 'space': key = FlxG.keys.justReleased.SPACE;//an extra key for convinience
			}
			return key;
		});
```

Replace It With
```haxe
	    	Lua_helper.add_callback(lua, "keyJustPressed", function(name:String) {
			var key:Bool = false;
			#if mobile
			if (name == extra1)
			    key = PlayState.instance.getControl('EXTRA1_P');
		    if (name == extra2)
		        key = PlayState.instance.getControl('EXTRA2_P');
		    if (name == extra3)
		        key = PlayState.instance.getControl('EXTRA3_P');
		    if (name == extra4)
		        key = PlayState.instance.getControl('EXTRA4_P');
			#end
			switch(name) {
				case 'left': key = PlayState.instance.getControl('NOTE_LEFT_P');
				case 'down': key = PlayState.instance.getControl('NOTE_DOWN_P');
				case 'up': key = PlayState.instance.getControl('NOTE_UP_P');
				case 'right': key = PlayState.instance.getControl('NOTE_RIGHT_P');
				case 'accept': key = PlayState.instance.getControl('ACCEPT');
				case 'back': key = PlayState.instance.getControl('BACK');
				case 'pause': key = PlayState.instance.getControl('PAUSE');
				case 'reset': key = PlayState.instance.getControl('RESET');	
				case 'space': key = FlxG.keys.justPressed.SPACE;//an extra key for convinience
				case 'ui_left': key = PlayState.instance.getControl('UI_LEFT_P');
				case 'ui_down': key = PlayState.instance.getControl('UI_DOWN_P');
				case 'ui_up': key = PlayState.instance.getControl('UI_UP_P');
				case 'ui_right': key = PlayState.instance.getControl('UI_RIGHT_P');
			}
			return key;
		});
		Lua_helper.add_callback(lua, "keyPressed", function(name:String) {
			var key:Bool = false;
			#if mobile
			if (name == extra1)
			    key = PlayState.instance.getControl('EXTRA1');
		    if (name == extra2)
		        key = PlayState.instance.getControl('EXTRA2');
		    if (name == extra3)
		        key = PlayState.instance.getControl('EXTRA3');
		    if (name == extra4)
		        key = PlayState.instance.getControl('EXTRA4');
			#end
			switch(name) {
				case 'left': key = PlayState.instance.getControl('NOTE_LEFT');
				case 'down': key = PlayState.instance.getControl('NOTE_DOWN');
				case 'up': key = PlayState.instance.getControl('NOTE_UP');
				case 'right': key = PlayState.instance.getControl('NOTE_RIGHT');
				case 'space': key = FlxG.keys.pressed.SPACE;//an extra key for convinience
				case 'ui_left': key = PlayState.instance.getControl('UI_LEFT');
				case 'ui_down': key = PlayState.instance.getControl('UI_DOWN');
				case 'ui_up': key = PlayState.instance.getControl('UI_UP');
				case 'ui_right': key = PlayState.instance.getControl('UI_RIGHT');
			}
			return key;
		});
		Lua_helper.add_callback(lua, "keyReleased", function(name:String) {
			var key:Bool = false;
			#if mobile
			if (name == extra1)
			    key = PlayState.instance.getControl('EXTRA1_R');
		    if (name == extra2)
		        key = PlayState.instance.getControl('EXTRA2_R');
		    if (name == extra3)
		        key = PlayState.instance.getControl('EXTRA3_R');
		    if (name == extra4)
		        key = PlayState.instance.getControl('EXTRA4_R');
			#end
			switch(name) {
				case 'left': key = PlayState.instance.getControl('NOTE_LEFT_R');
				case 'down': key = PlayState.instance.getControl('NOTE_DOWN_R');
				case 'up': key = PlayState.instance.getControl('NOTE_UP_R');
				case 'right': key = PlayState.instance.getControl('NOTE_RIGHT_R');		
				case 'space': key = FlxG.keys.justReleased.SPACE;//an extra key for convinience
				case 'ui_left': key = PlayState.instance.getControl('UI_LEFT_R');
				case 'ui_down': key = PlayState.instance.getControl('UI_DOWN_R');
				case 'ui_up': key = PlayState.instance.getControl('UI_UP_R');
				case 'ui_right': key = PlayState.instance.getControl('UI_RIGHT_R');
			}
			return key;
		});
```

On This Line
```haxe
	    Lua_helper.add_callback(lua, "getPropertyFromClass", function(classVar:String, variable:String) {
			@:privateAccess
			var killMe:Array<String> = variable.split('.');
			if(killMe.length > 1) {
				var coverMeInPiss:Dynamic = getVarInArray(Type.resolveClass(classVar), killMe[0]);
				for (i in 1...killMe.length-1) {
					coverMeInPiss = getVarInArray(coverMeInPiss, killMe[i]);
				}
				return getVarInArray(coverMeInPiss, killMe[killMe.length-1]);
			}
			return getVarInArray(Type.resolveClass(classVar), variable);
		});
```

Replace It With
```haxe
    		Lua_helper.add_callback(lua, "getPropertyFromClass", function(classVar:String, variable:String) {
			@:privateAccess
			#if mobile
			var myClass:Dynamic = classCheck(classVar);
			var variableplus:String = varCheck(myClass, variable);
			#end
			var killMe:Array<String> = variable.split('.');
			#if mobile
			if (MusicBeatState.mobilec != null && myClass == 'flixel.FlxG' && variableplus.indexOf('key') != -1){
    		    var check:Dynamic;
    		    check = specialKeyCheck(variableplus); //fuck you old lua 🙃
    		    if (check != null) return check;
    		}
			#end
           
			if(killMe.length > 1) {
				var coverMeInPiss:Dynamic = getVarInArray(Type.resolveClass(classVar), killMe[0]);
				for (i in 1...killMe.length-1) {
					coverMeInPiss = getVarInArray(coverMeInPiss, killMe[i]);
				}
				return getVarInArray(coverMeInPiss, killMe[killMe.length-1]);
			}
			return getVarInArray(Type.resolveClass(classVar), variable);
		});
```

After
```haxe
    	public function stop() {
		#if LUA_ALLOWED
		if(lua == null) {
			return;
		}

		Lua.close(lua);
		lua = null;
		#end
	}
```

Add
```haxe
	#if mobile
    	public static function varCheck(className:Dynamic, variable:String):String{
	    return variable;
	}
	
	public static function classCheck(className:String):Dynamic
	{
	    return Type.resolveClass(className);
	}
	
	public static function specialKeyCheck(keyName:String):Dynamic
	{
	    var textfix:Array<String> = keyName.trim().split('.');
	    var type:String = textfix[1].trim();
	    var key:String = textfix[2].trim();    			
	    var extraControl:Dynamic = null;
	    
	    for (num in 1...5){
	        if (ClientPrefs.extraKeys >= num && key == Reflect.field(ClientPrefs, 'extraKeyReturn' + num)){
	            if (MusicBeatState.mobilec.newhbox != null)
	                extraControl = Reflect.getProperty(MusicBeatState.mobilec.newhbox, 'buttonExtra' + num);	            
	            else
	                extraControl = Reflect.getProperty(MusicBeatState.mobilec.vpad, 'buttonExtra' + num);
	            if (Reflect.getProperty(extraControl, type))
	                return true;
	        }
	    }	    	    
	    return null;
	}
	#end
```

14. CopyState (optional)

in Main.hx
On This Line
```haxe
	addChild(new FlxGame(game.width, game.height, game.initialState, #if (flixel < "5.0.0") game.zoom, #end game.framerate, game.framerate, game.skipSplash, game.startFullscreen));
```

Replace It With
```haxe
	addChild(new FlxGame(game.width, game.height, #if (mobile && MODS_ALLOWED) CopyState.checkExistingFiles() ? game.initialState : CopyState #else game.initialState #end, #if (flixel < "5.0.0") game.zoom, #end game.framerate, game.framerate, game.skipSplash, game.startFullscreen));
```
