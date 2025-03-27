# **L'Oiseau Blanc**

> ESMA - Rennes   
> Student Project - 2024 - 3 months  
> Unity - C#
> Team of 5    
> Gameplay Programmer, Puzzle programmer, Game Designer   


![OiseauBlanc_Icon](![RdR_Icon](https://github.com/AshiyroMisachi/RiallotAlexandre_Portfolio/blob/main/Projects/Rolland%20de%20Rennes/Assets/RollandDeRennes_Icon.png))


## **Context**

During my second year of my scholarship at ESMA, we got asked to do a **escape room game** on **Unity** in team of 5, it was the second project we did in team. 

In this project we was **2 programmer** and **3 artist** and we was all game designer and everyone did one puzzle. 

With my team we decided to place the game in a toys museum in a manor where the character you play come do some urbex, but the manor was not abandoned and your character get trap and got asked to resolve some puzzle to escape before the police catch him.

The game demands you to resolve 5 enigmas with different toys before a final challenge in 15 minutes. 


## **What I Did**



### **Gameplay Programmer**

In this project we was 2 programmer and I got the mission to do the **3C** who was in this project, **Camera and Movement**, **Interraction** with puzzle.   

**First person camera I did:**
```C#
public class S_PlayerCamera : MonoBehaviour
{
    [SerializeField]
    private float mouseSensivity = 100f;

    [SerializeField]
    private Transform playerBody;

    private float xRotation;

    void Start()
    {
        S_CameraFunction.LockCursor();
    }

    void Update()
    {
        //Block the camera if not in exploration
        if (S_ManagerManager.GetManager<S_PlayerManager>().GetPlayerState() != PlayerState.Exploration)
        {
            return;
        }
        MoveCameraView();
    }

    private void MoveCameraView()
    {
        float mouseX = Input.GetAxis("Mouse X") * mouseSensivity * Time.deltaTime;
        float mouseY = Input.GetAxis("Mouse Y") * mouseSensivity * Time.deltaTime;

        xRotation -= mouseY;
        xRotation = Mathf.Clamp(xRotation, -90, 90);

        transform.localEulerAngles = new Vector3(xRotation, 0f, 0f);

        playerBody.Rotate(Vector3.up * mouseX);
    }
}
```


**Player Movement I did:**
```c#
[RequireComponent(typeof(CharacterController))]
public class S_PlayerMovement : MonoBehaviour
{
    [Header("Movement")]
    [SerializeField]
    private float speed = 12f;

    private CharacterController controller;

    [Header("Gravity")]
    private Vector3 velocity;

    [SerializeField]
    private float gravity = -9.81f;


    [Header("GroundCheck")]
    [SerializeField]
    private Transform groundCheck;

    [SerializeField]
    private float groundDistance = 0.04f;

    [SerializeField]
    private LayerMask groundMask;

    private bool isGrounded;

    void Start()
    {
        //Get Reference
        controller = GetComponent<CharacterController>();
    }

    void Update()
    {
        if (S_ManagerManager.GetManager<S_PlayerManager>().GetPlayerState() != PlayerState.Exploration)
        {
            return;
        }
        IsGrounded();
        Movement();
        PlayerGravity();
    }

    private void Movement()
    {
        //Stock Axis value
        float x = Input.GetAxis("Horizontal");
        float z = Input.GetAxis("Vertical");

        Vector3 move = transform.right * x + transform.forward * z;

        controller.Move(move * speed * Time.deltaTime);
    }

    private void PlayerGravity()
    {
        velocity.y += gravity * Time.deltaTime;
        controller.Move(velocity * Time.deltaTime);
    }

    private void IsGrounded()
    {
        isGrounded = Physics.CheckSphere(groundCheck.position, groundDistance, groundMask);

        //If the player touch the ground, reset the gravity velocity
        if (isGrounded && velocity.y < 0)
        {
            velocity.y = -2f;
        }
    }
}
```

### **Puzzle Programmer**

I made three puzzle on the project:  
* A little quest to find the love of a puppet    

[comment]: <> (METTRE GIF ET CODE PUZZLE PUPPET)

* A big simons says 

[comment]: <> (METTRE GIF ET CODE PUZZLE SIMON)

* A basket ball items collection who needed some reordering

[comment]: <> (METTRE GIF ET CODE PUZZLE Basket)


## **What I learned**

It was the first time I did a project other than Jam with another programmer, so, I learned to **divide task** depending on affinity and skills, and learn to make **understandable scripts and documentation** for my team. 

It was also the firt time I work with multiple 3D artist and learned the **workflow of communication and integration** with them to work quickly without conflicts in assets demand. 

This was my second big project on Unity and improved my overall skills on the Engine.


## **More about the Project**

* [Test the game!](https://github.com/AshiyroMisachi/PEZ-GroupeG-LOiseauBlanc)

***
  


[Get back to the project page](https://github.com/AshiyroMisachi/RiallotAlexandre_Portfolio/blob/main/Projects/Projects.md)    
[Get back to the main page](https://github.com/AshiyroMisachi/RiallotAlexandre_Portfolio)