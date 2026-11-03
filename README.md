<?xml version="1.0" encoding="utf-8"?>
<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
    android:layout_width="match_parent"
    android:layout_height="wrap_content"
    android:orientation="vertical"
    android:padding="16dp"
    android:layout_marginBottom="12dp"
    android:background="#FFFFFF"
    android:elevation="3dp">

    <TextView
        android:id="@+id/tvCustomer"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:text="Pelanggan"
        android:textSize="17sp"
        android:textStyle="bold"
        android:textColor="#543A2C" />

    <TextView
        android:id="@+id/tvOrderMenu"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:text="Menu"
        android:textColor="#543A2C"
        android:paddingTop="6dp" />

    <TextView
        android:id="@+id/tvOrderQuantity"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:text="Jumlah"
        android:textColor="#543A2C"
        android:paddingTop="4dp" />

    <TextView
        android:id="@+id/tvOrderDiscount"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:text="Diskon"
        android:textColor="#4CAF50"
        android:paddingTop="4dp" />

    <TextView
        android:id="@+id/tvOrderTotal"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:text="Total"
        android:textSize="17sp"
        android:textStyle="bold"
        android:textColor="#795548"
        android:paddingTop="6dp" />

    <TextView
        android:id="@+id/tvOrderDate"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:text="Tanggal"
        android:textSize="12sp"
        android:textColor="#888888"
        android:paddingTop="6dp" />

</LinearLayout>




<?xml version="1.0" encoding="utf-8"?>
<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:app="http://schemas.android.com/apk/res-auto"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:orientation="vertical"
    android:padding="20dp"
    android:background="#FFF8F0">

    <TextView
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:text="RIWAYAT PESANAN"
        android:textSize="24sp"
        android:textStyle="bold"
        android:textColor="#543A2C"
        android:gravity="center"
        android:padding="12dp" />

    <androidx.recyclerview.widget.RecyclerView
        android:id="@+id/rvHistory"
        android:layout_width="match_parent"
        android:layout_height="0dp"
        android:layout_weight="1"
        android:paddingTop="10dp" />

    <TextView
        android:id="@+id/tvEmpty"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:text="Belum ada transaksi."
        android:textSize="16sp"
        android:textColor="#795548"
        android:gravity="center"
        android:visibility="gone" />

    <Button
        android:id="@+id/btnBack"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:text="Kembali ke Menu"
        android:backgroundTint="#795548"
        android:textColor="#FFFFFF" />

</LinearLayout>

package uts.c14220290.app

import android.view.LayoutInflater
import android.view.View
import android.view.ViewGroup
import android.widget.TextView
import androidx.recyclerview.widget.RecyclerView
import java.text.NumberFormat
import java.util.Locale

class OrderAdapter(
    private val orderList: List<Order>
) : RecyclerView.Adapter<OrderAdapter.OrderViewHolder>() {

    class OrderViewHolder(view: View) : RecyclerView.ViewHolder(view) {
        val customer: TextView = view.findViewById(R.id.tvCustomer)
        val menu: TextView = view.findViewById(R.id.tvOrderMenu)
        val quantity: TextView = view.findViewById(R.id.tvOrderQuantity)
        val total: TextView = view.findViewById(R.id.tvOrderTotal)
        val date: TextView = view.findViewById(R.id.tvOrderDate)
        val discount: TextView = view.findViewById(R.id.tvOrderDiscount)
    }

    override fun onCreateViewHolder(
        parent: ViewGroup,
        viewType: Int
    ): OrderViewHolder {
        val view = LayoutInflater.from(parent.context)
            .inflate(R.layout.item_order, parent, false)

        return OrderViewHolder(view)
    }

    override fun onBindViewHolder(
        holder: OrderViewHolder,
        position: Int
    ) {
        val order = orderList[position]

        holder.customer.text = "Pelanggan: ${order.customerName}"
        holder.menu.text = "Menu: ${order.menuName}"
        holder.quantity.text = "Jumlah: ${order.quantity}"
        holder.discount.text = "Diskon: ${formatRupiah(order.discount)}"
        holder.total.text = "Total: ${formatRupiah(order.total)}"
        holder.date.text = "Tanggal: ${order.date}"
    }

    override fun getItemCount(): Int = orderList.size

    private fun formatRupiah(value: Int): String {
        return NumberFormat.getCurrencyInstance(
            Locale("id", "ID")
        ).format(value)
    }
}package uts.c14220290.app

import android.content.Intent
import android.net.Uri
import android.os.Bundle
import android.widget.Button
import android.widget.CheckBox
import android.widget.EditText
import android.widget.TextView
import android.widget.Toast
import androidx.appcompat.app.AppCompatActivity
import java.text.NumberFormat
import java.text.SimpleDateFormat
import java.util.Date
import java.util.Locale

class OrderActivity : AppCompatActivity() {

    private lateinit var dbHelper: DatabaseHelper

    private var menuId = 0
    private var menuName = ""
    private var menuPrice = 0

    private var subtotal = 0
    private var discount = 0
    private var total = 0
    private var calculated = false

