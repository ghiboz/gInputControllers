# gInputControllers

![](https://github.com/ghiboz/gInputControllers/blob/master/img/large.png?raw=true)

Welcome in the docs/help repository for the [gInputControllers](https://www) asset for Unity3D.

## What is?
gInputControllers _(GIC)_ basically is a plugin _(windows dll, 32 and 64 bit)_ that manages all the input controllers _(like steering wheels, joysticks, handbrakes, gamepad, etc...)_ attached on your pc.

## What does?
**GIC** let to use all the inputs from the controllers into your game, you can read the analogic and digital values in the `Update()` function or registering to the `ButtonUp` and `ButtonDown` and `AxisMoved`.
You are able to manage the force feedback _(if present)_.

## What does not?
**GIC** is not an asset that contains prefabs or similar to put directly in your game, it's simply _under the hood_.

# Installation.
Adding the package to your Unity3D project **GIC** is being installed, the package contains also a scene that simply let you to detect all your controllers and the relatives buttons and analogic axis and force feedback.

# Usage.
Use **GIC** is extremely simple: in the package there's the `GIC.cs` class that manage the dll calls, is not necessary modify or understand it.
The `GIC_Loader.cs` class contains an example on how initalize **GIC** and detect the controllers attached and, for each controller, the number of the analogic axis, the digital buttons and the force feedback.

### Initialization.
```CSharp
if (GIC.Init(ProjectName))
{
    Debug.Log("gInputControllers initalized!");
    Debug.Log(string.Format("num controllers: {0}", GIC.NumControllers));
}
else
{
    Debug.LogError("error during the init of gInputControllers");
}
```
This piece of code initialize **GIC**.

### Updating.
```CSharp
GIC.Update();
```
This piece of code update all the controllers, it update the list `GIC.Controllers` that contains a list of the controllers, containing the info of the controller
```CSharp
public string Name;
public int NumAxis;
public int NumButtons;
public bool HasForceFeedback;
```
and a list of the Axis _(Analogic)_ and Buttons _(Digital)_ elements, so if I want read the value of the 2nd axis of the first controller, I just need to do this:
```CSharp
var value = GIC.Controllers[0].Axis[1];
```


## Value scale.
* the `Buttons` elements has the value of **0** if is not pressed and **1** if is pressed;
* the `Axis` elements has the value between **-32768 and 32767**;
* the `ForceFeedback` elements accept a value between **-10000 and 10000**;

