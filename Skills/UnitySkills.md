 # **My Skills on Unity**

 I have started Unity in 2023, it was my first 3D engine and use it a lot during my scholarship.   
 I used Unity for differents kind of projects or prototypes so I am used to 2D and 3D games and worked on PC and Android games. 

I really like Unity for his simplicity when I am doing Gamejam or little project but love to explore and learn all his complex aspect !

## **Scripting in general**

During my scholarship at ESMA I learned all the basic thing of Unity scripting and how to use them correctly.

I know how to use **heritage** and **delagate** on Unity to simplify addition to my project.   
I know how to use **data assets** to easely make variation of the same GameObject with scriting to not accumulate Prefab.   

***
## **Gameplay Programming**

Gameplay programming is my prefered type of programmation on Unity. In my different project and prototype I learned how to make different type of camera for my game like First and Third person and adjust them with what the game need.

**First person code exemple:**
```C#
public class S_PlayerCamera : MonoBehaviour
{
    //Rotation speed of the Camera
    [SerializeField]
    private float mouseSensivity = 100f;

    //Reference of the Player Transform
    [SerializeField]
    private Transform playerBody;

    //Current xRotation of the Camera
    private float xRotation;

    void Start()
    {
        //Lock the cursor at the start of the game
        S_CameraFunction.LockCursor();
    }

    void Update()
    {
        //Block the camera if not in exploration
        if (S_ManagerManager.GetManager<S_PlayerManager>().GetPlayerState() != PlayerState.Exploration)
        {
            return;
        }
        //Move the Camera each frame
        MoveCameraView();
    }

    private void MoveCameraView()
    {
        //Get Axis value of the Cursor      Multiplied with Sensitivity   And deltaTime to work with all frameRate
        float mouseX = Input.GetAxis("Mouse X") * mouseSensivity * Time.deltaTime;
        float mouseY = Input.GetAxis("Mouse Y") * mouseSensivity * Time.deltaTime;

        //Stock xRotation modified by Y axis of the mouse
        xRotation -= mouseY;
        //Clamp make xRotation didn't exceed certain value
        xRotation = Mathf.Clamp(xRotation, -90, 90);

        //xRotation is for the PlayerCamera only
        transform.localEulerAngles = new Vector3(xRotation, 0f, 0f);

        //Rotate the player based on X axis of the mouse
        playerBody.Rotate(Vector3.up * mouseX);
    }
}
```    

**Third person camera exemple:**
```C#
public class S_PlayerCamera : MonoBehaviour
{

    [Header("References")]

    public Transform orientation;
    public Transform player;
    public Transform playerObj;
    public CharacterController characterController;

    public float rotationSpeed;


    void Start()
    {
        Cursor.lockState = CursorLockMode.Locked;
        Cursor.visible = false;
    }


    void Update()
    {
        if (player.GetComponent<S_PlayerMovement2>().playerInMenu)
        {
            return;
        }

        //rotate orientation
        Vector3 viewDr = player.position - new Vector3(transform.position.x, player.position.y, transform.position.z);
        orientation.forward = viewDr;

        //rotate player object 
        float horizontalInput = Input.GetAxis("Horizontal");
        float verticalInput = Input.GetAxis("Vertical");
        Vector3 inputDir = orientation.forward * verticalInput + orientation.right * horizontalInput;

        if (inputDir != Vector3.zero) {
            playerObj.forward = Vector3.Slerp(playerObj.forward, inputDir.normalized, Time.deltaTime + rotationSpeed);
        }
        
    }
}
```

***

## UI **Programming**

I familiar with the UI system of Unity. I can make responsive UI adapted for different screen size.  
I did a lot of menu and HUD and I know how add theses at the gameplay part.


**Example of UI I made for main menu and level selection for my project Rolland De Rennes**   
![LevelUI_RollandDeRennes](https://github.com/AshiyroMisachi/RiallotAlexandre_Portfolio/blob/main/Skills/Assets/Gif/RollandDeRennes_Level.gif)


**Example of In game HUD and menu I made for the same project**   
![InGameUI_RollandDeRennes](https://github.com/AshiyroMisachi/RiallotAlexandre_Portfolio/blob/main/Skills/Assets/Gif/RollandDeRennes_InGame.gif) 
![MenuUI_RollandDeRennes](https://github.com/AshiyroMisachi/RiallotAlexandre_Portfolio/blob/main/Skills/Assets/Gif/RollandDeRennes_Menu.gif)
***

## **Animator**

I use the animator generally to add some little animation to my game on gameplay or UI, I know how to settup basic animator. I know how to integrate animation to a project with C#.   


[comment]: <> (METTRE SCRIPT DANS ANIMATOR + GIF RESULTAT D'UN TRUC)



***

[Get back to the skills page](https://github.com/AshiyroMisachi/RiallotAlexandre_Portfolio/blob/main/Skills/Skills.md)  
[Get back to the main page](https://github.com/AshiyroMisachi/RiallotAlexandre_Portfolio)