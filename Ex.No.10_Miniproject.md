# Ex.No: 10  Implementation of 3D car game
### DATE:23/03/10                                                                         
### REGISTER NUMBER :212224100043
### AIM: 
To develop a 3D car game in Unity 
### Algorithm:
```
1.Initialize the game environment
2.Create a 3D scene in Unity
Add a plane to represent the road
Add a car object as the player
Add obstacle objects (cubes) on the road
Initialize variables:
speed
turnSpeed
score = 0
gameOver = false
Attach required components
Add Rigidbody and Collider to the car
Add Collider (Is Trigger enabled) to obstacles
Assign tag "Obstacle" to obstacle objects
Start the game loop (Update function)
Check game state
If gameOver = false, perform the following:
Move the car
Move the car forward continuously using speed
Get user input (left/right arrow keys)
Rotate the car based on input
Update score
Increase score with respect to time
Display score (optional)
Collision detection
If the car collides with an obstacle:
Set gameOver = true
Display "Game Over" message
Pause the game
Restart condition
If gameOver = true and user presses ‘R’ key:
Reload the scene
Reset score and variables
Repeat the loop until the game ends
Stop the program
```  
### Program:
## car 
using UnityEngine;

public class CarController: MonoBehaviour
{
    public float speed = 15f;
    public float turnSpeed = 120f;

    private float score = 0;
    private bool isGameOver = false;

    void Update()
    {
        if (!isGameOver)
        {
            // Move forward
            transform.Translate(Vector3.forward * speed * Time.deltaTime);

            // Turn left/right
            float turn = Input.GetAxis("Horizontal") * turnSpeed * Time.deltaTime;
            transform.Rotate(0, turn, 0);

            // Increase score over time
            score += Time.deltaTime * 10;
            Debug.Log("Score: " + (int)score);
        }

        // Restart game
        if (isGameOver && Input.GetKeyDown(KeyCode.R))
        {
            Time.timeScale = 1;
            UnityEngine.SceneManagement.SceneManager.LoadScene(0);
        }
    }

    void OnCollisionEnter(Collision collision)
    {
        if (collision.gameObject.CompareTag("Obstacle"))
        {
            Debug.Log("Game Over!");
            isGameOver = true;
            Time.timeScale = 0;
        }
    }
}```

```
```
using UnityEngine;

public class ObstacleMover : MonoBehaviour
{
    public float speed = 15f;
    public float turnSpeed = 120f;

    private float score = 0;
    private bool isGameOver = false;

    void Update()
    {
        if (!isGameOver)
        {
            transform.Translate(Vector3.forward * speed * Time.deltaTime);

            float turn = Input.GetAxis("Horizontal") * turnSpeed * Time.deltaTime;
            transform.Rotate(0, turn, 0);

            score += Time.deltaTime * 10;
            Debug.Log("Score: " + (int)score);
        }

        if (isGameOver && Input.GetKeyDown(KeyCode.R))
        {
            Time.timeScale = 1;
            UnityEngine.SceneManagement.SceneManager.LoadScene(0);
        }
    }

    void OnTriggerEnter(Collider other)
    {
        if (other.CompareTag("Obstacle"))
        {
            Debug.Log("Game Over!");
            isGameOver = true;
            Time.timeScale = 0;
        }
    }
}
```
```
### Output:
<img width="1918" height="1138" alt="image" src="https://github.com/user-attachments/assets/88ccd054-d68f-482a-be43-93521c351db7" />


### Result:
Thus the game was developed using Unity and adopt AI technology.
