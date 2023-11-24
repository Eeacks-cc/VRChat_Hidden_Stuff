# notice

VRCCustomAction is currently suspended. 

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

# reveal
good luck, we waited for 'Hololive Meet', what is going on?

the VRCustomAction doesnt do shit, i was wrong and got big misunderstanding, the `virtual` keyword literally told its will be use for override, so let see what happen:

child classes
```cs
// Namespace: 
[ÍÌÏÍÌÎÏÎÌÌÏÍÏÎÎÏÍÌÍÎÎÎÏ(3)]
public class ÌÌÏÎÏÎÌÌÎÎÍÏÏÌÎÏÍÎÌÌÍÍÍ : VRCCustomAction // TypeDefIndex: 1628
{
	// Fields
	public string ÌÎÎÏÍÍÎÍÍÌÏÍÍÎÎÌÎÌÎÎÌÎÎ; // 0x20
	public string ÎÌÍÌÎÌÏÎÏÎÍÏÎÏÌÍÎÏÏÌÎÍÌ; // 0x28

	// Methods
	// this is fake only Debug.Log "cant do shit in vive platform blahblah"
	// RVA: 0xDFB3F0 Offset: 0xDFA3F0 VA: 0x180DFB3F0 Slot: 4
	public override void Execute(string ÏÏÎÏÎÏÌÎÏÎÍÌÏÎÎÎÍÎÎÍÏÍÍ) { }

	// RVA: 0xDFB450 Offset: 0xDFA450 VA: 0x180DFB450
	public void .ctor() { }
}

// Namespace: 
[ÍÌÏÍÌÎÏÎÌÌÏÍÏÎÎÏÍÌÍÎÎÎÏ(0)]
public class VRCUrlLauncher : VRCCustomAction // TypeDefIndex: 1629
{
	// Fields
	public VRCUrl[] urls; // 0x20

	// Methods

	// RVA: 0xE0F480 Offset: 0xE0E480 VA: 0x180E0F480 Slot: 6
	public override void Execute(VRCUrl ÎÍÌÏÌÌÍÏÏÎÍÍÌÎÌÍÌÍÌÌÎÍÏ) { }

	// RVA: 0x7F6900 Offset: 0x7F5900 VA: 0x1807F6900
	public void .ctor() { }
	
	// real url launcher
	// RVA: 0xE0F670 Offset: 0xE0E670 VA: 0x180E0F670 Slot: 4
	public override void Execute(string ÌÌÎÏÏÏÏÎÎÍÍÎÏÍÎÌÌÌÏÎÌÌÏ) { }

	// RVA: 0xE0F360 Offset: 0xE0E360 VA: 0x180E0F360 Slot: 5
	public override void Execute(int ÌÍÌÎÌÍÍÍÎÏÏÍÍÎÌÌÌÍÍÍÎÎÏ) { }
}

// Namespace: VRC.SDK.Events
[ÍÌÏÍÌÎÏÎÌÌÏÍÏÎÎÏÍÌÍÎÎÎÏ(4)]
public class VRCRemoteString : VRCCustomAction // TypeDefIndex: 3081
{
	// Fields
	[SerializeField]
	public VRCUrl[] urls; // 0x20
	[SerializeField]
	public UdonBehaviour[] behaviours; // 0x28
	[SerializeField]
	public string[] variables; // 0x30
	private bool ÍÌÌÍÏÌÎÌÍÏÎÏÎÏÎÌÌÎÎÎÍÍÍ; // 0x38
	private const float ÍÍÌÎÍÌÏÏÎÎÍÍÌÌÍÍÏÎÍÌÍÌÏ = 60;

	// Methods

	// RVA: 0x10F7C40 Offset: 0x10F6C40 VA: 0x1810F7C40
	private void ÎÍÍÏÏÎÍÎÎÌÎÌÏÌÍÌÏÍÏÌÏÎÎ() { }

	// RVA: 0x10F7320 Offset: 0x10F6320 VA: 0x1810F7320
	private void ÍÌÌÌÏÌÍÌÍÌÍÎÏÍÍÏÍÎÎÎÌÎÍ() { }

	// RVA: 0x10F7A10 Offset: 0x10F6A10 VA: 0x1810F7A10
	private void ÎÌÌÌÍÎÏÎÍÍÌÎÎÎÏÎÏÏÍÎÌÍÎ() { }

	// RVA: 0x6507D0 Offset: 0x64F7D0 VA: 0x1806507D0
	private void OnDestroy() { }

	// RVA: 0x10F7260 Offset: 0x10F6260 VA: 0x1810F7260
	private void Start() { }

	[IteratorStateMachine(typeof(VRCRemoteString.ÎÌÎÌÎÏÎÏÎÌÌÎÎÎÎÎÍÍÎÌÏÍÎ))]
	// RVA: 0x10F7560 Offset: 0x10F6560 VA: 0x1810F7560
	private IEnumerator ÍÌÍÎÍÎÏÍÎÏÎÏÏÎÏÍÍÏÍÎÌÍÏ(int ÌÍÌÎÌÍÍÍÎÏÏÍÍÎÌÌÌÍÍÍÎÎÏ, string ÎÍÌÏÌÌÍÏÏÎÍÍÌÎÌÍÌÍÌÌÎÍÏ) { }

	// RVA: 0x10F77D0 Offset: 0x10F67D0 VA: 0x1810F77D0
	private void ÍÎÎÌÌÌÌÎÏÏÏÍÌÏÍÌÍÏÌÌÏÎÌ() { }

	// RVA: 0x10F7F10 Offset: 0x10F6F10 VA: 0x1810F7F10
	private void ÏÍÌÎÌÏÎÎÎÎÏÍÌÏÎÏÏÎÌÎÌÎÍ() { }

	// RVA: 0x10F7E70 Offset: 0x10F6E70 VA: 0x1810F7E70
	private IEnumerator ÎÍÏÌÌÍÎÏÌÍÎÌÌÏÎÎÌÏÎÍÎÏÎ(int ÌÍÌÎÌÍÍÍÎÏÏÍÍÎÌÌÌÍÍÍÎÎÏ, string ÎÍÌÏÌÌÍÏÏÎÍÍÌÎÌÍÌÍÌÌÎÍÏ) { }

	// RVA: 0xE41650 Offset: 0xE40650 VA: 0x180E41650
	private void ÏÎÏÌÍÎÏÌÎÌÌÏÏÌÍÍÍÎÌÍÍÏÎ() { }

	// RVA: 0x10F7FD0 Offset: 0x10F6FD0 VA: 0x1810F7FD0
	private void ÏÏÏÏÎÏÍÌÍÏÏÏÏÌÏÌÏÍÏÎÍÏÏ() { }

	// RVA: 0x7F6900 Offset: 0x7F5900 VA: 0x1807F6900
	public void .ctor() { }

	// RVA: 0x10F7600 Offset: 0x10F6600 VA: 0x1810F7600
	public bool ÍÎÍÌÏÏÏÏÎÌÌÌÏÎÏÏÎÏÌÏÎÎÏ() { }
}


// Namespace: VRC.SDK.Experimental
[ÍÌÏÍÌÎÏÎÌÌÏÍÏÎÎÏÍÌÍÎÎÎÏ(4)]
public class VRCImageSaver : VRCCustomAction // TypeDefIndex: 3085
{
	// Fields
	public RenderTexture[] textures; // 0x20
	public bool useAlpha; // 0x28
	private string ÍÍÎÍÏÌÏÏÌÌÏÎÎÍÌÍÌÏÏÎÍÏÌ; // 0x30
	private Regex ÎÌÏÍÏÍÍÍÍÎÍÍÎÎÌÏÏÌÎÏÌÏÍ; // 0x38

	// Methods

	[AsyncStateMachine(typeof(VRCImageSaver.ÏÎÏÏÌÍÎÎÎÎÍÏÎÎÏÌÍÌÏÌÏÏÌ))]
	// RVA: 0x10F6620 Offset: 0x10F5620 VA: 0x1810F6620
	private UniTask<bool> ÌÌÏÎÎÎÎÎÏÏÍÏÌÍÎÌÎÍÍÎÏÌÍ(RenderTexture ÌÎÌÌÏÌÌÏÎÎÌÏÌÏÌÏÎÎÍÌÏÍÍ, Texture2D ÎÌÏÌÎÏÎÍÍÌÎÍÎÎÍÏÍÌÍÌÎÌÎ) { }

	// RVA: 0x10F71B0 Offset: 0x10F61B0 VA: 0x1810F71B0
	public void .ctor() { }

	// RVA: 0x10F6740 Offset: 0x10F5740 VA: 0x1810F6740
	private UniTask<bool> ÍÎÌÎÏÎÏÌÏÎÎÍÌÌÍÍÌÎÎÌÌÌÍ(RenderTexture ÌÎÌÌÏÌÌÏÎÎÌÏÌÏÌÏÎÎÍÌÏÍÍ, Texture2D ÎÌÏÌÎÏÎÍÍÌÎÍÎÎÍÏÍÌÍÌÎÌÎ) { }

	// RVA: 0x10F6ED0 Offset: 0x10F5ED0 VA: 0x1810F6ED0
	private UniTask<bool> ÎÏÍÍÎÎÌÍÎÍÌÏÏÍÍÌÍÍÌÎÌÌÏ(RenderTexture ÌÎÌÌÏÌÌÏÎÎÌÏÌÏÌÏÎÎÍÌÏÍÍ, Texture2D ÎÌÏÌÎÏÎÍÍÌÎÍÎÎÍÏÍÌÍÌÎÌÎ) { }

	// RVA: 0x10F6860 Offset: 0x10F5860 VA: 0x1810F6860
	public bool ÍÎÍÌÏÏÏÏÎÌÌÌÏÎÏÏÎÏÌÏÎÎÏ() { }

	// RVA: 0x10F6FF0 Offset: 0x10F5FF0 VA: 0x1810F6FF0
	public bool ÏÎÌÎÍÌÎÌÍÎÎÏÌÎÎÍÏÎÍÎÍÏÎ() { }

	// RVA: 0x10F64E0 Offset: 0x10F54E0 VA: 0x1810F64E0 Slot: 4
	public override void Execute(string ÏÏÍÎÍÍÌÌÌÎÏÌÏÎÎÏÍÏÎÎÎÎÎ) { }

	// RVA: 0x10F6D10 Offset: 0x10F5D10 VA: 0x1810F6D10
	public bool ÎÌÏÎÎÌÌÎÌÏÍÎÏÍÌÎÌÌÌÏÎÎÎ() { }

	// RVA: 0x10F6B50 Offset: 0x10F5B50 VA: 0x1810F6B50
	public bool ÍÏÎÏÌÎÍÍÎÍÍÍÌÎÍÏÎÌÏÎÏÏÌ() { }

	// RVA: 0x10F6A30 Offset: 0x10F5A30 VA: 0x1810F6A30
	private UniTask<bool> ÍÎÏÎÍÍÎÎÍÍÌÏÏÎÎÎÏÍÌÏÍÌÍ(RenderTexture ÌÎÌÌÏÌÌÏÎÎÌÏÌÏÌÏÎÎÍÌÏÍÍ, Texture2D ÎÌÏÌÎÏÎÍÍÌÎÍÎÎÍÏÍÌÍÌÎÌÎ) { }

	[AsyncStateMachine(typeof(VRCImageSaver.ÍÎÍÌÌÏÏÎÌÍÎÎÏÏÍÌÏÌÍÎÌÍÌ))]
	// RVA: 0x10F6550 Offset: 0x10F5550 VA: 0x1810F6550 Slot: 5
	public override void Execute(int ÌÍÌÎÌÍÍÍÎÏÏÍÍÎÌÌÌÍÍÍÎÎÏ) { }
}

// Namespace: VRC.SDK.Experimental
[ÍÌÏÍÌÎÏÎÌÌÏÍÏÎÎÏÍÌÍÎÎÎÏ(4)]
public class VRCUdonMovieCapture : VRCCustomAction // TypeDefIndex: 3086
{
	// Fields
	public Camera[] Cameras; // 0x20

	// Methods

	// RVA: 0x1114670 Offset: 0x1113670 VA: 0x181114670
	private void ÎÎÍÎÌÍÍÍÍÎÏÍÎÏÏÎÌÌÌÍÏÌÍ() { }

	// RVA: 0x1114BF0 Offset: 0x1113BF0 VA: 0x181114BF0
	public bool ÏÎÏÎÍÏÌÏÍÌÌÏÎÏÏÍÏÏÌÍÌÍÎ() { }

	// RVA: 0x1114850 Offset: 0x1113850 VA: 0x181114850
	public bool ÍÎÍÌÏÏÏÏÎÌÌÌÏÎÏÏÎÏÌÏÎÎÏ() { }

	// RVA: 0x1114670 Offset: 0x1113670 VA: 0x181114670
	private void ÏÏÏÏÎÏÍÌÍÏÏÏÏÌÏÌÏÍÏÎÍÏÏ() { }

	// RVA: 0x1114670 Offset: 0x1113670 VA: 0x181114670
	private void ÏÌÏÏÌÎÌÏÍÏÌÍÎÎÎÌÌÍÌÏÍÏÎ() { }

	// RVA: 0x1114680 Offset: 0x1113680 VA: 0x181114680
	public bool ÌÍÎÎÎÍÏÍÏÌÍÎÏÎÍÍÌÏÎÌÍÎÏ() { }

	// RVA: 0x1114A20 Offset: 0x1113A20 VA: 0x181114A20
	public bool ÎÌÎÍÌÍÌÏÎÍÍÏÌÌÌÌÎÏÌÍÎÍÏ() { }

	// RVA: 0x1114670 Offset: 0x1113670 VA: 0x181114670
	private void Start() { }

	// RVA: 0x11143F0 Offset: 0x11133F0 VA: 0x1811143F0 Slot: 5
	public override void Execute(int ÌÍÌÎÌÍÍÍÎÏÏÍÍÎÌÌÌÍÍÍÎÎÏ) { }

	// RVA: 0x1114670 Offset: 0x1113670 VA: 0x181114670
	private void ÎÎÏÎÎÏÎÍÎÎÌÎÌÌÏÏÌÏÏÍÎÏÌ() { }

	// RVA: 0x7F6900 Offset: 0x7F5900 VA: 0x1807F6900
	public void .ctor() { }
}

// Namespace: VRC.SDK.Internal
[ÍÌÏÍÌÎÏÎÌÌÏÍÏÎÎÏÍÌÍÎÎÎÏ(2)]
public class VRCJokeJamTracker : VRCCustomAction // TypeDefIndex: 3088
{
	// Methods

	// RVA: 0x110E2C0 Offset: 0x110D2C0 VA: 0x18110E2C0
	public bool ÏÎÌÎÍÌÎÌÍÎÎÏÌÎÎÍÏÎÍÎÍÏÎ() { }

	// RVA: 0x7F6900 Offset: 0x7F5900 VA: 0x1807F6900
	public void .ctor() { }

	// RVA: 0x110DC90 Offset: 0x110CC90 VA: 0x18110DC90
	public bool ÌÍÎÎÎÍÏÍÏÌÍÎÏÎÍÍÌÏÎÌÍÎÏ() { }

	// RVA: 0x110E400 Offset: 0x110D400 VA: 0x18110E400
	public bool ÏÎÏÎÍÏÌÏÍÌÌÏÎÏÏÍÏÏÌÍÌÍÎ() { }

	// RVA: 0x110E180 Offset: 0x110D180 VA: 0x18110E180
	public bool ÎÌÏÎÎÌÌÎÌÏÍÎÏÍÌÎÌÌÌÏÎÎÎ() { }

	// RVA: 0x110DDC0 Offset: 0x110CDC0 VA: 0x18110DDC0
	public bool ÍÎÍÌÏÏÏÏÎÌÌÌÏÎÏÏÎÏÌÏÎÎÏ() { }

	// RVA: 0x110DA20 Offset: 0x110CA20 VA: 0x18110DA20 Slot: 5
	public override void Execute(int ÏÏÎÏÎÏÌÎÏÎÍÌÏÎÎÎÍÎÎÍÏÍÍ) { }

	// RVA: 0x110E040 Offset: 0x110D040 VA: 0x18110E040
	public bool ÎÌÎÍÌÍÌÏÎÍÍÏÌÌÌÌÎÏÌÍÎÍÏ() { }

	// RVA: 0x110DF00 Offset: 0x110CF00 VA: 0x18110DF00
	public bool ÍÏÎÏÌÎÍÍÎÍÍÍÌÎÍÏÎÌÏÎÏÏÌ() { }
}


// Namespace: VRC.SDK.Internal
[ÍÌÏÍÌÎÏÎÌÌÏÍÏÎÎÏÍÌÍÎÎÎÏ(1)]
public class VRCUdonAnalytics : VRCCustomAction // TypeDefIndex: 3091
{
	// Fields
	[HideInInspector]
	public string prefix; // 0x20
	[SerializeField]
	private string[] eventNames; // 0x28
	[SerializeField]
	private string[] guids; // 0x30

	// Methods

	// RVA: 0x1113690 Offset: 0x1112690 VA: 0x181113690 Slot: 5
	public override void Execute(int ÌÍÌÎÌÍÍÍÎÏÏÍÍÎÌÌÌÍÍÍÎÎÏ) { }

	// RVA: 0x1114140 Offset: 0x1113140 VA: 0x181114140
	public bool ÏÎÌÎÍÌÎÌÍÎÎÏÌÎÎÍÏÎÍÎÍÏÎ() { }

	// RVA: 0x1113D90 Offset: 0x1112D90 VA: 0x181113D90
	public bool ÍÏÎÏÌÎÍÍÎÍÍÍÌÎÍÏÎÌÏÎÏÏÌ() { }

	// RVA: 0x1113980 Offset: 0x1112980 VA: 0x181113980 Slot: 4
	public override void Execute(string ÏÏÎÏÎÏÌÎÏÎÍÌÏÎÎÎÍÎÎÍÏÍÍ) { }

	// RVA: 0x1113C50 Offset: 0x1112C50 VA: 0x181113C50
	public bool ÍÎÍÌÏÏÏÏÎÌÌÌÏÎÏÏÎÏÌÏÎÎÏ() { }

	// RVA: 0x1113ED0 Offset: 0x1112ED0 VA: 0x181113ED0
	public bool ÎÌÎÍÌÍÌÏÎÍÍÏÌÌÌÌÎÏÌÍÎÍÏ() { }

	// RVA: 0x11138F0 Offset: 0x11128F0 VA: 0x1811138F0 Slot: 6
	public override void Execute(VRCUrl ÏÏÌÌÏÎÌÍÏÏÍÍÍÍÍÍÎÌÌÌÍÍÏ) { }

	// RVA: 0x1114000 Offset: 0x1113000 VA: 0x181114000
	public bool ÎÌÏÎÎÌÌÎÌÏÍÎÏÍÌÎÌÌÌÏÎÎÎ() { }

	// RVA: 0x1113B10 Offset: 0x1112B10 VA: 0x181113B10
	public bool ÌÍÎÎÎÍÏÍÏÌÍÎÏÎÍÍÌÏÎÌÍÎÏ() { }

	// RVA: 0x11143A0 Offset: 0x11133A0 VA: 0x1811143A0
	public void .ctor() { }

	// RVA: 0x1114270 Offset: 0x1113270 VA: 0x181114270
	public bool ÏÎÏÎÍÏÌÏÍÌÌÏÎÏÏÍÏÏÌÍÌÍÎ() { }
}

```

as my comment on function, the `VRCUrlLauncher` is the real launcher for opening url,

i have not checked others overrides with `Execute(string param1)` functions, ye they are sus, but you wanna hear more?

what about this funny class `VRCJokeJamTracker` with `Execute(int param1)` ?? are we drunk? its trying to open an int? WHAT? 

but what we get is, we know they have `VRC.SDK.Experimental` and `VRC.SDK.Internal`, yes, very internal. 

wait, back to topic, what we gonna do? whatif i say, i trying to rebuild sdk to support this feature? isnt it crazy? well ye, but its still hard work.

come on, share to us the 30k$/yr feature.

look at current sdk i have (maybe from ~2022.8 ver), go dnspy and check what is inside of magic sdk

but lets suspend for moment, i will continue later, not reversed + sleepy.

i feel kind of sad here i cant continue to do this since this crap is a big chain,

you need modify at least 4 modules with implemented code, i tried, but the compiler will set your own VRCUrlLauncher as null and udon will halted.

but i still believe there is way to use this, i think maybe... manually edit assembly? but it sounds like bullshit, i will try find out how to use it personally...

Note: this shit is 30k$ sdk for 1 year(imagine you sell url opener for 30k$)

