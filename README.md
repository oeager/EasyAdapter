# EasyAdapter


(Supports only with DataBinding)

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
class CategoryAdapter() :EasyAdapter<Category, InflaterCategoryBinding>(R.layout.inflater_category) {

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

#### To Handle View events of recycler view item override method and set View events 
#### i.e To set OnClickListener to View use baseHolder.clickListener

``` kotlin
override fun onCreatingHolder(binding: InflaterCategoryBinding, baseHolder: BaseHolder) {
        super.onCreatingHolder(binding, baseHolder)
        binding.root.setOnClickListener(baseHolder.clickListener)
    }
```

#### and you will have callback of each item click

``` kotlin
adapter.setRecyclerViewItemClick { itemView, model -> //Perform Operation here }
```

#### Filter (Search,etc..)
``` kotlin
adapter.performFilter(text, object :EasyAdapter.OnFilter<Category>{
                    override fun onFilterApply(text: String, model: Category): Boolean {
                        if (model.name?.toLowerCase()?.contains(text.toLowerCase())!!) {
                            return true //Return True if you want to include this model in this text search
                        }
                        return false //It will not include model if you return false
                    }

                    override fun onResult(data: java.util.ArrayList<Category>?) {
                        //Filtered List to do any operation
                    }
                })

```

#### Load More
``` kotlin
adapter.enableLoadMore(binding.recyclerView, EasyAdapter.OnLoadMoreListener {
            if (paging != -1) {
                requestLoadMore() //Your Method
                return@OnLoadMoreListener true // Returns True if you have more data
            }
            return@OnLoadMoreListener false // Return false if you don't have more data
        })

```

Happy Coding..!

License
=======

    Copyright 2013 DC, Inc.

    Licensed under the Apache License, Version 2.0 (the "License");
    you may not use this file except in compliance with the License.
    You may obtain a copy of the License at

       http://www.apache.org/licenses/LICENSE-2.0

    Unless required by applicable law or agreed to in writing, software
    distributed under the License is distributed on an "AS IS" BASIS,
    WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
    See the License for the specific language governing permissions and
    limitations under the License.
