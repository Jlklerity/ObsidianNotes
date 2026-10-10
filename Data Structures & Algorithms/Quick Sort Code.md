

	 int partition(int arr[], int f, int l)
	 {
	    int pivot = arr[l];
	    int i = f;
	    for (int j = f; j < l; ++j)
	    {
		    if (arr[j] <= pivot)
		    {
				std::swap(arr[i], arr[j]);
				++i;
		    }
	    }
	    std::swap(arr[i], arr[l]);
	    return i;
	 }
	 
    void quickSort(int arr[], int f, int l)
    {
	    if (f < l)
	    {
		    int pivot_index = partition(int arr[], int f, int l);
		    quickSort(arr, f, pivot_index - 1);
		    quickSort(arr, pivot_index + 1, l);
	    }
    }