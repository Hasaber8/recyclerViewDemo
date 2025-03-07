# RecyclerView Sample Application

This project demonstrates how to implement a RecyclerView in Android with modern Material Design principles. It showcases various RecyclerView features including item addition, deletion with swipe gestures, and state persistence.

## Project Structure

### Core Components

1. **MainActivity.java**
   - Entry point of the application
   - Manages the RecyclerView and its data
   - Handles user interactions (adding items, swipe-to-delete)
   - Implements state saving/restoration for orientation changes

2. **ItemCard.java**
   - Model class that represents each item in the RecyclerView
   - Contains properties: image source, item name, description, and checked status
   - Handles state changes when an item is clicked or checked

3. **RviewAdapter.java**
   - Adapter that connects the data (ItemCard objects) to the RecyclerView
   - Creates and binds ViewHolders
   - Manages the list of items to display

4. **RviewHolder.java**
   - ViewHolder pattern implementation for RecyclerView
   - Caches references to the views inside each item layout
   - Improves scrolling performance

5. **ItemClickListener.java**
   - Interface for handling click events on RecyclerView items
   - Provides methods for item clicks and checkbox clicks

### Layout Files

1. **activity_main.xml**
   - Main layout using CoordinatorLayout for proper Material Design behavior
   - Contains a MaterialToolbar, RecyclerView, and FloatingActionButton
   - Uses app:layout_behavior to coordinate scrolling behavior

2. **item_card.xml**
   - Layout for each individual item in the RecyclerView
   - Uses MaterialCardView with ConstraintLayout for optimal positioning
   - Contains ImageView, TextViews for name and description, and a MaterialCheckBox

### Resource Files

1. **colors.xml**
   - Defines the color scheme for the application
   - Includes primary, accent, and supporting colors
   - Provides consistent color references throughout the app

2. **styles.xml**
   - Defines the app theme using Material Components
   - Contains custom styles for text appearances and card views
   - Uses NoActionBar theme to support custom toolbar

## Key Features Implementation

### RecyclerView Setup

```java
private void createRecyclerView() {
    rLayoutManger = new LinearLayoutManager(this);
    recyclerView = findViewById(R.id.recycler_view);
    recyclerView.setHasFixedSize(true);
    rviewAdapter = new RviewAdapter(itemList);
    // ... set click listeners
    recyclerView.setAdapter(rviewAdapter);
    recyclerView.setLayoutManager(rLayoutManger);
}
```

### Swipe-to-Delete with Visual Feedback

```java
private void setupSwipeToDelete() {
    ItemTouchHelper itemTouchHelper = new ItemTouchHelper(new ItemTouchHelper.SimpleCallback(0, 
            ItemTouchHelper.LEFT | ItemTouchHelper.RIGHT) {
        private final ColorDrawable background = new ColorDrawable(Color.parseColor("#FF5252"));
        
        @Override
        public boolean onMove(RecyclerView recyclerView, RecyclerView.ViewHolder viewHolder, 
                             @NonNull RecyclerView.ViewHolder target) {
            return false;
        }

        @Override
        public void onSwiped(RecyclerView.ViewHolder viewHolder, int direction) {
            // Remove item and show Snackbar with UNDO option
            // ...
        }
        
        @Override
        public void onChildDraw(@NonNull Canvas c, @NonNull RecyclerView recyclerView, 
                               @NonNull RecyclerView.ViewHolder viewHolder, float dX, float dY, 
                               int actionState, boolean isCurrentlyActive) {
            // Draw background color during swipe
            // ...
        }
    });
    itemTouchHelper.attachToRecyclerView(recyclerView);
}
```

### Adding New Items

```java
private void addItem(int position) {
    // Create a new ItemCard with random description
    // Add to the list and notify adapter
    // Show confirmation Snackbar
}
```

### State Persistence

The app saves and restores the state of all items when configuration changes occur (like screen rotation):

```java
@Override
protected void onSaveInstanceState(@NonNull Bundle outState) {
    // Save number of items and their properties
    // ...
    super.onSaveInstanceState(outState);
}

private void initialItemData(Bundle savedInstanceState) {
    // Restore items from savedInstanceState if available
    // Otherwise load default items
    // ...
}
```

## Material Design Implementation

The app uses Material Design components and principles:

1. **MaterialToolbar**: Provides a consistent navigation experience
2. **MaterialCardView**: Displays content with proper elevation and corner radius
3. **FloatingActionButton**: Offers a prominent action (adding items)
4. **Snackbar**: Provides feedback for user actions with options to undo
5. **MaterialCheckBox**: Follows Material Design guidelines for selection controls

## Building and Running the Project

This project uses Gradle 8.2 and Android Gradle Plugin 8.2.2. It targets Android API level 34 (Android 14) with a minimum SDK of 23 (Android 6.0 Marshmallow).

To build and run the project:

1. Clone the repository
2. Open in Android Studio
3. Sync Gradle files
4. Run on an emulator or physical device

## Extending the Application

You can extend this sample in several ways:

1. Add item editing functionality
2. Implement different RecyclerView layouts (GridLayoutManager, StaggeredGridLayoutManager)
3. Add item animations for more visual feedback
4. Implement filtering and sorting of items
5. Connect to a backend service to persist data
