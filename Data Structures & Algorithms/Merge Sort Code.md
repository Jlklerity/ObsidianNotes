	
	 void merge(std::vector<int>& arr, int F, int middle, int L)
	 {
		 const std::vector<int> leftarr{arr.begin() + F, arr.begin() + middle + 1};
		 const std::vector<int> rightarr{arr.begin() + middle + 1, arr.begin() + L + 1};
		 int i = 0;
		 int j = 0;
		 int k = F;
		 
		 while (i < leftarr.size() && j < rightarr.size())
		{
		     if (rightarr[j] < leftarr[i])
		     {
				arr[k] = rightarr[j];
			     ++j;
		     }
			     
			 else
			 {
				 arr[k] = leftarr[i];
				  ++i; 
			 }
			 ++k;
		}
		
		// remaining while loops to catch any remaining numbers have no  
											// counterparts to compare with
											
		while (i < leftarr.size())
		{
			 arr[k] = leftarr[i];
			 ++k; ++i;
		}
		while (j < rightarr.size())
		{
			arr[k] = rightarr[j];
			++k; ++j;
		}
	 }
		
	int arr[] = {6,5,4,3,2,1};
	int F = first index of arr;
	int L = last index of arr;
	void mergeSort(std::vector<int>& arr, int F, int L)
	{
		if F >= L return;
		int middle = (F + L) / 2;  //round down to nearest integer
		mergeSort(arr, F, middle);
		mergeSort(arr, middle+1, L);
		merge(arr, F, middle, L);  	
	}
	int main()
	 { 
		 std::vector<int> arr = {6, 5, 4, 3, 2, 1};
		 int F = 0;
		 int L = arr.size() - 1;
		 mergeSort(arr, F, L); 
		 for (int num : arr)
		 {
		    std::cout << num << " "; 
		 }
		  return 0;
	 }
