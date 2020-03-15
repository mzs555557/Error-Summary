#### RecyclerView的建立 

```java
public class MainActivity extends AppCompatActivity {
    private RecyclerView mRecyclerView;
    private RecyclerAdapter mAdapter;
    
    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);
        mRecyclerView = findViewById(R.id.recycler_view)
        initRecyclerView();
    }
    private void initRecyclerView() {
        List<String> datas = new ArrayList<>();
		mAdapter = new RecyclerAdapter(datas);
        mRecyclerView.setAdapter(mAdapter);
        mRecyclerView.setLayoutManager(new LinearLayoutManager(this.getActivity()));
    }
}
```

```java
public class RecyclerAdapter extends RecyclerView.Adapter<HomeCategoryAdapter.ViewHolder>{
    private List<String> mDatas;
    private LayoutInflater mInflater;
    
    public HomeCategoryAdapter(List<HomeCategory> mDatas) {
        this.mDatas = mDatas;
    }
    
    @NonNull
    @Override
    public ViewHolder onCreateViewHolder(@NonNull ViewGroup parent, int viewType) {
        mInflater = LayoutInflater.from(parent.getContext());
        return new ViewHolder(mInflater.inflate(R.layout.recycler_item, parent, false));
    }

    @Override
    public void onBindViewHolder(@NonNull ViewHolder holder, int position) {
        holder.textTitle.setText(mDatas.get(position));
    }

    @Override
    public int getItemCount() {
        return mDatas.size();
    }

    class ViewHolder extends RecyclerView.ViewHolder {
        TextView textTitle;

        public ViewHolder(@NonNull View itemView) {
            super(itemView);

            textTitle = itemView.findViewById(R.id.text_title);
        }
    }
    
}
```

```

```

