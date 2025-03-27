# **Rolland De Rennes**

> ESMA - Rennes   
> Student Project - 2023 - 2 months  
> Unity - C#
> Team of 3    
> Gameplay Programmer, UI programmer, System programmer

IMAGE ICONE

## **Context**

During my second year at ESMA, we transitioned from Phaser 3.6 to Unity, a huge change in term of interface and options more than scripting.   
Few months after discovering Unity, we got a group project of 3 (One programmer, One 3D artist and one Game Designer) to make a serious game presenting a part of Western France's heritage.

With my team we decided to make a game around murder case in Rennes, where you play a detective who collect clues in crimes scenes to resolve the mysteries behind crime case.

The game is a point'n'click game on mobile where you can move your phone to inspect the crime scene, the game have one level. 


This project was the first project I did on Unity, I was still learning the Engine and his workflow, a lot of thing are not clean but for a first project I am very proud of it !


## **What I Did**

On the project I was obviously the programmer and did all the work on the different need of the project. 


### **Gameplay Programmer**

The 3C of the game was relatively simple, we just needed a camera who moved with the gyroscope of the mobile and a way to interract with clues in the level.   


**For the interraction**, your programming professor make a plugin to make GameObject touchable on phone directly but before that I used a simple Raycast who check the object it touch to launch a function :

```C# 
//Raycast when touch screen to detect object
            if (Input.touchCount > 0 && Input.touchCount != 2)
            {
                if (!raycastOneTime)
                {
                    Vector3 touchPos = new Vector3(Input.touches[0].position.x, Input.touches[0].position.y, myCamera.farClipPlane);
                    Vector3 touchPosInWorld = myCamera.ScreenToWorldPoint(touchPos);
                    if (!MouseOverUILayerObject.IsPointerOverUIObject())
                    {
                        if (Physics.Raycast(myCamera.transform.position, touchPosInWorld - myCamera.transform.position, out var info, 500, mask))
                        {
                            Proof touchProof = info.transform.GetComponent<Proof>();
                            if (touchProof != null)
                            {
                                touchProof.getPickUp(this);
                            }

                        }
                    }
                }
                raycastOneTime = true;
            }
            else
            {
                raycastOneTime = false;
            }

```



**For the camera**, it was a the start looking difficult but with some reshearh pretty simple:
```C#
transform.rotation = Input.gyro.attitude;
transform.Rotate(0f, 0f, 180f, Space.Self);
transform.Rotate(90f, 180f, 0f, Space.World);
```
Just 3 line of code is needed to get the rotation of the phone and adapt it to Unity coordinate system.  
After that I make so QoL on the camera because she was too much reactive:
```C#
if (cameraMode && Vector3.Distance(Input.gyro.attitude.eulerAngles, lastAcceleromter) > 0.35f)
            {
                transform.rotation = Input.gyro.attitude;
                transform.Rotate(0f, 0f, 180f, Space.Self);
                transform.Rotate(90f, 180f, 0f, Space.World);
                transform.eulerAngles = new Vector3(transform.eulerAngles.x, transform.eulerAngles.y, 0);
            }
            lastAcceleromter = Input.gyro.attitude.eulerAngles;

```
[comment]: <> (METTRE GIF DE MOUVEMENT DE LA CAMERA)



### **UI Programmer**

The game needed a lot of work in UI and it was the first time I make a game with "complex" UI like Inventory, it endend up pretty smoothly and I learned a lot in term of UI in Unity.   
I learned how to make a responsive UI and it was a nightmare at first. 

I made the different canva on different Level to not have multiple canva with a lot of item in the same scene but now I think of it, it was not the best idea because I needed with that to store a lot of information in a GameObject to travel information scene to scene. 


All the different UI I made: 
* An Inspection pannel    

[comment]: <> (METTRE GIF Inspection)


