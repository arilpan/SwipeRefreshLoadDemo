# SwipeRefreshLoadDemo

我写的新组件RecyclerViewPullRefresh #https://github.com/AndyZhaofeng/RecyclerViewPullRefresh#


改写的android.support.v4.widget.SwipeRefreshLayout类，使其可以上拉加载更多数据。其中对android.support.v7.widget.RecyclerView支持更好一些，当然也支持listview；

其中ListViewDemoActivity.java是ListView的例子，点击“菜单”选择“RecyclerViewDemo”进入RecyclerViewDemoActivity.java，RecyclerViewDemoActivity.java是RecyclerView的例子。
<pre>
使用示例：
mRefreshLayout.setOnRefreshListener(new SwipeRefreshLoadLayout.OnRefreshListener() {
	@Override
	public void onRefresh() {
		refreshContent();
	}
});
mRefreshLayout.setLoadMoreListener(new SwipeRefreshLoadLayout.LoadMoreListener() {
	@Override
	public void loadMore() {
		loadMoreData();
	}
});
	
private void refreshContent() {
	new Handler().postDelayed(new Runnable() {
		@Override
		public void run() {
			isLoadMore = false;
			isRefresh = true;
			EventBus.getDefault().post(new NetworkEvent(RequestType.INDEX_DISH_HOT));
			Log.e("arilpan", "调用 refreshContent  ");
			mRefreshLayout.setRefreshing(false);
		}
	}, 1000);
}

private void loadMoreData() {

	new Handler().postDelayed(new Runnable() {
		@Override
		public void run() {
			isLoadMore = true;
			isRefresh = false;
			EventBus.getDefault().post(new NetworkEvent(RequestType.INDEX_DISH_HOT));
			Log.e("arilpan", "调用loadMoreData  ");
			mRefreshLayout.setLoadMore(false);
		}
	}, 1000);
}

使用注意事项：
1.使用自定义组件com.zfeng.swiperefreshload.SwipeRefreshLoadLayout包裹RecyclerView，
  定义下拉setOnRefreshListener上拉setLoadMoreListener事件，
  然后刷新完成后使用setRefreshing,setLoadMore设置刷新状态。
2.网络请求，请不要在主线程中进行；
3.布局中有举例下边距，可以自行调整；
</pre>