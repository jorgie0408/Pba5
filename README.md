<?xml version="1.0" encoding="utf-8"?>
<ScrollView xmlns:android="http://schemas.android.com/apk/res/android"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:background="#FFF8F0">

    <LinearLayout
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:orientation="vertical"
        android:padding="24dp">

        <TextView
            android:layout_width="match_parent"
            android:layout_height="wrap_content"
            android:text="FORM PEMESANAN"
            android:textSize="24sp"
            android:textStyle="bold"
            android:textColor="#543A2C"
            android:gravity="center"
            android:paddingBottom="20dp" />

        <TextView
            android:id="@+id/tvSelectedMenu"
            android:layout_width="match_parent"
            android:layout_height="wrap_content"
            android:text="Menu"
            android:textSize="20sp"
            android:textStyle="bold"
            android:textColor="#543A2C" />

        <TextView
            android:id="@+id/tvSelectedPrice"
            android:layout_width="match_parent"
            android:layout_height="wrap_content"
            android:text="Harga"
            android:textSize="16sp"
            android:textColor="#795548"
            android:paddingBottom="16dp" />

        <EditText
            android:id="@+id/etCustomerName"
            android:layout_width="match_parent"
            android:layout_height="wrap_content"
            android:hint="Nama pelanggan"
            android:inputType="textPersonName" />

        <EditText
            android:id="@+id/etPhone"
            android:layout_width="match_parent"
            android:layout_height="wrap_content"
            android:hint="Nomor telepon"
            android:inputType="phone" />

        <TextView
            android:layout_width="match_parent"
            android:layout_height="wrap_content"
            android:text="Jumlah Pesanan"
            android:textColor="#543A2C"
            android:textStyle="bold"
            android:paddingTop="12dp" />

        <EditText
            android:id="@+id/etQuantity"
            android:layout_width="match_parent"
            android:layout_height="wrap_content"
            android:hint="Masukkan jumlah"
            android:inputType="number"
            android:text="1" />

        <CheckBox
            android:id="@+id/cbMember"
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"
            android:text="Saya adalah Member (Diskon 10%)"
            android:textColor="#543A2C" />

        <Button
            android:id="@+id/btnCalculate"
            android:layout_width="match_parent"
            android:layout_height="wrap_content"
            android:text="Hitung Total"
            android:backgroundTint="#795548" />

        <TextView
            android:id="@+id/tvSubtotal"
            android:layout_width="match_parent"
            android:layout_height="wrap_content"
            android:text="Subtotal: Rp0"
            android:textSize="16sp"
            android:textColor="#543A2C"
            android:paddingTop="12dp" />

        <TextView
            android:id="@+id/tvDiscount"
            android:layout_width="match_parent"
            android:layout_height="wrap_content"
            android:text="Diskon: Rp0"
            android:textSize="16sp"
            android:textColor="#543A2C"
            android:paddingTop="8dp" />

        <TextView
            android:id="@+id/tvTotal"
            android:layout_width="match_parent"
            android:layout_height="wrap_content"
            android:text="Total: Rp0"
            android:textSize="20sp"
            android:textStyle="bold"
            android:textColor="#795548"
            android:paddingTop="8dp" />

        <Button
            android:id="@+id/btnConfirm"
            android:layout_width="match_parent"
            android:layout_height="wrap_content"
            android:text="Konfirmasi Pesanan"
            android:backgroundTint="#4CAF50"
            android:textColor="#FFFFFF"
            android:layout_marginTop="16dp" />

    </LinearLayout>
</ScrollView>
