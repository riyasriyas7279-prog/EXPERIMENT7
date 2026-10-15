# Experiment: Create an Adaptive UI Using ListView and ImageView

## Aim

To develop an adaptive user interface in an Android application using `ListView` and `ImageView` with Kotlin in Android Studio.

## Software Requirements

- Android Studio
- Kotlin programming language
- Android SDK
- Android Emulator or Android mobile device

## Theory

### ListView

`ListView` is an Android UI component used to display a scrollable list of items. It uses an adapter to connect data to individual list rows.

### ImageView

`ImageView` is an Android UI component used to display images from drawable resources or other image sources.

### Adaptive User Interface

An adaptive user interface adjusts its layout and appearance to suit different screen sizes and orientations. Using responsive layouts, appropriate image scaling, and flexible dimensions helps the application work across different Android devices.

## Procedure

1. Open Android Studio and create a new Kotlin project.
2. Create the main activity layout using XML.
3. Add a `ListView` to display a list of items.
4. Create a custom row layout containing an `ImageView` and a `TextView`.
5. Add sample images to the `res/drawable` folder.
6. Create a custom adapter to display images and text in the list.
7. Use flexible layout dimensions and appropriate image scaling to support different screen sizes.
8. Run the application on an emulator or Android device.
9. Verify that the list scrolls correctly and images are displayed properly.

## Implementation

### 1. MainActivity.kt

```kotlin
package com.example.adaptiveui

import android.app.Activity
import android.os.Bundle
import android.widget.ListView
import android.widget.SimpleAdapter

class MainActivity : Activity() {

    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)
        setContentView(R.layout.activity_main)

        val listView = findViewById<ListView>(R.id.listView)

        val names = arrayOf(
            "Android",
            "Kotlin",
            "Java",
            "Python",
            "Flutter"
        )

        val images = intArrayOf(
            R.drawable.android,
            R.drawable.kotlin,
            R.drawable.java,
            R.drawable.python,
            R.drawable.flutter
        )

        val items = ArrayList<HashMap<String, Any>>()

        for (i in names.indices) {
            val item = HashMap<String, Any>()
            item["name"] = names[i]
            item["image"] = images[i]
            items.add(item)
        }

        val adapter = SimpleAdapter(
            this,
            items,
            R.layout.list_item,
            arrayOf("name", "image"),
            intArrayOf(R.id.itemName, R.id.itemImage)
        ).apply {
            setViewBinder { view, data, _ ->
                if (view is android.widget.ImageView &&
                    data is Int
                ) {
                    view.setImageResource(data)
                    true
                } else {
                    false
                }
            }
        }

        listView.adapter = adapter
    }
}
```

### 2. activity_main.xml

Create this file in `res/layout/activity_main.xml`.

```xml
<?xml version="1.0" encoding="utf-8"?>
<LinearLayout
    xmlns:android="http://schemas.android.com/apk/res/android"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:orientation="vertical"
    android:padding="12dp">

    <TextView
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:text="Adaptive UI - ListView and ImageView"
        android:textSize="22sp"
        android:textStyle="bold"
        android:padding="12dp" />

    <ListView
        android:id="@+id/listView"
        android:layout_width="match_parent"
        android:layout_height="0dp"
        android:layout_weight="1"
        android:dividerHeight="8dp"
        android:clipToPadding="false" />

</LinearLayout>
```

### 3. list_item.xml

Create this file in `res/layout/list_item.xml`.

```xml
<?xml version="1.0" encoding="utf-8"?>
<LinearLayout
    xmlns:android="http://schemas.android.com/apk/res/android"
    android:layout_width="match_parent"
    android:layout_height="wrap_content"
    android:minHeight="88dp"
    android:orientation="horizontal"
    android:gravity="center_vertical"
    android:padding="12dp">

    <ImageView
        android:id="@+id/itemImage"
        android:layout_width="64dp"
        android:layout_height="64dp"
        android:scaleType="fitCenter"
        android:contentDescription="List item image" />

    <TextView
        android:id="@+id/itemName"
        android:layout_width="0dp"
        android:layout_height="wrap_content"
        android:layout_weight="1"
        android:layout_marginStart="16dp"
        android:textSize="18sp"
        android:maxLines="2" />

</LinearLayout>
```

## Adding Images

Place five image files in the `res/drawable` directory:

- `android.png`
- `kotlin.png`
- `java.png`
- `python.png`
- `flutter.png`

Use lowercase filenames with no spaces or special characters. If you use different filenames, update the corresponding drawable references in `MainActivity.kt`.

## Expected Output

The application displays a scrollable list of programming technologies. Each row contains an image and its corresponding name. The layout uses flexible sizing and image scaling to improve usability on different screen sizes.

## Result

An adaptive Android user interface using `ListView` and `ImageView` was implemented successfully using Kotlin and XML layouts in Android Studio.

## Conclusion

This experiment demonstrates how to create a scrollable list containing images and text and how to use flexible layout parameters to make an Android UI more adaptable across devices.

