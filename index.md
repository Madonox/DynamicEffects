# DynamicEffects

## What is DynamicEffects?
DynamicEffects is a Roblox module that allows developers to quickly create environmental effects, such as Bloom, ColorCorrection, etc.  These effects can also be stored in groups, so that you can quickly play an effect set without worrying about disabling other pre-existing effects.

## Data structure
DynamicEffects is an Object-Oriented System.  These classes are main controls, which act as effect "groups".  These groups can store effect sets, or code explaining how to render in an effect.  Each "group" may only display one effect set at a time, but DynamicEffects allows for more than one group to exist.

## Usage
As mentioned before, DynamicEffects is a Roblox module for scripting.  This module can be installed from the toolbox [here](https://www.roblox.com/library/9365160802/DynamicEffects).  Below is the documented usage code.

**Notice: any functions / variables starting with an _ should not be used externally.  Those are internal methods for DynamicEffects.**

### Initializing the module:
In order to initialize the module, you must first require it.  This can be done by placing the module into ReplicatedStorage, requiring it, and calling the `start` function.  Below is an example.
```lua
local DynamicEffects = require(game.ReplicatedStorage.DynamicEffects.DynamicEffects)
DynamicEffects.start()
```
### Creating your first group and adding effects:
In order to begin playing effects, you must create a group.  These groups contain effect sets, which can be played.  You may register as many effects as you wish.
```lua
local effectGroup = DynamicEffects.new() -- This creates the effect group.
effectGroup:RegisterEffect("effect name here",{
	{ -- Each bracket represents one effect instance.
		EffectType = "BloomEffect"; -- Any lighting effects are valid here.
		Properties = { -- Properties of the effect.
			Intensity = 100;
		};
	};
})
```

### Playing your effect:
Playing effects is quite a simple system, where you simply call the `PlayEffect` method.  Please note, an individual group may only have **one** effect playing at a time.  If you try to play a different effect, it will simply disable the old effect.
```lua
effectGroup:PlayEffect("effect name here") -- This will play the effect group defined above.
effectGroup:PlayEffect("some different effect") -- This will stop the effect that is playing above, then play this effect.
```
### Stopping effects:
If you wish to stop an effect without playing another one, you can just call the `StopEffects` method.
```lua
effectGroup:StopEffects()
```
### Removing effects:
If you wish to remove an effect set, you can use the `RemoveEffect` method.
```lua
effectGroup:RemoveEffect("effect name here") -- If this effect is currently running, it will be stopped.
```

### NOTICE:
The methods above work on **both** the server and client, the code below is server-only.

### Sending effect data directly to the player:
If you wish to have a player display an effect from the server, without using an effect group, you can do this:
```lua
local effectData = { -- This is the same data for the effect set above.
	{
	EffectType = "BloomEffect";
	Properties = {
			Intensity = 100;
		};
	};
}
DynamicEffects.SendEffect(player,effectData)
```

#### Stopping the effect:
In order to stop the effect, you can simply use this method:
```lua
DynamicEffects.StopServerEffect(player)
```

### This is all the methods there are for now, please notice this is in a development phase, and changes will be made.
