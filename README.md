# Android ListView Inside ScrollView

You can use the following function for solving the problem arise when putting a ListView inside a ScrollView. This will help you to set the height of ListView depends on the item sum of list item height.

```java

	public static void setListViewHeightBasedOnChildren(ListView listView) {
        ListAdapter listAdapter = listView.getAdapter();
        if (listAdapter == null) {
            // pre-condition
            return;
        }

        int totalHeight = 0;
        for (int i = 0; i < listAdapter.getCount(); i++) {
            View listItem = listAdapter.getView(i, null, listView);
            listItem.measure(0, 0);
            totalHeight += listItem.getMeasuredHeight();
        }

        ViewGroup.LayoutParams params = listView.getLayoutParams();
        params.height = totalHeight + (listView.getDividerHeight() * (listAdapter.getCount() - 1));
        listView.setLayoutParams(params);
    }
```

After setting the adapter to the ListView, just call this function by passing the ListView object as the parameter as follows.

```java
	......
	......
	myListView.setAdapter(adapter);
	setListViewHeightBasedOnChildren(myListView);
	......
	......
```
