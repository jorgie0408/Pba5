package uts.c14220290.app

import android.content.Intent
import android.os.Bundle
import android.widget.Button
import androidx.appcompat.app.AppCompatActivity
import androidx.recyclerview.widget.LinearLayoutManager
import androidx.recyclerview.widget.RecyclerView

class MainActivity : AppCompatActivity() {

    private lateinit var rvMenu: RecyclerView
    private lateinit var btnHistory: Button

    private val menuList = listOf(
        Menu(1, "Espresso", "Kopi espresso original", 15000),
        Menu(2, "Americano", "Espresso dengan air panas", 18000),
        Menu(3, "Cafe Latte", "Espresso dengan susu steamed", 22000),
        Menu(4, "Cappuccino", "Espresso dengan foam susu", 22000),
        Menu(5, "Matcha Latte", "Matcha dengan susu creamy", 25000),
        Menu(6, "Chocolate", "Minuman cokelat premium", 23000)
    )

    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)
        setContentView(R.layout.activity_main)

        rvMenu = findViewById(R.id.rvMenu)
        btnHistory = findViewById(R.id.btnHistory)

        rvMenu.layoutManager = LinearLayoutManager(this)

        rvMenu.adapter = MenuAdapter(menuList) { menu ->
            val intent = Intent(this, OrderActivity::class.java)

            intent.putExtra("MENU_ID", menu.id)
            intent.putExtra("MENU_NAME", menu.name)
            intent.putExtra("MENU_PRICE", menu.price)

            startActivity(intent)
        }

        btnHistory.setOnClickListener {
            startActivity(
                Intent(this, HistoryActivity::class.java)
            )
        }
    }
}

import android.view.LayoutInflater
import android.view.View
import android.view.ViewGroup
import android.widget.Button
import android.widget.TextView
import androidx.recyclerview.widget.RecyclerView
import java.text.NumberFormat
import java.util.Locale

class MenuAdapter(
    private val menuList: List<Menu>,
    private val onClick: (Menu) -> Unit
) : RecyclerView.Adapter<MenuAdapter.MenuViewHolder>() {

    class MenuViewHolder(view: View) : RecyclerView.ViewHolder(view) {
        val name: TextView = view.findViewById(R.id.tvMenuName)
        val description: TextView = view.findViewById(R.id.tvMenuDescription)
        val price: TextView = view.findViewById(R.id.tvMenuPrice)
        val button: Button = view.findViewById(R.id.btnChoose)
    }

    override fun onCreateViewHolder(
        parent: ViewGroup,
        viewType: Int
    ): MenuViewHolder {
        val view = LayoutInflater.from(parent.context)
            .inflate(R.layout.item_menu, parent, false)

        return MenuViewHolder(view)
    }

    override fun onBindViewHolder(holder: MenuViewHolder, position: Int) {
        val menu = menuList[position]

        holder.name.text = menu.name
        holder.description.text = menu.description

        holder.price.text = formatRupiah(menu.price)

        holder.button.setOnClickListener {
            onClick(menu)
        }
    }

    override fun getItemCount(): Int = menuList.size

    private fun formatRupiah(value: Int): String {
        return NumberFormat.getCurrencyInstance(
            Locale("id", "ID")
        ).format(value)
    }
}package uts.c14220290.app

import android.content.ContentValues
import android.content.Context
import android.database.sqlite.SQLiteDatabase
import android.database.sqlite.SQLiteOpenHelper

