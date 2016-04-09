#AndroidUtilities
This library contains various utilities for use in Android development. The library is split into two packages: helpers and collections. The helpers package contains simple classes with useful static methods. The collections package only contains one class currently. To use this library, add `compile 'com.matthew-tamlin:android-utilities-library:1.3.1'` to your build.gradle file. Older versions are available in the [maven repo](https://bintray.com/matthewtamlin/maven/AndroidUtilities/view).

## Helper classes
The helpers package contains several simple classes. The classes cannot be instantiated, instead they provide functionality by means of static methods. The following helpers are available for use:
- `AudioFocusHelper`: Contains methods for obtaining and abandoning audio focus without boilerplate code.
- `BitmapHelper`: Contains methods for efficiently decoding and storing bitmap images in memory.
- `ColorHelper`: Contains methods for blending colors and retreiving the colors of the current theme.
- `DimensionHelper`: Contains methods for converting complex dimensions (e.g. dp, in) to pixels without boilerplate code.
- `PermissionHelper`: Contains methods for requesting permissions without boilderplate code (for SDK >= 23). 
- `ScreenSizeHelper`: Contains methods for querying information about the device screen size.
- `StatusBarHelper`: Contains methods for showing and hiding the status bar. Functionality varies depending on SDK version.

## Collections
There is currently only one class in the collections package: `ArrayListWithCallbacks`. This class extends `ArrayList` and functions exactly the same, but with one difference. Whenever the collection is modified in any way (add, set, remove etc.) then the collection delivers callback events to registered listeners. Each callback contains information about which collection was modified and the nature of the modification. This means that a collection can be modified anywhere in code, and other components can be automatically notified of the change. 

Consider a scenario where an `ArrayList` of names is displayed to the user with a `RecyclerView`. The adapter which takes the names and displays them in the UI must be notified whenever the list is changed, which requires additional boilerplate code. This approach can cause problems and may lead to difficult to find bugs on two accounts: It is easy to forget to notify the adapter when coding, and the UI thread may not always be visible to the modifying component. By using an `ArrayListWithCallbacks`, it is impossible to forget to notify the adapter since the action of modifying the collection automatically triggers the notification. The activity which manages the adapter simply has to register to receive callbacks, and then use the UI thread to notify the adapter.

