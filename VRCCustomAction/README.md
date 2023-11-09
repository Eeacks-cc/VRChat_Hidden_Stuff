# VRCCustomAction

have you ever notice you have literally same udonsharp sdk as everyone's, but why would vket maps are able to 'open url in browser' that you cant do? secure is hidden here...

check disassembled udonsharp file 'WebPageManager' from vket map, it calls 
```
EXTERN "VRCSDKBaseVRCCustomAction.__Execute__SystemString__SystemVoid
```
and you dont have proper u# compiler to write this code, but look, we can still find funny in game binary and il2cppdumper's dump.cs.

```cs
// Namespace: VRC.SDKBase
public class VRCCustomAction : MonoBehaviour // TypeDefIndex: 23026
{
	// Methods

	// RVA: 0x5B0DCE0 Offset: 0x5B0D0E0 VA: 0x185B0DCE0 Slot: 4
	public virtual void Execute(string parameter) { }

	// RVA: 0x5B0DC50 Offset: 0x5B0D050 VA: 0x185B0DC50 Slot: 5
	public virtual void Execute(int parameter) { }

	// RVA: 0x5B0DBE0 Offset: 0x5B0CFE0 VA: 0x185B0DBE0 Slot: 6
	public virtual void Execute(VRCUrl parameter) { }

	// RVA: 0x64EB80 Offset: 0x64DF80 VA: 0x18064EB80
	public void .ctor() { }
}
```

but how it implemented? 

no clue for right now, but surely i took a look to game binary,

the function 'Execute' in current game binary version is just empty function with Debug.Log(parameter).

so i guess... this function is risky? that they only build code implemention during vket actvity? still a mistery. but i will update here once next time vrchat has any activity.


Note: this shit is 30k$ sdk for 1 year(imagine you sell url opener for 30k$)

