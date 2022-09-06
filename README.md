# Android-RecylerView Kotlin

✨Basically using a recyclerview in a project consists of 3 Steps!

1-Needs to create a cardview in our XML layout
2-Needs to create a dataclass which we will use datas in recyclerView.
3-Needs an Adapter for datas.

So Let's make an example. 🛠

⏩ Fisrtly build.gradle(Module) let's add below implementations;

<img width="528" alt="1" src="https://user-images.githubusercontent.com/88722745/186468900-c3776006-df97-4834-900b-613c9eb9efd9.png">

⏩ Create a new layout XML for cardview as below;

<?xml version="1.0" encoding="utf-8"?>
<androidx.cardview.widget.CardView
    xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:app="http://schemas.android.com/apk/res-auto"
    android:layout_width="match_parent"
    android:layout_height="50dp"
    android:layout_margin="10dp"
    app:cardElevation="6dp">

    <LinearLayout
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:orientation="horizontal"
        android:padding="5dp">

        <ImageView
            android:id="@+id/imageview"
            android:layout_width="40dp"
            android:layout_height="40dp" />

        <TextView
            android:id="@+id/textView"
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"
            android:layout_marginStart="10dp"
            android:layout_marginLeft="15dp"
            android:text="Title"
            android:textSize="20sp"
            android:textStyle="bold" />

    </LinearLayout>

</androidx.cardview.widget.CardView>

⏩ Add a cardview to activity main layout

<?xml version="1.0" encoding="utf-8"?>
<LinearLayout
    xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:tools="http://schemas.android.com/tools"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:orientation="vertical"
    tools:context=".MainActivity">

    <androidx.recyclerview.widget.RecyclerView
        android:id="@+id/recyclerview"
        android:layout_width="match_parent"
        android:layout_height="match_parent"
        tools:itemCount="5"
        tools:listitem="@layout/card_view_design" />

</LinearLayout>

⏩ Create a dataclass named as ViewModel

    data class ViewModel(val image:Int, val text:String){
    
    }

⏩ Create an Adapter for class for datas to integrate recyclerview

    class CustomAdapter(private val mList: List<ViewModel>) : RecyclerView.Adapter<CustomAdapter.ViewHolder>() {

    // create new views
    override fun onCreateViewHolder(parent: ViewGroup, viewType: Int): ViewHolder {
        // inflates the card_view_design view
        // that is used to hold list item
        val view = LayoutInflater.from(parent.context)
            .inflate(R.layout.card_view_design, parent, false)

        return ViewHolder(view)
    }

    // binds the list items to a view
    override fun onBindViewHolder(holder: ViewHolder, position: Int) {

        val ItemsViewModel = mList[position]

        // sets the image to the imageview from our itemHolder class
        holder.imageView.setImageResource(ItemsViewModel.image)

        // sets the text to the textview from our itemHolder class
        holder.textView.text = ItemsViewModel.text

    }

    // return the number of the items in the list
    override fun getItemCount(): Int {
        return mList.size
    }

    // Holds the views for adding it to image and text
    class ViewHolder(ItemView: View) : RecyclerView.ViewHolder(ItemView) {
        val imageView: ImageView = itemView.findViewById(R.id.imageview)
        val textView: TextView = itemView.findViewById(R.id.textView)
    }
}

⏩ At least define recyclerview in MainActivity

class MainActivity : AppCompatActivity() {
    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)
        setContentView(R.layout.activity_main)

        // getting the recyclerview by its id
        val recyclerview = findViewById<RecyclerView>(R.id.recyclerview)

        // this creates a vertical layout Manager
        recyclerview.layoutManager = LinearLayoutManager(this)

        // ArrayList of class ViewModel
        val data = ArrayList<ViewModel>()

        // This loop will create 20 Views containing
        // the image with the count of view
        for (i in 1..20) {
            data.add(ViewModel(R.drawable.ic_baseline_folder_24, "Item " + i))
        }

        // This will pass the ArrayList to our Adapter
        val adapter = CustomAdapter(data)

        // Setting the Adapter with the recyclerview
        recyclerview.adapter = adapter

    }
}

🏁 <img width="224" alt="2" src="https://user-images.githubusercontent.com/88722745/186472080-f17c09ad-e609-4833-9363-4d81050618dd.png">


That's ALL 😊


