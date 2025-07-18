# Search Algorithms in [[C++]]

###[[Linear Search]] Algorithm
The function:

	int linearSearch(int array[], int size, int searchValue)
	{
		for(int i = 0; i < size; i++){
			if (searchValue == array[i]){
				return i;
			}
		}
		return -1;
	}

### Binary Search Algorithm
The function:

	int binarySearch(int array[], int size, int searchValue)
	{
		int low = 0;
		int high = size - 1;
		
		int mid;
		mid = (low + high) / 2;
		
		while (low <= high){
			if(searchValue == array[mid]){
				return mid;
			}
			else if (searchValue > array[mid]) {
				low = mid + 1;
			}
			else {
				high = mid - 1;
			}
		}
		return -1;
	}

See also:
- 