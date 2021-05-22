# Roll-a-Ball by Yunni Zhu

## Game Changes

### Player Capabilities

1. The player now has the option to **_jump_** during the game

   - In order to jump, simply press the `space` key on the keyboard
   - The more you press the `space` key, the higher you will be able to jump

   ### **Altered Script**

   ### `line 20` in `PlayerController.cs`

   ```
   private float z;
   ```

   ### `line 55` to `line 62` in `PlayerController.cs` at `Update()`

   ```
   if (Keyboard.current.spaceKey.wasPressedThisFrame)
   {
       z = 15f;
   }
   else
   {
       z = 0;
   }
   ```

   ### `line 82` in `PlayerController.cs` at `FixedUpdate()`

   ```
   Vector3 movement = new Vector3(movementX, z, movementY);
   ```

2. The player is now required to collect **_40 blue species_** in order to win the game

   - There are two types of blue species: the cubes and the square
   - All species need to be collected in order to win the game
   - The species rotating in the same manner. This helps the player to distinguish which ones are collectibles

   ### **Altered Script**

   ### `line 47` to `line 50` in `PlayerController.cs` at `SetCountText()`

   ```
   if(count >= 40)
   {
       winTextObject.SetActive(true);
   }
   ```

3. The player can restart the game upon winning or losing
   - Once you collect 40 blue species, the game will prompt ou with the message **_"You Lost!"_**
   - If you fell off the game ground, in other words, if your ball is no longer in the gaming area, the game will prompt you with the message **_"You Win!"_**
   - Under both of the above circumstances, you will have the option to press the `enter` key to restart the game
   ### **Altered Script**
   ### `line 13` in `PlayerController.cs`
   ```
   public GameObject lostTextObject;
   ```
   ### `line 30` in `PlayerController.cs` in `Start()`
   ```
   lostTextObject.SetActive(false);
   ```
   ### `line 63` to `line 77` in `PlayerController.cs` in `Start()`
   ```
   if (rb.velocity.y < -20 && count < 40)
   {
       lostTextObject.SetActive(true);
       if (Keyboard.current.enterKey.wasPressedThisFrame)
       {
        SceneManager.LoadScene(SceneManager.GetActiveScene().name);
       }
   }
   if (count >= 40)
   {
       if (Keyboard.current.enterKey.wasPressedThisFrame)
       {
        SceneManager.LoadScene(SceneManager.GetActiveScene().name);
       }
   }
   ```

### UI Changes

1. A new **_maze_** layout is added to the level
2. **_Slopes_** are added to the maze for players to access the higher pickups
3. A **_separate playground_** is added to the level
   - The player can access it through the yellow slope in the middle of the scene
4. A **_How to Play_** is added to the top left of the screen
5. Some pickups are now placed higher
   - This change was made for players to experience the jumping capabilities
   - The players can only access these pickups by jumping
6. **_Instructions_** for restarting the game are added to the end of the game
