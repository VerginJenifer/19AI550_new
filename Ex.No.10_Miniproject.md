# Ex.No: 10  Implementation of 2D/3D game flipfrogger.
### DATE: 24/10/25                                                                           
### REGISTER NUMBER : 212223240174
### AIM: 
To develop a flipfrogger game in Unity that jumps over an obstracle and collects coins.
### Algorithm:
```

1. Create a new 2D Unity Project

2. Add the Ground
   - Right-click Hierarchy → 2D Object → Sprite → Square → Rename to Ground
   - Scale: X = 8, Y = 1
   - Position: (0, 0, 0)

3. Add the Frog (Player)
   - Right-click Hierarchy → 2D Object → Sprite → Import or draw a Frog image → Rename to Player
   - Position: (-3, 0.5, 0)

4. Add Rigidbody2D to the Player
   - Select Player → Inspector → Add Component → Rigidbody2D
   - Body Type = Dynamic
   - Collision Detection = Continuous
   - Freeze Rotation Z = ON

5. Add Box Collider 2D to the Player
   - Select Player → Inspector → Add Component → Box Collider 2D

6. Add Box Collider 2D to the Ground
   - Select Ground → Inspector → Add Component → Box Collider 2D
   - Ensure "Is Trigger" = OFF

7. Create an Obstacle
   - Right-click Hierarchy → 2D Object → Sprite → Square → Rename to Obstacle
   - Scale: X = 1, Y = 1
   - Position: (0, 0.5, 0)   // Place it on the ground in front of the Frog

8. Add Box Collider 2D to the Obstacle
   - Select Obstacle → Inspector → Add Component → Box Collider 2D
   - Ensure "Is Trigger" = OFF

9. Set the Ground Layer
   - Click the Layer dropdown at the top of the Inspector
   - Add a new Layer named "Ground"
   - Assign the "Ground" layer to both Ground and Obstacle

10. Create the Player Controller Script
    - In Project Window → Right-click → Create → C# Script → Name it "PlayerController"

11. Open PlayerController.cs and replace all code with
12. Save the Script and return to Unity

13. Attach the Script to the Player
    - Drag "PlayerController" onto the Player object in the Hierarchy

14. Add Coins
    - Right-click Hierarchy → 2D Object → Sprite → Circle (or import Coin sprite)
    - Rename to Coin
    - Scale: (0.5, 0.5, 1)
    - Position some Coins above the obstacle
    - Duplicate to make more coins

15. Add Collider to Coins
    - Select a Coin → Inspector → Add Component → Circle Collider 2D
    - Check "Is Trigger" = ON

16. Create the Coin Collector Script
    - In Project Window → Right-click → Create → C# Script → Name it "CoinCollect"

17. Open CoinCollect.cs and replace all code with:

    using UnityEngine;

    public class CoinCollect : MonoBehaviour
    {
        void OnTriggerEnter2D(Collider2D other)
        {
            if (other.CompareTag("Player"))
            {
                Destroy(gameObject);
                Debug.Log("Coin collected!");
            }
        }
    }

18. Save the Script and return to Unity

19. Attach CoinCollect Script
    - Select all Coins in Hierarchy → Drag "CoinCollect" onto them

20. Tag the Player
    - Select Player → Inspector → Tag → Add Tag...
    - Create a new tag named "Player"
    - Assign the "Player" tag to the Player object

21. Test the Game
    - Press Play ▶
    - Move the Frog left/right using A/D or arrow keys
    - Press Spacebar or ↑ to jump
    - Jump over the Obstacle and collect Coins

22. Result
    - The Frog moves and jumps only when on the ground or obstacle
    - The Frog can jump over the obstacle
    - Coins disappear when collected
    - “Coin collected!” message appears in Console

```  
### Program:
PlayerController.cs
```
using UnityEngine;

    public class PlayerController : MonoBehaviour
    {
        public float moveSpeed = 5f;
        public float jumpForce = 8f;
        private Rigidbody2D rb;
        private bool isGrounded = true;

        void Start()
        {
            rb = GetComponent<Rigidbody2D>();
        }

        void Update()
        {
            // Move left and right
            float move = Input.GetAxis("Horizontal");
            rb.velocity = new Vector2(move * moveSpeed, rb.velocity.y);

            // Jump when grounded
            if (isGrounded && (Input.GetKeyDown(KeyCode.Space) || Input.GetKeyDown(KeyCode.UpArrow)))
            {
                rb.velocity = new Vector2(rb.velocity.x, jumpForce);
                isGrounded = false;
            }
        }

        void OnCollisionEnter2D(Collision2D collision)
        {
            // Ground and obstacle are both considered ground for jumping
            if (collision.gameObject.layer == LayerMask.NameToLayer("Ground"))
            {
                isGrounded = true;
            }
        }
    }
```
CoinCollector.cs:
```
  using UnityEngine;

    public class CoinCollect : MonoBehaviour
    {
        void OnTriggerEnter2D(Collider2D other)
        {
            if (other.CompareTag("Player"))
            {
                Destroy(gameObject);
                Debug.Log("Coin collected!");
            }
        }
    }
```
### Output:
<img width="1919" height="1022" alt="image" src="https://github.com/user-attachments/assets/4edc56a8-8439-404c-863b-8c50267d81e0" />
<img width="1915" height="1012" alt="image" src="https://github.com/user-attachments/assets/8dc2ffb2-5a59-474f-bc11-0fa529038da5" />
<img width="1919" height="1020" alt="image" src="https://github.com/user-attachments/assets/90551dad-668b-43b2-bde7-829dade92c61" />


### Result:
Thus, the Frog Jump game was developed using Unity and adopted Artificial Intelligence-based collision and movement control technology.
