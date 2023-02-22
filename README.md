# Threads-Dreams-

RelativeLayout xmlns:android="http://schemas.android.com/apk/res/android"
    android:layout_width="match_parent"
    android:layout_height="match_parent" >

    <TextView
        android:id="@+id/title"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="Kleider-Shop"
        android:textSize="24sp"
        android:layout_margin="16dp"
        android:layout_alignParentTop="true"
        android:layout_centerHorizontal="true" />

    <ListView
        android:id="@+id/item_list"
        android:layout_width="match_parent"
        android:layout_height="match_parent"
        android:layout_below="@+id/title" />

</RelativeLayout>

public class Item {
    private String name;
    private String description;
    private double price;

    public Item(String name, String description, double price) {
        this.name = name;
        this.description = description;
        this.price = price;
    }

    public String getName() {
        return name;
    }

    public String getDescription() {
        return description;
    }

    public double getPrice() {
        return price;
    }
}

public class ItemAdapter extends ArrayAdapter<Item> {

    private Context mContext;
    private int mResource;

    public ItemAdapter(Context context, int resource, List<Item> items) {
        super(context, resource, items);
        mContext = context;
        mResource = resource;
    }

    @Override
    public View getView(int position, View convertView, ViewGroup parent) {
        if (convertView == null) {
            convertView = LayoutInflater.from(mContext).inflate(mResource, parent, false);
        }

        Item item = getItem(position);

        TextView nameView = convertView.findViewById(R.id.item_name);
        TextView descView = convertView.findViewById(R.id.item_desc);
        TextView priceView = convertView.findViewById(R.id.item_price);

        nameView.setText(item.getName());
        descView.setText(item.getDescription());
        priceView.setText("$" + String.format("%.2f", item.getPrice()));

        return convertView;
    }
}

public class MainActivity extends AppCompatActivity {

    private ListView mItemList;
    private ItemAdapter mItemAdapter;

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);

        mItemList = findViewById(R.id.item_list);

        List<Item> items = loadItems();
        mItemAdapter = new
