# MagicLeapTutorial

## Set Up 

[Package Manager](https://creator.magicleap.com/downloads/lumin-sdk/overview)

Within Package Manager

- Lumin SDK
- Magic Leap Unity Package

Lumin SDK 
  - From package manager -> open folder -> Virtual Device -> bin -> UIFrontend -> Magic Leap Remote
  
Unity 

- New Project (Magic Leap Project)
- File -> Build Settings -> Lumin OS && Lumin SDK Location -> (MagicLeap -> mlsdk)
- Magic Leap -> Enable Zero Iteration


## Scripting

```c#

using UnityEngine.XR.MagicLeap;


public class _______ : MonoBehaviour {

	
   public enum ButtonStates { 
	   Normal, 
	   Pressed, 
	   JustReleased
   };
   public ButtonStates BtnState;  


      private void Awake() {
       // Start input
       MLInput.Start();

       // Add button callbacks
       MLInput.OnControllerButtonDown += HandleOnButtonDown;
       MLInput.OnControllerButtonUp += HandleOnButtonUp;

       // Initial State of the Control is Normal
       BtnState = ButtonStates.Normal;
   }

   private void OnDestroy() {
       // Stop input
       MLInput.Stop();

       // Remove button callbacks
       MLInput.OnControllerButtonDown -= HandleOnButtonDown;
       MLInput.OnControllerButtonUp -= HandleOnButtonUp;
   }

   private void Update() {
	   if(BtnState == ButtonStates.Pressed) {
		     //Do Something
	   }
   }
   
   void HandleOnButtonUp(byte controller_id, MLInputControllerButton button) {
       // Callback - Button Up
       if (button == MLInputControllerButton.Bumper) {
           BtnState = ButtonStates.JustReleased;
       }
   }

   void HandleOnButtonDown(byte controller_id, MLInputControllerButton button) {
       // Callback - Button Down
       if (button == MLInputControllerButton.Bumper) {
           BtnState = ButtonStates.Pressed;
       }
   }
}
```