class DatabaseHelper(context: Context) :
    SQLiteOpenHelper(context, "CafeDB", null, 1) {

    override fun onCreate(db: SQLiteDatabase) {
        val query = """
            CREATE TABLE orders (
                id INTEGER PRIMARY KEY AUTOINCREMENT,
                customer_name TEXT,
                phone TEXT,
                menu_name TEXT,
                price INTEGER,
                quantity INTEGER,
                subtotal INTEGER,
                discount INTEGER,
                total INTEGER,
                is_member INTEGER,
                date TEXT
            )
        """.trimIndent()

        db.execSQL(query)
    }

    override fun onUpgrade(
        db: SQLiteDatabase,
        oldVersion: Int,
        newVersion: Int
    ) {
        db.execSQL("DROP TABLE IF EXISTS orders")
        onCreate(db)
    }

    fun insertOrder(order: Order): Long {
        val db = writableDatabase
        val values = ContentValues().apply {
            put("customer_name", order.customerName)
            put("phone", order.phone)
            put("menu_name", order.menuName)
            put("price", order.price)
            put("quantity", order.quantity)
            put("subtotal", order.subtotal)
            put("discount", order.discount)
            put("total", order.total)
            put("is_member", if (order.isMember) 1 else 0)
            put("date", order.date)
        }

        return db.insert("orders", null, values)
    }

    fun getAllOrders(): ArrayList<Order> {
        val orders = ArrayList<Order>()
        val db = readableDatabase

        val cursor = db.rawQuery(
            "SELECT * FROM orders ORDER BY id DESC",
            null
        )

        cursor.use {
            while (it.moveToNext()) {
                orders.add(
                    Order(
                        id = it.getInt(it.getColumnIndexOrThrow("id")),
                        customerName = it.getString(it.getColumnIndexOrThrow("customer_name")),
                        phone = it.getString(it.getColumnIndexOrThrow("phone")),
                        menuName = it.getString(it.getColumnIndexOrThrow("menu_name")),
                        price = it.getInt(it.getColumnIndexOrThrow("price")),
                        quantity = it.getInt(it.getColumnIndexOrThrow("quantity")),
                        subtotal = it.getInt(it.getColumnIndexOrThrow("subtotal")),
                        discount = it.getInt(it.getColumnIndexOrThrow("discount")),
                        total = it.getInt(it.getColumnIndexOrThrow("total")),
                        isMember = it.getInt(it.getColumnIndexOrThrow("is_member")) == 1,
                        date = it.getString(it.getColumnIndexOrThrow("date"))
                    )
                )
            }
        }

        return orders
    }
}


KETENTUAN UMUM & REPOSITORY GITHUB
Sifat UTS : Open ALL Kecuali penggunaan AI
Nama Project: uts_nrp (Contoh: uts_c142300002)
Nama Package: uts.nrp.app (Ganti nrp dengan NRP lengkap Anda, contoh: uts.c142300002)
[WAJIB] GitHub Repository:
Buat Private Repository dengan nama yang sama dengan nama project (uts_nrp).
Tambahkan anitaforpetra@gmail.com sebagai collaborator.
Lakukan commit dengan pesan terstruktur sesuai tahapan fitur di bawah ini (Contoh format pesan commit: 1a - Desain Halaman Katalog).
Pastikan melakukan PUSH dan repo yang dikumpulkan adalah hasil commit terakhir.


KETENTUAN APLIKASI
Aplikasi yang harus Anda buat adalah Sistem Pesanan & Kalkulasi Kasir Cafe, yang terdiri dari 3 Halaman Utama (Halaman Katalog Menu, Halaman Pesanan, dan Halaman Daftar Pesanan).

Buat Desain per halaman sesuai dengan kebutuhan dan dapat di desain bebas (Desain akan diberikan penilaian tersendiri )


1. Halaman KATALOG MENU (Halaman Daftar)
(a) Item yang harus muncul pada setiap baris/card di daftar menu:

Nama Menu (Contoh: Caffe Latte, Matcha Frappe, Signature Tuna Bowl)

Harga Satuan Dasar (dalam format Rupiah)

(b) Aturan Interaksi:

Saat salah satu menu di-klik, user akan diarahkan ke Halaman Pesanan.

2. Halaman PESANAN
(a) Informasi yang harus ditampilkan/diinput:

Menampilkan Nama Menu dan Harga Satuan yang dipilih dari halaman sebelumnya.

Input Jumlah Qty

Pilihan Diskon Member: Checkbox atau RadioButton untuk menentukan apakah pembeli memiliki status "Member" (Diskon 10%).

(b) Total Harga akan dihitung otomatis saat ada perubahan :

Subtotal = Harga Satuan * Jumlah Porsi

Nilai Diskon = Jika berstatus Member, maka ada diskon 10%, jika tidak maka 0%.

Total Pembayaran Akhir = Subtotal - Nilai Diskon 

(c) Aturan Navigasi: 

Tombol "Konfirmasi Pesanan" akan menyimpan data transaksi dan meminta user input nama pemesan kemudian berpindah halaman ke Halaman Daftar Pesanan.
3. Halaman DAFTAR PESANAN
(a) Ketentuan Halaman:

Pesanan yang ada ditampilkan dalam bentuk daftar / List

Menampilkan rincian lengkap pesanan (Nama Pemesan, Nama Menu,  Rincian Perhitungan (Harga Satuan, Jumlah Porsi,  Diskon yang didapat, dan Grand Total Pembayaran)).

(b) Fitur Tambahan:

Saat salah satu daftar ditekan. aplikasi akan meminta user memasukkan Nama Pelanggan dan no HP, lalu membuka aplikasi SMS untuk mengirimkan pesanan yang dipilih itu ke no HP yang dimasukkan.

Isi SMS: Struk Pesanan - [Nama Menu] - [Nama Pelanggan]

Tambahkan Log SMS Berhasil disiapkan beserta datanya agar mudah di tracking