* An Inventory for all the clues    
![MenuUI_RollandDeRennes](https://github.com/AshiyroMisachi/RiallotAlexandre_Portfolio/blob/main/Skills/Assets/Gif/RollandDeRennes_Menu.gif)

* A Quizz section for the end of the level

[comment]: <> (METTRE GIF Quizz)


* And the Main,Level Menu and Score Menu   
![LevelUI_RollandDeRennes](https://github.com/AshiyroMisachi/RiallotAlexandre_Portfolio/blob/main/Skills/Assets/Gif/RollandDeRennes_Level.gif)


### **System Programmer**


In term of system I made a simple **language system** with the number of an enum to get the good text, It demanded to use a list for each text of the game and for UI text, I made a simple script to change the text during runtime:
```C#
public class TraductionWord : MonoBehaviour
{
    public DataHolder dataHolder;


    public string french, english;


    void Start()
    {
        dataHolder = FindObjectOfType<DataHolder>();

        switch (dataHolder.language)
        {
            case Language.Français:
                gameObject.GetComponent<TextMeshProUGUI>().text = french;
                break;
            case Language.English:
                gameObject.GetComponent<TextMeshProUGUI>().text = english;
                break;
        }
    }
}
```

After the end of the project, we learned to make a **save system** on Unity and I decided to test this on this project, It was pretty chaotic but I manage to make it with this:
```C#
public class SaveManager : MonoBehaviour
{
    public SaveState currentSave;
    public DataHolder dataHolder;

    void Start()
    {
        DontDestroyOnLoad(gameObject);
        currentSave = new SaveState();
        dataHolder = FindObjectOfType<DataHolder>();
        Load();
    }
    public void Save()
    {
        var t = JsonUtility.ToJson(currentSave);
        //Save to json file
        string saveFilePath = Application.persistentDataPath + "/Save_RollandDeRennes.txt";
        var Writer = File.CreateText(saveFilePath);
        Writer.Close();
        File.WriteAllText(saveFilePath, t, System.Text.Encoding.UTF8);
    }

    public void SaveOptions()
    {
        currentSave.volume = dataHolder.volume;
        currentSave.son = dataHolder.son;
        currentSave.cameraMode = dataHolder.cameraMode;
        currentSave.difficulty = dataHolder.difficulty;
        currentSave.language = dataHolder.language;

        Save();
    }

    public void SaveLevelScore()
    {
        currentSave.scoreArray = dataHolder.scoreArray;
        currentSave.scoreProofArray = dataHolder.scoreProofArray;
    }

    public void SaveCurrentLevel()
    {
        currentSave.lastLevel = dataHolder.levelName;
        currentSave.levelStarted = dataHolder.levelStarted;
    }

    public void SaveProofInfo()
    {
        currentSave.proofsLevel = dataHolder.proofsLevel;
        currentSave.proofsCount = dataHolder.proofsCount;
    }

    public void SaveNotebookInfo()
    {
        currentSave.actualAnswers = dataHolder.actualAnswers;
        currentSave.numberTry = dataHolder.numberTry;
    }

    public void Load()
    {
        //Load savestate from Json File
        string saveFilePath = Application.persistentDataPath + "/Save_RollandDeRennes.txt";
        if (File.Exists(saveFilePath))
        {
            var Writer = File.OpenText(saveFilePath);
            Writer.Close();
            var t = File.ReadAllText(saveFilePath);
            currentSave = JsonUtility.FromJson<SaveState>(t);

            //Attribute var from saveState
            //Options Value
            dataHolder.volume = currentSave.volume;
            dataHolder.son = currentSave.son;
            dataHolder.cameraMode = currentSave.cameraMode;
            dataHolder.difficulty = currentSave.difficulty;
            dataHolder.language = currentSave.language;

            //Levels
            dataHolder.scoreArray = currentSave.scoreArray;
            dataHolder.scoreProofArray = currentSave.scoreProofArray;

            //Current Level
            dataHolder.levelStarted = currentSave.levelStarted;
            dataHolder.proofsLevel = currentSave.proofsLevel;
            dataHolder.actualAnswers = currentSave.actualAnswers;
            dataHolder.proofsCount = currentSave.proofsCount;
            dataHolder.numberTry = currentSave.numberTry;
        }
    }
}
```
with a basic class to store information, after in the Start function of GameObject, in shearch and apply the save value.


## **What I learned**

Like I said, this was my first project on Unity and in a team, so I learned a lot on the workflow of Unity by testing a lot of thing and make me more confident on Unity after this experience. 

I learned to make game on Mobile with this project who was pretty interresting in game option like feedback or interraction. 

The final product is not very clean in term of script organization but show me the importance of dividing behaviour in different script to make thing clear and easy to find. I think I maybe will redo the game with all the skills and experiende I have now because the game have some probleme now with recent Android Update. 


## **More about the Project**

* [Test the game!](https://maerys.itch.io/rolland-de-rennes)

***
[Get back to the project page](https://github.com/AshiyroMisachi/RiallotAlexandre_Portfolio/blob/main/Projects/Projects.md)    
[Get back to the main page](https://github.com/AshiyroMisachi/RiallotAlexandre_Portfolio)