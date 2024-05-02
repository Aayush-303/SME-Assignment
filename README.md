# SME-Assignment

In file **`PlayerController.h`**

In line 20, the potential bug lies in the use of the **`PlayerView* player_view`** and **`PlayerModel* player_model`** pointers.

In line 20, we declare two pointers: **`PlayerView* player_view`** and **`PlayerModel* player_model`**. These pointers are intended to point to instances of the **`PlayerView`** and **`PlayerModel`** classes, respectively. However, at this point, these pointers are uninitialized, meaning they do not yet point to valid memory locations.

The issue arises from the fact that these pointers are declared but not initialized in the constructor **`PlayerController()`**. If these pointers are used before they are properly initialized to point to valid **`PlayerView`** and **`PlayerModel`** objects, it can lead to undefined behavior, such as crashes or accessing invalid memory.

To fix this bug, you need to ensure that these pointers are properly initialized before they are used. This could involve initializing them in the constructor using **`new`** and deallocating the memory using **`delete`** in the destructor, or better yet, using smart pointers like **`std::unique_ptr`** or **`std::shared_ptr`** to manage the memory automatically.

namespace Player
{
class PlayerController : public Collision::ICollider
{
private:
std::unique_ptr<PlayerView> player_view;
std::unique_ptr<PlayerModel> player_model;

then in the file PlayerController.cpp

PlayerController::PlayerController()
: player_view(std::make_unique<PlayerView>()),
player_model(std::make_unique<PlayerModel>())

And in the destructor **`~PlayerController()`**, there's no need to manually deallocate memory, as the smart pointers will handle that automatically when they go out of scope.