    private lateinit var etCustomerName: EditText
    private lateinit var etPhone: EditText
    private lateinit var etQuantity: EditText
    private lateinit var cbMember: CheckBox

    private lateinit var tvSelectedMenu: TextView
    private lateinit var tvSelectedPrice: TextView
    private lateinit var tvSubtotal: TextView
    private lateinit var tvDiscount: TextView
    private lateinit var tvTotal: TextView

    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)
        setContentView(R.layout.activity_order)

        dbHelper = DatabaseHelper(this)

        menuId = intent.getIntExtra("MENU_ID", 0)
        menuName = intent.getStringExtra("MENU_NAME") ?: ""
        menuPrice = intent.getIntExtra("MENU_PRICE", 0)

        etCustomerName = findViewById(R.id.etCustomerName)
        etPhone = findViewById(R.id.etPhone)
        etQuantity = findViewById(R.id.etQuantity)
        cbMember = findViewById(R.id.cbMember)

        tvSelectedMenu = findViewById(R.id.tvSelectedMenu)
        tvSelectedPrice = findViewById(R.id.tvSelectedPrice)
        tvSubtotal = findViewById(R.id.tvSubtotal)
        tvDiscount = findViewById(R.id.tvDiscount)
        tvTotal = findViewById(R.id.tvTotal)

        val btnCalculate = findViewById<Button>(R.id.btnCalculate)
        val btnConfirm = findViewById<Button>(R.id.btnConfirm)

        tvSelectedMenu.text = menuName
        tvSelectedPrice.text = "Harga: ${formatRupiah(menuPrice)}"

        btnCalculate.setOnClickListener {
            calculateTotal()
        }

        btnConfirm.setOnClickListener {
            confirmOrder()
        }
    }

    private fun calculateTotal() {
        val quantity = etQuantity.text.toString().toIntOrNull()

        if (quantity == null || quantity <= 0) {
            etQuantity.error = "Masukkan jumlah yang valid"
            calculated = false
            return
        }

        subtotal = menuPrice * quantity

        discount = if (cbMember.isChecked) {
            (subtotal * 0.10).toInt()
        } else {
            0
        }

        total = subtotal - discount
        calculated = true

        tvSubtotal.text = "Subtotal: ${formatRupiah(subtotal)}"
        tvDiscount.text = "Diskon: ${formatRupiah(discount)}"
        tvTotal.text = "Total: ${formatRupiah(total)}"
    }

    private fun confirmOrder() {
        val customerName = etCustomerName.text.toString().trim()
        val phone = etPhone.text.toString().trim()
        val quantity = etQuantity.text.toString().toIntOrNull()

        if (customerName.isEmpty()) {
            etCustomerName.error = "Nama harus diisi"
            return
        }

        if (phone.isEmpty()) {
            etPhone.error = "Nomor telepon harus diisi"
            return
        }

        if (quantity == null || quantity <= 0) {
            etQuantity.error = "Jumlah pesanan tidak valid"
            return
        }

        // Hitung ulang untuk memastikan nilai terbaru tersimpan
        calculateTotal()

        if (!calculated) return

        val currentDate = SimpleDateFormat(
            "dd-MM-yyyy HH:mm",
            Locale("id", "ID")
        ).format(Date())

        val order = Order(
            id = 0,
            customerName = customerName,
            phone = phone,
            menuName = menuName,
            price = menuPrice,
            quantity = quantity,
            subtotal = subtotal,
            discount = discount,
            total = total,
            isMember = cbMember.isChecked,
            date = currentDate
        )

        val result = dbHelper.insertOrder(order)

        if (result == -1L) {
            Toast.makeText(
                this,
                "Gagal menyimpan transaksi",
                Toast.LENGTH_SHORT
            ).show()
            return
        }

        Toast.makeText(
            this,
            "Pesanan berhasil disimpan",
            Toast.LENGTH_SHORT
        ).show()

        sendSMS(customerName, phone, quantity)
    }

    private fun sendSMS(
        customerName: String,
        phone: String,
        quantity: Int
    ) {
        val message = """
            STRUK JORGIE CAFE

            Pelanggan: $customerName
            Menu: $menuName
            Harga: ${formatRupiah(menuPrice)}
            Jumlah: $quantity
            Subtotal: ${formatRupiah(subtotal)}
            Diskon: ${formatRupiah(discount)}
            Total: ${formatRupiah(total)}

            Terima kasih telah berbelanja!
        """.trimIndent()

        val intent = Intent(
            Intent.ACTION_SENDTO,
            Uri.parse("smsto:$phone")
        )

        intent.putExtra("sms_body", message)

        try {
            startActivity(intent)
            finish()
        } catch (e: Exception) {
            Toast.makeText(
                this,
                "Pesanan tersimpan, tetapi aplikasi SMS tidak tersedia",
                Toast.LENGTH_LONG
            ).show()
            finish()
        }
    }

    private fun formatRupiah(value: Int): String {
        return NumberFormat.getCurrencyInstance(
            Locale("id", "ID")
        ).format(value)
    }
}


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
