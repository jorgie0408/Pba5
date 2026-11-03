<?xml version="1.0" encoding="utf-8"?>
<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:orientation="vertical"
    android:padding="20dp"
    android:background="#FFF8F0">

    <TextView
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:text="JORGIE CAFE"
        android:textSize="28sp"
        android:textStyle="bold"
        android:textColor="#543A2C"
        android:gravity="center"
        android:padding="12dp" />

    <TextView
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:text="Nikmati kopi dan minuman favoritmu"
        android:textSize="14sp"
        android:textColor="#795548"
        android:gravity="center"
        android:paddingBottom="16dp" />

    <TextView
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:text="DAFTAR MENU"
        android:textSize="18sp"
        android:textStyle="bold"
        android:textColor="#543A2C"
        android:padding="8dp" />

    <androidx.recyclerview.widget.RecyclerView
        android:id="@+id/rvMenu"
        android:layout_width="match_parent"
        android:layout_height="0dp"
        android:layout_weight="1"
        android:clipToPadding="false" />

    <Button
        android:id="@+id/btnHistory"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:text="Lihat Riwayat Pesanan"
        android:backgroundTint="#795548"
        android:textColor="#FFFFFF" />

</LinearLayout>
