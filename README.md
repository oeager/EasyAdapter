# EasyAdapter

It Removes Boilerplate code of creating adapter

Features

- Removes Boilerplate code to create adapter.
- You can filter adapter without coding much.
- You wil have load more feature with loading at bottom.
- It has swipe to action functionality.
- and many more..

Usage
----------


## Adapter Creation

``` kotlin
class CategoryAdapter(categories: ArrayList<Category>, private val showSelection: Boolean = false) :
        BaseAdapter<Category, InflaterCategoryBinding>(categories, R.layout.inflater_category) {

    override fun onCreatingHolder(binding: InflaterCategoryBinding, baseHolder: BaseHolder) {
        super.onCreatingHolder(binding, baseHolder)
        binding.cbCategory.setVisible(showSelection)
        binding.root.setOnClickListener(baseHolder.clickListener)
    }

    override fun onBind(binding: InflaterCategoryBinding, model: Category) {
        binding.apply {
            tvName.text = model.name
            tvName.isSelected = model.isSelected
            cbCategory.isChecked = model.isSelected
            ivCategoryIcon.loadImage(model.image!!, R.drawable.img_nocate)
        }
    }
}
```

## View usage

### Handle click events of recycler view item
### override this method and set OnClickListener to baseHolder.clickListener

``` kotlin
override fun onCreatingHolder(binding: InflaterCategoryBinding, baseHolder: BaseHolder) {
        super.onCreatingHolder(binding, baseHolder)
        binding.cbCategory.setVisible(showSelection)
        binding.root.setOnClickListener(baseHolder.clickListener)
    }
```

### and you will have callback of each item click

``` kotlin
adapter.setRecyclerViewItemClick { itemView, model ->
            if (getSelectedCategoryCSV().size == 5 && !model.isSelected) {
                getString(R.string.msg_max_cat_sel).showToast()
            } else {
                model.isSelected = !model.isSelected
                adapter.notifyItemChanged(adapter.data.indexOf(model))
            }
        }

```

### Filter (Search,etc..)

adapter.performFilter(text, object :BaseAdapter.OnFilter<Category>{
                    override fun onFilterApply(text: String, model: Category): Boolean {
                        if (model.name?.toLowerCase()?.contains(text.toLowerCase())!!) {
                            return true
                        }
                        return false
                    }

                    override fun onResult(data: java.util.ArrayList<Category>?) {
                        //Filtered List to do any operation
                    }
                })


### Load More
``` kotlin
adapter.enableLoadMore(binding.recyclerView, BaseAdapter.OnLoadMoreListener {
            if (paging != -1) {
                requestLoadMore() //Your Method
                return@OnLoadMoreListener true // Returns True if you have more data
            }
            return@OnLoadMoreListener false // Return false if you don't have more data
        })

```

Happy Coding..!