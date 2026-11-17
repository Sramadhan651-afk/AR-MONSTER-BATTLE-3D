# AR Monster Battle 3D — Unity starter

Starter project source for an Android AR monster-battle prototype.
The monsters and names should be original creations; do not use Pokémon logos,
models, sounds, names, or other protected assets without permission.

## Recommended setup

- Unity 6 (3D URP project)
- AR Foundation package
- Google ARCore XR Plugin
- TextMeshPro (import TMP Essentials when prompted)
- Android Build Support, Android SDK & NDK Tools, and OpenJDK

Package versions change over time. In Unity Package Manager, install compatible
versions of AR Foundation and ARCore XR Plugin recommended for your Unity editor.

## 1. Create the Unity project

1. Open Unity Hub and create a **3D (URP)** project.
2. Open **Window > Package Manager**.
3. Install **AR Foundation** and **Google ARCore XR Plugin**.
4. In **Edit > Project Settings > XR Plug-in Management**, install XR Plug-in
   Management if prompted, select the Android tab, and enable **ARCore**.
5. Set the platform to Android in **File > Build Profiles** (or Build Settings
   in older Unity versions).

## 2. Build the AR scene

1. Create a new scene named `ARBattle`.
2. Remove the default Main Camera.
3. Add **XR > AR Session**.
4. Add **XR > XR Origin (Mobile AR)**. Depending on the AR Foundation version,
   the menu wording may differ.
5. Select the XR Origin object. Ensure it has:
   - AR Plane Manager
   - AR Raycast Manager
   - AR Camera Manager on its child AR Camera
   - AR Camera Background on its child AR Camera
6. Set AR Plane Manager's Detection Mode to Horizontal.
7. (Optional) Assign an AR Plane prefab to visualize detected planes.
8. Add an empty GameObject named `GameController` and attach
   `ARBattleController.cs`.

## 3. Make temporary monster prefabs

For the first test, simple primitives are enough:

1. Create a Capsule or a small combination of spheres/capsules.
2. Give it a distinct material and a recognizable silhouette.
3. Drag it from the Hierarchy into `Assets/Prefabs` to create a prefab.
4. Make a second, different monster prefab.
5. Assign both prefabs to the `Player Monster Prefab` and
   `Enemy Monster Prefab` fields on GameController.

Replace these placeholders later with original rigged 3D models (FBX) and
Animator Controllers. Keep model scale appropriate; start around 0.3–0.6 m tall.

## 4. Connect the script

On `GameController`:
- Drag XR Origin's **AR Raycast Manager** into `Raycast Manager`.
- Drag the child **AR Camera** into `Ar Camera`.
- Assign both monster prefabs.
- Set Monster Spacing to about `0.9`.

Create a Canvas (Screen Space - Overlay) with:
- TMP text for status
- TMP text for player HP
- TMP text for enemy HP
- Button named SERANG
- Button named BERTAHAN
- Button named ULANGI

Drag the three TMP text objects into the matching script fields.
For each button's **On Click()**:
- SERANG -> GameController -> `ARBattleController.Attack()`
- BERTAHAN -> GameController -> `ARBattleController.Defend()`
- ULANGI -> GameController -> `ARBattleController.ResetBattle()`

Place the UI near the bottom of the screen and make buttons large enough for touch.

## 5. Android settings

- Player Settings > Other Settings > Scripting Backend: IL2CPP (recommended).
- Target Architectures: ARM64.
- Minimum API Level: use the minimum supported by your selected Unity/ARCore
  package versions.
- Set a unique package identifier, e.g. `com.yourstudio.armonsterbattle`.
- Add `ARBattle` to the build scene list.
- Use a real compatible ARCore phone for testing; AR camera features generally
  do not work in the ordinary Unity Editor Game view.

## 6. Test flow

1. Install the APK on the Android phone.
2. Grant camera permission.
3. Move the phone slowly toward a well-lit, textured floor or table.
4. Wait for a horizontal surface to be detected.
5. Tap the detected surface to place the two monsters.
6. Try SERANG and BERTAHAN. ULANGI removes the monsters and lets you place them again.

## Current prototype limitations

- This is a starter source package, not a finished APK.
- It uses simple prefab models; it does not include finished monster art,
  sound, capture mechanics, online multiplayer, or saving.
- Battle is a simple turn-based loop. Damage values are placeholders.
- The AR placement uses a plane hit and does not yet attach monsters to a
  persistent AR anchor. Tracking can shift if AR tracking is poor.
- Verify ARCore device support on the exact phone model and Android build
  before relying on AR features.
