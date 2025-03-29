#include <iostream>
#include <vector>
#include <algorithm>

using namespace std;

// 1. Linear Search
int linearSearch(const vector<int>& arr, int target) {
    for (int i = 0; i < arr.size(); ++i)
        if (arr[i] == target)
            return i;
    return -1;
}

// 2. Binary Search (array must be sorted)
int binarySearch(const vector<int>& arr, int target) {
    int left = 0, right = arr.size() - 1;

    while (left <= right) {
        int mid = left + (right - left) / 2;

        if (arr[mid] == target) return mid;
        else if (arr[mid] < target) left = mid + 1;
        else right = mid - 1;
    }
    return -1;
}

// 3. Interpolation Search (array must be sorted and uniformly distributed)
int interpolationSearch(const vector<int>& arr, int target) {
    int low = 0, high = arr.size() - 1;

    while (low <= high && target >= arr[low] && target <= arr[high]) {
        if (low == high) {
            return (arr[low] == target) ? low : -1;
        }

        int pos = low + ((double)(high - low) / (arr[high] - arr[low]) * (target - arr[low]));

        if (arr[pos] == target)
            return pos;
        if (arr[pos] < target)
            low = pos + 1;
        else
            high = pos - 1;
    }
    return -1;
}

// 4. Exponential Search (array must be sorted)
int binarySearchExponential(const vector<int>& arr, int left, int right, int target) {
    while (left <= right) {
        int mid = left + (right - left) / 2;
        if (arr[mid] == target) return mid;
        if (arr[mid] < target) left = mid + 1;
        else right = mid - 1;
    }
    return -1;
}

int exponentialSearch(const vector<int>& arr, int target) {
    if (arr[0] == target) return 0;

    int i = 1;
    while (i < arr.size() && arr[i] <= target)
        i *= 2;

    return binarySearchExponential(arr, i / 2, min(i, (int)arr.size() - 1), target);
}

int main() {
    vector<int> data = {2, 4, 7, 10, 23, 37, 45, 51, 68, 77};
    int target = 37;

    cout << "Target: " << target << endl;
    cout << "Linear Search Index: " << linearSearch(data, target) << endl;
    cout << "Binary Search Index: " << binarySearch(data, target) << endl;
    cout << "Interpolation Search Index: " << interpolationSearch(data, target) << endl;
    cout << "Exponential Search Index: " << exponentialSearch(data, target) << endl;

    return 0;
}
