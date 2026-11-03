<?xml version="1.0" encoding="utf-8"?>
<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
    android:layout_width="match_parent"
    android:layout_height="wrap_content"
    android:orientation="vertical"
    android:padding="16dp"
    android:layout_marginBottom="10dp"
    android:background="#FFFFFF"
    android:elevation="3dp">

    <TextView
        android:id="@+id/tvMenuName"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:text="Cafe Latte"
        android:textSize="18sp"
        android:textStyle="bold"
        android:textColor="#543A2C" />

    <TextView
        android:id="@+id/tvMenuDescription"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:text="Deskripsi menu"
        android:textSize="13sp"
        android:textColor="#777777"
        android:paddingTop="4dp" />

    <TextView
        android:id="@+id/tvMenuPrice"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:text="Rp22.000"
        android:textSize="16sp"
        android:textStyle="bold"
        android:textColor="#795548"
        android:paddingTop="8dp" />

    <Button
        android:id="@+id/btnChoose"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:text="Pilih Menu"
        android:backgroundTint="#795548"
        android:textColor="#FFFFFF" />

</LinearLayout>
