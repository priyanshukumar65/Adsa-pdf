//1. Explain the concept of a prefix sum array and its applications.

//1. 1. Prefix Sum Array
Concept: A prefix sum array is an auxiliary array that allows for efficient range sum queries. The prefix sum at index i contains the sum of all elements from the start of the array up to index i.

Applications:

Efficiently calculating the sum of elements in a subarray.
Solving problems related to cumulative sums, such as finding averages or checking conditions over ranges.

//2. Write a program to find the sum of elements in a given range [L, R] using a prefix sum array. Write its algorithm, program. Find its time and space complexities. Explain with suitable example.

//2. Program to Find the Sum of Elements in a Given Range [L, R] Using Prefix Sum Array
Algorithm:

Create a prefix sum array prefix where prefix[i] is the sum of the array elements from index 0 to i.
To find the sum of elements from index L to R, use the formula:
If L > 0: sum(L, R) = prefix[R] - prefix[L-1]
If L == 0: sum(L, R) = prefix[R]
C++ Program:

cpp

#include <iostream>
#include <vector>
using namespace std;

vector<int> prefixSum(const vector<int>& arr) {
    int n = arr.size();
    vector<int> prefix(n);
    prefix[0] = arr[0];
    for (int i = 1; i < n; i++) {
        prefix[i] = prefix[i - 1] + arr[i];
    }
    return prefix;
}

int rangeSum(const vector<int>& prefix, int L, int R) {
    if (L > 0) {
        return prefix[R] - prefix[L - 1];
    } else {
        return prefix[R];
    }
}

int main() {
    vector<int> arr = {1, 2, 3, 4, 5};
    vector<int> prefix = prefixSum(arr);
    int L = 1, R = 3; // Sum from index 1 to 3
    cout << "Sum from index " << L << " to " << R << " is: " << rangeSum(prefix, L, R) << endl; // Output: 9
    return 0;
}
Time Complexity: O(n) for creating the prefix sum array, O(1) for each range sum query. Space Complexity: O(n) for the prefix sum array.

//3. Solve the problem of finding the equilibrium index in an array. Write its algorithm, program. Find its time and space complexities. Explain with suitable example.

//3. Finding the Equilibrium Index in an Array
Algorithm:

Calculate the total sum of the array.
Initialize a variable left_sum to 0.
Iterate through the array, and for each index i, check if left_sum equals total_sum - left_sum - arr[i].
If they are equal, return the index i.
C++ Program:

cpp

#include <iostream>
#include <vector>
using namespace std;

int findEquilibriumIndex(const vector<int>& arr) {
    int total_sum = 0;
    for (int num : arr) {
        total_sum += num;
    }
    
    int left_sum = 0;
    for (int i = 0; i < arr.size(); i++) {
        if (left_sum == total_sum - left_sum - arr[i]) {
            return i;
        }
        left_sum += arr[i];
    }
    return -1; // No equilibrium index found
}

int main() {
    vector<int> arr = {1, 3, 5, 2, 2};
    int index = findEquilibriumIndex(arr);
    if (index != -1) {
        cout << "Equilibrium index is: " << index << endl; // Output: 2
    } else {
        cout << "No equilibrium index found." << endl;
    }
    return 0;
}
Time Complexity: O(n) Space Complexity: O(1)

//4. Check if an array can be split into two parts such that the sum of the prefix equals the sum of the suffix. Write its algorithm, program. Find its time and space complexities. Explain with suitable example.

//4. Check if an Array Can Be Split into Two Parts Such That the Sum of the Prefix Equals the Sum of the Suffix
Algorithm:

Calculate the total sum of the array.
Initialize a variable left_sum to 0.
Iterate through the array, and for each index i, check if left_sum equals total_sum - left_sum - arr[i].
If they are equal at any index, return true; otherwise, return false.
C++ Program:

cpp

#include <iostream>
#include <vector>
using namespace std;

bool canSplitEqualPrefixSuffix(const vector<int>& arr) {
    int total_sum = 0;
    for (int num : arr) {
        total_sum += num;
    }
    
    int left_sum = 0;
    for (int i = 0; i < arr.size(); i++) {
        if (left_sum == total_sum - left_sum - arr[i]) {
            return true;
        }
        left_sum += arr[i];
    }
    return false;
}

int main() {
    vector<int> arr = {1, 2, 3, 3};
    if (canSplitEqualPrefixSuffix(arr)) {
        cout << "The array can be split into two parts with equal prefix and suffix sums." << endl;
    } else {
        cout << "The array cannot be split into two parts with equal prefix and suffix sums." << endl;
    }
    return 0;
}
Time Complexity: O(n)
Space Complexity: O(1)

Example Explanation: For the array [1, 2, 3, 3], the prefix sum at index 1 is 1, and the suffix sum starting from index 2 is also 3. Thus, the array can be split.

//5. Find the maximum sum of any subarray of size K in a given array. Write its algorithm, program. Find its time and space complexities. Explain with suitable example.

//5. Find the Maximum Sum of Any Subarray of Size K
Algorithm:

Calculate the sum of the first K elements.
Slide the window across the array, updating the sum by subtracting the element that is left behind and adding the new element.
Keep track of the maximum sum encountered.
C++ Program:

cpp

#include <iostream>
#include <vector>
using namespace std;

int maxSumSubarrayOfSizeK(const vector<int>& arr, int K) {
    int n = arr.size();
    if (n < K) return -1; // Not enough elements

    int max_sum = 0, window_sum = 0;

    // Calculate the sum of the first window
    for (int i = 0; i < K; i++) {
        window_sum += arr[i];
    }
    max_sum = window_sum;

    // Slide the window
    for (int i = K; i < n; i++) {
        window_sum += arr[i] - arr[i - K];
        max_sum = max(max_sum, window_sum);
    }
    return max_sum;
}

int main() {
    vector<int> arr = {2, 1, 5, 1, 3, 2};
    int K = 3;
    cout << "Maximum sum of any subarray of size " << K << " is: " << maxSumSubarrayOfSizeK(arr, K) << endl; // Output: 9
    return 0;
}
Time Complexity: O(n)
Space Complexity: O(1)

Example Explanation: For the array [2, 1, 5, 1, 3, 2] and K = 3, the maximum sum of any subarray of size 3 is 9 (from the subarray [5, 1, 3]).

//6. Find the length of the longest substring without repeating characters. Write its algorithm, program. Find its time and space complexities. Explain with suitable example.

//6. Find the Length of the Longest Substring Without Repeating Characters
Algorithm:

Use a sliding window approach with two pointers.
Use a hash map to store the last index of each character.
Expand the right pointer and check for duplicates. If a duplicate is found, move the left pointer to the right of the last occurrence of the duplicate.
Update the maximum length.
C++ Program:

cpp

#include <iostream>
#include <unordered_map>
#include <string>
using namespace std;

int lengthOfLongestSubstring(const string& s) {
    unordered_map<char, int> charIndexMap;
    int maxLength = 0;
    int left = 0;

    for (int right = 0; right < s.length(); right++) {
        if (charIndexMap.find(s[right]) != charIndexMap.end()) {
            left = max(left, charIndexMap[s[right]] + 1);
        }
        charIndexMap[s[right]] = right;
        maxLength = max(maxLength, right - left + 1);
    }
    return maxLength;
}

int main() {
    string s = "abcabcbb";
    cout << "Length of the longest substring without repeating characters: " << lengthOfLongestSubstring(s) << endl; // Output: 3
    return 0;
}
Time Complexity: O(n)
Space Complexity: O(min(n, m)), where n is the length of the string and m is the size of the character set.

Example Explanation: For the string "abcabcbb", the longest substring without repeating characters is "abc", which has a length of 3.

//7. Find the longest palindromic substring in a given string. Write its algorithm, program.

//7. 7. Explain the Sliding Window Technique and Its Use in String Problems
Sliding Window Technique: The sliding window technique is a method for solving problems that involve contiguous subarrays or substrings. It uses two pointers to create a window that can expand and contract based on certain conditions.

Use in String Problems:

Finding the longest substring without repeating characters.
Finding the smallest substring containing all characters of another string.
Calculating the maximum sum of a subarray of fixed size.
The technique is efficient because it allows us to avoid unnecessary recalculations by maintaining a window of valid elements.

//8.Find the longest palindromic substring in a given string. Write its algorithm, program. 
Find its time and space complexities. Explain with suitable example.

//8.Problem: Find the Longest Palindromic Substring in a Given String
Algorithm:

Expand Around Center: For each character in the string, treat it as the center of a potential palindrome. There are two cases to consider:
Odd-length palindromes (single character center).
Even-length palindromes (two character center).
For each center, expand outwards as long as the characters on both sides are equal.
Keep track of the longest palindrome found during the expansion.
Steps:

Initialize variables to store the starting index and maximum length of the longest palindrome found.
Loop through each character in the string:
Expand around the character for odd-length palindromes.
Expand around the gap between the character and the next character for even-length palindromes.
Update the starting index and maximum length whenever a longer palindrome is found.
Return the longest palindromic substring using the starting index and maximum length.
C++ Program
cpp

#include <iostream>
#include <string>
using namespace std;

string longestPalindrome(const string& s) {
    if (s.empty()) return "";

    int start = 0, maxLength = 1;

    for (int i = 0; i < s.length(); i++) {
        // Check for odd-length palindromes
        int left = i, right = i;
        while (left >= 0 && right < s.length() && s[left] == s[right]) {
            if (right - left + 1 > maxLength) {
                start = left;
                maxLength = right - left + 1;
            }
            left--;
            right++;
        }

        // Check for even-length palindromes
        left = i, right = i + 1;
        while (left >= 0 && right < s.length() && s[left] == s[right]) {
            if (right - left + 1 > maxLength) {
                start = left;
                maxLength = right - left + 1;
            }
            left--;
            right++;
        }
    }
    return s.substr(start, maxLength);
}

int main() {
    string s = "babad";
    cout << "Longest palindromic substring: " << longestPalindrome(s) << endl; // Output: "bab" or "aba"
    return 0;
}
Time and Space Complexities
Time Complexity: O(n^2), where n is the length of the string. This is because for each character, we may expand up to n/2 times in the worst case.
Space Complexity: O(1), since we are using a constant amount of space for variables and not using any additional data structures that grow with input size.
Example Explanation
For the input string "babad":

The algorithm checks each character and its neighbors to find palindromes.
It finds "bab" and "aba" as valid palindromic substrings.
Both have the same length of 3, so either can be returned as the longest palindromic substring.
The output will be:

Run

Longest palindromic substring: bab
or

Run

Longest palindromic substring: aba
This approach efficiently finds the longest palindromic substring by leveraging the properties of palindromes and the expand-around-center technique.
 
 //9.Find the longest common prefix among a list of strings. Write its algorithm, program. 
Find its time and space complexities. Explain with suitable example.

//9. Algorithm
Edge Case Handling: If the list of strings is empty, return an empty string.
Initialize the Prefix: Start with the first string as the initial prefix.
Iterate Through Strings: For each string in the list (starting from the second string):
Compare the current prefix with the string character by character.
Update the prefix to the common part found.
If at any point the prefix becomes empty, break out of the loop.
Return the Result: After processing all strings, return the longest common prefix.
C++ Implementation
cpp

#include <iostream>
#include <vector>
#include <string>

std::string longestCommonPrefix(const std::vector<std::string>& strs) {
    if (strs.empty()) return "";

    std::string prefix = strs[0]; // Start with the first string as the prefix

    for (size_t i = 1; i < strs.size(); ++i) {
        const std::string& current = strs[i];
        size_t j = 0;

        // Compare characters of prefix and current string
        while (j < prefix.length() && j < current.length() && prefix[j] == current[j]) {
            j++;
        }

        // Update the prefix to the common part found
        prefix = prefix.substr(0, j);

        // If at any point the prefix becomes empty, break
        if (prefix.empty()) break;
    }

    return prefix;
}

int main() {
    std::vector<std::string> strs = {"flower", "flow", "flight"};
    std::string result = longestCommonPrefix(strs);
    std::cout << "Longest Common Prefix: " << result << std::endl; // Output: "fl"
    return 0;
}
Example Explanation
Consider the input list of strings: ["flower", "flow", "flight"].

Start with the first string "flower" as the initial prefix.
Compare "flower" with "flow":
Common characters: "flow" (prefix becomes "flow").
Compare "flow" with "flight":
Common characters: "fl" (prefix becomes "fl").
The final longest common prefix is "fl".
Time Complexity
The time complexity of this algorithm is O(N * M), where:
N is the number of strings in the list.
M is the length of the shortest string among the list.
In the worst case, we may have to compare each character of the shortest string with each of the other strings.
Space Complexity
The space complexity is O(1) if we do not consider the output string, as we are using a constant amount of extra space for variables. If we consider the output string, it would be O(M), where M is the length of the longest common prefix.
This algorithm is efficient and straightforward, making it suitable for finding the longest common prefix in a list of strings.

//10.Generate all permutations of a given string. Write its algorithm, program. Find its time 
and space complexities. Explain with suitable example. 

//10.Algorithm
Base Case: If the current index is equal to the length of the string, add the current permutation to the result list.
Recursive Case: For each index from the current index to the end of the string:
Swap the current character with the character at the current index.
Recursively call the function to generate permutations for the next index.
Backtrack by swapping the characters back to their original positions.
Return the Result: After generating all permutations, return the list of permutations.
C++ Implementation
cpp

#include <iostream>
#include <vector>
#include <string>

void permuteHelper(std::string str, int left, int right, std::vector<std::string>& result) {
    if (left == right) {
        result.push_back(str); // Add the current permutation to the result
    } else {
        for (int i = left; i <= right; i++) {
            std::swap(str[left], str[i]); // Swap current index with left
            permuteHelper(str, left + 1, right, result); // Recur for the next index
            std::swap(str[left], str[i]); // Backtrack to the original string
        }
    }
}

std::vector<std::string> generatePermutations(const std::string& str) {
    std::vector<std::string> result;
    permuteHelper(str, 0, str.length() - 1, result);
    return result;
}

int main() {
    std::string str = "abc";
    std::vector<std::string> permutations = generatePermutations(str);
    
    std::cout << "Permutations of " << str << " are:\n";
    for (const std::string& perm : permutations) {
        std::cout << perm << std::endl;
    }
    
    return 0;
}
Example Explanation
Consider the input string "abc".

Start with the first character 'a':

Swap 'a' with 'a' (no change), and recursively generate permutations for "bc".
Swap 'b' with 'b' (no change), and recursively generate permutations for "c".
Add "abc" to the result.
Swap 'b' with 'c', and recursively generate permutations for "b".
Add "acb" to the result.
Backtrack to the original string.
Now swap 'a' with 'b':

Generate permutations for "ac".
Add "bac" to the result.
Swap 'a' with 'c', and generate permutations for "b".
Add "bca" to the result.
Backtrack to the original string.
Finally, swap 'a' with 'c':

Generate permutations for "ab".
Add "cab" to the result.
Swap 'a' with 'b', and generate permutations for "c".
Add "cba" to the result.
The final permutations generated are: ["abc", "acb", "bac", "bca", "cab", "cba"].

Time Complexity
The time complexity of generating all permutations of a string of length ( n ) is O(n!). This is because there are ( n! ) permutations of ( n ) characters, and generating each permutation takes ( O(n) ) time due to the string manipulation involved.
Space Complexity
The space complexity is O(n) for the recursion stack, where ( n ) is the length of the string. Additionally, we need space to store the result, which can also be considered O(n!) for storing all permutations.
This algorithm efficiently generates all permutations of a given string using backtracking, making it a common approach in combinatorial problems.

//11. Find two numbers in a sorted array that add up to a target. Write its algorithm, program. 
Find its time and space complexities. Explain with suitable example. 

//11.Algorithm
Initialize Two Pointers: Set one pointer (left) at the beginning of the array and the other pointer (right) at the end of the array.
Iterate Until Pointers Meet:
Calculate the sum of the elements at the two pointers.
If the sum equals the target, return the two numbers.
If the sum is less than the target, move the left pointer one step to the right (to increase the sum).
If the sum is greater than the target, move the right pointer one step to the left (to decrease the sum).
Return: If no such pair is found, return an indication that no pair exists.
C++ Implementation

Copy code
#include <iostream>
#include <vector>

std::pair<int, int> findTwoNumbers(const std::vector<int>& nums, int target) {
    int left = 0;
    int right = nums.size() - 1;

    while (left < right) {
        int sum = nums[left] + nums[right];

        if (sum == target) {
            return {nums[left], nums[right]}; // Found the pair
        } else if (sum < target) {
            left++; // Move left pointer to the right
        } else {
            right--; // Move right pointer to the left
        }
    }

    return {-1, -1}; // Indicate that no pair was found
}

int main() {
    std::vector<int> nums = {1, 2, 3, 4, 6};
    int target = 5;
    auto result = findTwoNumbers(nums, target);

    if (result.first != -1) {
        std::cout << "Numbers found: " << result.first << " and " << result.second << std::endl;
    } else {
        std::cout << "No two numbers add up to the target." << std::endl;
    }

    return 0;
}
Example Explanation
Consider the sorted array: [1, 2, 3, 4, 6] and the target sum of 5.

Initialize left to 0 (pointing to 1) and right to 4 (pointing to 6).
Calculate the sum: 1 + 6 = 7. Since 7 is greater than 5, move the right pointer to 3 (pointing to 4).
Calculate the sum: 1 + 4 = 5. Since 5 equals the target, we have found the pair: 1 and 4.
Time Complexity
The time complexity of this algorithm is O(n), where ( n ) is the number of elements in the array. In the worst case, we may have to traverse the entire array once.
Space Complexity
The space complexity is O(1), as we are using a constant amount of extra space for the pointers and the result.
This two-pointer technique is efficient and straightforward for finding two numbers in a sorted array that add up to a specified target.


Bookmark message
Copy message
Export

//12. Rearrange numbers into the lexicographically next greater permutation. Write its 
algorithm, program. Find its time and space complexities. Explain with suitable 
example.

//12. Algorithm
Find the Pivot: Traverse the array from right to left and find the first pair of consecutive elements where the left element is smaller than the right element. This is the pivot point.
Find the Successor: If a pivot is found, traverse the array from right to left again to find the first element that is greater than the pivot. This element will be the successor.
Swap: Swap the pivot with the successor.
Reverse the Suffix: Reverse the sequence of elements to the right of the pivot's original position to get the next permutation in lexicographical order.
Handle Edge Case: If no pivot is found, it means the array is in descending order, and we can simply reverse the entire array to get the smallest permutation.
C++ Implementation
cpp

#include <iostream>
#include <vector>
#include <algorithm>

void nextPermutation(std::vector<int>& nums) {
    int n = nums.size();
    int pivot = -1;

    // Step 1: Find the pivot
    for (int i = n - 2; i >= 0; i--) {
        if (nums[i] < nums[i + 1]) {
            pivot = i;
            break;
        }
    }

    if (pivot == -1) {
        // If no pivot, reverse the entire array
        std::reverse(nums.begin(), nums.end());
        return;
    }

    // Step 2: Find the successor
    for (int i = n - 1; i > pivot; i--) {
        if (nums[i] > nums[pivot]) {
            // Step 3: Swap
            std::swap(nums[i], nums[pivot]);
            break;
        }
    }

    // Step 4: Reverse the suffix
    std::reverse(nums.begin() + pivot + 1, nums.end());
}

int main() {
    std::vector<int> nums = {1, 2, 3};
    nextPermutation(nums);

    std::cout << "Next permutation: ";
    for (int num : nums) {
        std::cout << num << " ";
    }
    std::cout << std::endl;

    return 0;
}
Example Explanation
Consider the input array: [1, 2, 3].

Find the Pivot: Starting from the end, we find that 2 < 3 (at index 1), so the pivot is 2.
Find the Successor: The successor is 3 (the first number greater than 2 found from the end).
Swap: Swap 2 and 3, resulting in [1, 3, 2].
Reverse the Suffix: The suffix after the pivot is [2], which is already in order. Thus, the final result is [1, 3, 2].
For another example, consider the input array: [3, 2, 1].

Find the Pivot: No pivot is found since the array is in descending order.
Reverse the Entire Array: The array becomes [1, 2, 3], which is the smallest permutation.
Time Complexity
The time complexity of this algorithm is O(n), where ( n ) is the number of elements in the array. This is because we may need to traverse the array a few times (finding the pivot, finding the successor, and reversing the suffix).
Space Complexity
The space complexity is O(1), as we are using a constant amount of extra space for variables and do not require any additional data structures.
This algorithm efficiently finds the next lexicographical permutation of a sequence of numbers, making it a common approach in combinatorial problems.

//13. How to merge two sorted linked lists into one sorted list. Write its algorithm, program. 
Find its time and space complexities. Explain with suitable example.

//13.Algorithm
Initialize a Dummy Node: Create a dummy node to serve as the starting point of the merged list. This helps simplify the merging process.
Create a Pointer: Use a pointer to keep track of the last node in the merged list.
Iterate Through Both Lists:
Compare the current nodes of both linked lists.
Append the smaller node to the merged list and move the pointer of the merged list forward.
Move the pointer of the list from which the node was taken forward.
Attach Remaining Nodes: Once one of the lists is exhausted, attach the remaining nodes of the other list to the merged list.
Return the Merged List: The merged list starts from the next node of the dummy node.
C++ Implementation
cpp

#include <iostream>

struct ListNode {
    int val;
    ListNode* next;
    ListNode(int x) : val(x), next(nullptr) {}
};

ListNode* mergeTwoLists(ListNode* l1, ListNode* l2) {
    ListNode dummy(0); // Dummy node to simplify the merge process
    ListNode* tail = &dummy; // Pointer to the last node in the merged list

    while (l1 != nullptr && l2 != nullptr) {
        if (l1->val < l2->val) {
            tail->next = l1; // Append l1 node
            l1 = l1->next; // Move l1 pointer forward
        } else {
            tail->next = l2; // Append l2 node
            l2 = l2->next; // Move l2 pointer forward
        }
        tail = tail->next; // Move the tail pointer forward
    }

    // Attach the remaining nodes of l1 or l2
    if (l1 != nullptr) {
        tail->next = l1;
    } else {
        tail->next = l2;
    }

    return dummy.next; // Return the merged list starting from the next of dummy
}

// Helper function to print the linked list
void printList(ListNode* head) {
    while (head != nullptr) {
        std::cout << head->val << " -> ";
        head = head->next;
    }
    std::cout << "nullptr" << std::endl;
}

int main() {
    // Creating first sorted linked list: 1 -> 2 -> 4
    ListNode* l1 = new ListNode(1);
    l1->next = new ListNode(2);
    l1->next->next = new ListNode(4);

    // Creating second sorted linked list: 1 -> 3 -> 4
    ListNode* l2 = new ListNode(1);
    l2->next = new ListNode(3);
    l2->next->next = new ListNode(4);

    // Merging the two lists
    ListNode* mergedList = mergeTwoLists(l1, l2);

    // Printing the merged list
    std::cout << "Merged sorted linked list: ";
    printList(mergedList);

    // Clean up memory (not shown for brevity)
    return 0;
}
Example Explanation
Consider the two sorted linked lists:

List 1: 1 -> 2 -> 4
List 2: 1 -> 3 -> 4
Initialization: Start with a dummy node and a tail pointer.
Comparison:
Compare 1 (from List 1) and 1 (from List 2). Append 1 from List 2 to the merged list.
Compare 1 (from List 1) and 3 (from List 2). Append 1 from List 1 to the merged list.
Compare 2 (from List 1) and 3 (from List 2). Append 2 to the merged list.
Compare 4 (from List 1) and 3 (from List 2). Append 3 to the merged list.
Append the remaining 4 from List 1 and List 2.
Result: The merged list is 1 -> 1 -> 2 -> 3 -> 4 -> 4.
Time Complexity
The time complexity of this algorithm is O(n + m), where ( n ) is the number of nodes in the first linked list and ( m ) is the number of nodes in the second linked list. We traverse each list once.

//14. Find the median of two sorted arrays using binary search. Write its algorithm, program. 
Find its time and space complexities. Explain with suitable example.

//14.Algorithm
Ensure the First Array is the Smaller One: If the first array is larger than the second, swap them. This ensures that we always perform binary search on the smaller array.
Binary Search on the Smaller Array:
Set low to 0 and high to the length of the first array.
While low is less than or equal to high:
Calculate partitionX as the midpoint of the first array.
Calculate partitionY as the midpoint of the second array based on partitionX.
Determine the maximum and minimum values around the partitions:
maxX is the maximum value on the left side of the first array's partition.
minX is the minimum value on the right side of the first array's partition.
maxY is the maximum value on the left side of the second array's partition.
minY is the minimum value on the right side of the second array's partition.
Check for Correct Partition:
If maxX <= minY and maxY <= minX, we have found the correct partition.
If the combined length of the arrays is even, the median is the average of the two middle values.
If the combined length is odd, the median is the maximum of the left side.
If maxX > minY, move the high pointer to the left (decrease partitionX).
If maxY > minX, move the low pointer to the right (increase partitionX).
C++ Implementation
cpp

#include <iostream>
#include <vector>
#include <algorithm>
#include <limits>

double findMedianSortedArrays(std::vector<int>& nums1, std::vector<int>& nums2) {
    // Ensure nums1 is the smaller array
    if (nums1.size() > nums2.size()) {
        std::swap(nums1, nums2);
    }

    int x = nums1.size();
    int y = nums2.size();
    int low = 0, high = x;

    while (low <= high) {
        int partitionX = (low + high) / 2;
        int partitionY = (x + y + 1) / 2 - partitionX;

        // If partitionX is 0 it means nothing is there on left side. Use -inf for maxX
        // If partitionX is length of input then there is nothing on right side. Use +inf for minX
        int maxX = (partitionX == 0) ? std::numeric_limits<int>::min() : nums1[partitionX - 1];
        int minX = (partitionX == x) ? std::numeric_limits<int>::max() : nums1[partitionX];

        int maxY = (partitionY == 0) ? std::numeric_limits<int>::min() : nums2[partitionY - 1];
        int minY = (partitionY == y) ? std::numeric_limits<int>::max() : nums2[partitionY];

        if (maxX <= minY && maxY <= minX) {
            // We have partitioned array at correct place
            if ((x + y) % 2 == 0) {
                return (std::max(maxX, maxY) + std::min(minX, minY)) / 2.0;
            } else {
                return std::max(maxX, maxY);
            }
        } else if (maxX > minY) {
            // We are too far on right side for partitionX. Go on left side.
            high = partitionX - 1;
        } else {
            // We are too far on left side for partitionX. Go on right side.
            low = partitionX + 1;
        }
    }

    throw std::invalid_argument("Input arrays are not sorted.");
}

int main() {
    std::vector<int> nums1 = {1, 3};
    std::vector<int> nums2 = {2};

    double median = findMedianSortedArrays(nums1, nums2);
    std::cout << "Median of the two sorted arrays is: " << median << std::endl;

    return 0;
}
Example Explanation
Consider the two sorted arrays:

nums1 = [1, 3]
nums2 = [2]

//15. Find the k-th smallest element in a sorted matrix. Write its algorithm, program. Find its 
time and space complexities. Explain with suitable example.  

//15.Algorithm
Define the Search Space: The smallest element in the matrix is at the top-left corner, and the largest element is at the bottom-right corner. We will perform a binary search between these two values.
Binary Search:
Set low to the smallest element (matrix[0][0]) and high to the largest element (matrix[n-1][m-1]).
While low is less than or equal to high:
Calculate mid as the average of low and high.
Count how many elements are less than or equal to mid using a helper function.
If the count is less than k, it means the k-th smallest element is larger than mid, so move low to mid + 1.
If the count is greater than or equal to k, it means the k-th smallest element is less than or equal to mid, so move high to mid - 1.
Return the Result: When the loop ends, low will be the k-th smallest element.
C++ Implementation
cpp

#include <iostream>
#include <vector>

int countLessEqual(const std::vector<std::vector<int>>& matrix, int mid) {
    int count = 0;
    int n = matrix.size();
    int m = matrix[0].size();
    int row = n - 1, col = 0; // Start from the bottom-left corner

    while (row >= 0 && col < m) {
        if (matrix[row][col] <= mid) {
            count += (row + 1); // All elements in this column up to this row are <= mid
            col++; // Move right
        } else {
            row--; // Move up
        }
    }

    return count;
}

int kthSmallest(const std::vector<std::vector<int>>& matrix, int k) {
    int n = matrix.size();
    int m = matrix[0].size();
    int low = matrix[0][0];
    int high = matrix[n - 1][m - 1];

    while (low < high) {
        int mid = low + (high - low) / 2;
        int count = countLessEqual(matrix, mid);

        if (count < k) {
            low = mid + 1; // Move to the right half
        } else {
            high = mid; // Move to the left half
        }
    }

    return low; // low is the k-th smallest element
}

int main() {
    std::vector<std::vector<int>> matrix = {
        {1, 5, 9},
        {10, 11, 13},
        {12, 13, 15}
    };
    int k = 8;
    int result = kthSmallest(matrix, k);
    std::cout << "The " << k << "-th smallest element is: " << result << std::endl;

    return 0;
}
Example Explanation
Consider the following sorted matrix:

Run

1   5   9
10  11  13
12  13  15
We want to find the 8-th smallest element.

Initialization:

low = 1 (smallest element)
high = 15 (largest element)
Binary Search:

First iteration:
mid = (1 + 15) / 2 = 8
Count elements ≤ 8: There are 5 elements (1, 5, 9, 10, 11).
Since 5 < 8, we move low to mid + 1 = 9.
Second iteration:
mid = (9 + 15) / 2 = 12
Count elements ≤ 12: There are 6 elements (1, 5, 9, 10, 11, 12).
Since 6 < 8, we move low to mid + 1 = 13.
Third iteration:
mid = (13 + 15) / 2 = 14
Count elements ≤ 14: There are 8 elements (1, 5, 9, 10, 11, 12, 13, 13).
Since 8 ≥ 8, we move high to mid = 14.

//16. Find the majority element in an array that appears more than n/2 times. Write its 
algorithm, program. Find its time and space complexities. Explain with suitable 
example. 

//16.Algorithm
Initialize Variables:
Set a candidate variable to None and a count variable to 0.
First Pass (Finding the Candidate):
Iterate through each element in the array:
If count is 0, set the candidate to the current element and set count to 1.
If the current element is equal to the candidate, increment count.
If the current element is not equal to the candidate, decrement count.
Second Pass (Verification):
After finding the candidate, iterate through the array again to verify if the candidate appears more than ( n/2 ) times.
If it does, return the candidate; otherwise, return an indication that there is no majority element.
C++ Implementation

Copy code
#include <iostream>
#include <vector>

int majorityElement(const std::vector<int>& nums) {
    int candidate = 0;
    int count = 0;

    // First pass: Find the candidate
    for (int num : nums) {
        if (count == 0) {
            candidate = num;
            count = 1;
        } else if (num == candidate) {
            count++;
        } else {
            count--;
        }
    }

    // Second pass: Verify the candidate
    count = 0;
    for (int num : nums) {
        if (num == candidate) {
            count++;
        }
    }

    // Check if the candidate is indeed the majority element
    if (count > nums.size() / 2) {
        return candidate;
    } else {
        throw std::invalid_argument("No majority element found");
    }
}

int main() {
    std::vector<int> nums = {3, 2, 3};
    try {
        int result = majorityElement(nums);
        std::cout << "The majority element is: " << result << std::endl;
    } catch (const std::invalid_argument& e) {
        std::cout << e.what() << std::endl;
    }

    return 0;
}
Example Explanation
Consider the array: [3, 2, 3].

First Pass:

Start with candidate = 0 and count = 0.
For the first element 3:
count is 0, so set candidate = 3 and count = 1.
For the second element 2:
2 is not equal to 3, so decrement count to 0.
For the third element 3:
count is 0, so set candidate = 3 and count = 1.
After the first pass, the candidate is 3.

Second Pass:

Count occurrences of 3 in the array:
It appears 2 times.
Since 2 is greater than 3/2 (which is 1.5), 3 is confirmed as the majority element.
Time Complexity
The time complexity of this algorithm is O(n), where ( n ) is the number of elements in the array. We make two passes through the array.
Space Complexity
The space complexity is O(1), as we are using a constant amount of extra space for the candidate and count variables.

//17. Calculate how much water can be trapped between the bars of a histogram. Write its 
algorithm, program. Find its time and space complexities. Explain with suitable 
example

//17.Algorithm
Initialize Pointers and Variables:

Set two pointers, left at the beginning (0) and right at the end (length of the array - 1).
Initialize two variables, left_max and right_max, to keep track of the maximum heights encountered from the left and right sides, respectively.
Initialize a variable water_trapped to accumulate the total amount of trapped water.
Two-Pointer Traversal:

While left is less than or equal to right:
If the height at the left pointer is less than or equal to the height at the right pointer:
If the height at the left pointer is greater than or equal to left_max, update left_max.
Otherwise, calculate the trapped water at the left pointer as left_max - height[left] and add it to water_trapped.
Move the left pointer one step to the right.
Otherwise:
If the height at the right pointer is greater than or equal to right_max, update right_max.
Otherwise, calculate the trapped water at the right pointer as right_max - height[right] and add it to water_trapped.
Move the right pointer one step to the left.
Return the Result: After the loop, water_trapped will contain the total amount of trapped water.

C++ Implementation

Copy code
#include <iostream>
#include <vector>

int trap(const std::vector<int>& height) {
    if (height.empty()) return 0;

    int left = 0, right = height.size() - 1;
    int left_max = 0, right_max = 0;
    int water_trapped = 0;

    while (left <= right) {
        if (height[left] <= height[right]) {
            if (height[left] >= left_max) {
                left_max = height[left];
            } else {
                water_trapped += left_max - height[left];
            }
            left++;
        } else {
            if (height[right] >= right_max) {
                right_max = height[right];
            } else {
                water_trapped += right_max - height[right];
            }
            right--;
        }
    }

    return water_trapped;
}

int main() {
    std::vector<int> height = {0, 1, 0, 2, 1, 0, 1, 3, 2, 1, 2, 1};
    int result = trap(height);
    std::cout << "The amount of water trapped is: " << result << " units." << std::endl;

    return 0;
}
Example Explanation
Consider the histogram represented by the array: [0, 1, 0, 2, 1, 0, 1, 3, 2, 1, 2, 1].

Initialization:

left = 0, right = 11 (length of the array - 1)
left_max = 0, right_max = 0, water_trapped = 0
Two-Pointer Traversal:

Step 1: height[left] (0) ≤ height[right] (1)
Update left_max to 0 (no change).
Move left to 1.
Step 2: height[left] (1) ≤ height[right] (1)
Update left_max to 1.
Move left to 2.
Step 3: height[left] (0) ≤ height[right] (1)
left_max (1) > height[left] (0), so trapped water = 1 - 0 = 1.
Add 1 to water_trapped (total = 1).
Move left to 3.
Step 4: height[left] (2) > height[right] (1)
Update right_max to 1.
Move right to 10.
Step 5: height[left] (2) > height[right] (2)
Update right_max to 2.
Move right to 9.
Step 6: `height

//18.Find the maximum XOR of two numbers in an array. Write its algorithm, program. 
Find its time and space complexities. Explain with suitable example.

//18.Algorithm
Build a Trie:

Create a trie where each node represents a bit (0 or 1).
Insert each number from the array into the trie, bit by bit, starting from the most significant bit (MSB) to the least significant bit (LSB).
Calculate Maximum XOR:

For each number in the array, traverse the trie to find the number that gives the maximum XOR.
For each bit in the number, try to go in the opposite direction (i.e., if the current bit is 0, try to go to 1, and vice versa) to maximize the XOR.
Return the Maximum XOR: Keep track of the maximum XOR found during the traversal.

C++ Implementation
cpp

#include <iostream>
#include <vector>
#include <unordered_map>

class TrieNode {
public:
    TrieNode* children[2]; // Two children for 0 and 1
    TrieNode() {
        children[0] = nullptr;
        children[1] = nullptr;
    }
};

class Trie {
public:
    TrieNode* root;

    Trie() {
        root = new TrieNode();
    }

    void insert(int num) {
        TrieNode* node = root;
        for (int i = 31; i >= 0; i--) { // Assuming 32-bit integers
            int bit = (num >> i) & 1;
            if (!node->children[bit]) {
                node->children[bit] = new TrieNode();
            }
            node = node->children[bit];
        }
    }

    int findMaxXOR(int num) {
        TrieNode* node = root;
        int maxXOR = 0;
        for (int i = 31; i >= 0; i--) {
            int bit = (num >> i) & 1;
            // Try to go to the opposite bit to maximize XOR
            if (node->children[1 - bit]) {
                maxXOR |= (1 << i); // Set the i-th bit of maxXOR
                node = node->children[1 - bit];
            } else {
                node = node->children[bit];
            }
        }
        return maxXOR;
    }
};

int findMaximumXOR(const std::vector<int>& nums) {
    Trie trie;
    for (int num : nums) {
        trie.insert(num);
    }

    int maxXOR = 0;
    for (int num : nums) {
        maxXOR = std::max(maxXOR, trie.findMaxXOR(num));
    }
    return maxXOR;
}

int main() {
    std::vector<int> nums = {3, 10, 5, 25, 2, 8};
    int result = findMaximumXOR(nums);
    std::cout << "The maximum XOR of two numbers in the array is: " << result << std::endl;

    return 0;
}
Example Explanation
Consider the array: [3, 10, 5, 25, 2, 8].

Insert Numbers into the Trie:

Convert each number to its binary representation and insert it into the trie.
For example, the binary representation of 3 is 00000000000000000000000000000011, 10 is 00000000000000000000000000001010, and so on.
Calculate Maximum XOR:

For each number, traverse the trie to find the number that gives the maximum XOR.
For 3, we try to find a number that has the opposite bits at each position to maximize the XOR.
The maximum XOR for 3 is found with 10, resulting in 3 XOR 10 = 9.
Repeat this for all numbers in the array.
Final Result:

The maximum XOR found during the process is 28, which is the result of 5 XOR 25.
Time Complexity
The time complexity of this algorithm is O(n * b), where ( n ) is the number of elements in the array and ( b ) is the number of bits in the integers (32 for standard integers). This is because we insert each number into the trie and then find the maximum XOR for each number.
Space Complexity
The space complexity is O(n * b), where ( n ) is the number of elements in the array and ( b ) .

//19. How to find the maximum product subarray. Write its algorithm, program. Find its time 
and space complexities. Explain with suitable example.

//19.Algorithm
Initialize Variables:

Set max_product to the first element of the array.
Set current_max and current_min to the first element of the array.
Iterate Through the Array:

For each element in the array (starting from the second element):
If the current element is negative, swap current_max and current_min because multiplying by a negative number will change the signs.
Update current_max to be the maximum of the current element and the product of current_max and the current element.
Update current_min to be the minimum of the current element and the product of current_min and the current element.
Update max_product to be the maximum of max_product and current_max.
Return the Result: After iterating through the array, max_product will contain the maximum product of any subarray.

C++ Implementation
cpp

#include <iostream>
#include <vector>
#include <algorithm>

int maxProduct(const std::vector<int>& nums) {
    if (nums.empty()) return 0;

    int max_product = nums[0];
    int current_max = nums[0];
    int current_min = nums[0];

    for (size_t i = 1; i < nums.size(); i++) {
        if (nums[i] < 0) {
            std::swap(current_max, current_min); // Swap when we encounter a negative number
        }

        current_max = std::max(nums[i], current_max * nums[i]);
        current_min = std::min(nums[i], current_min * nums[i]);

        max_product = std::max(max_product, current_max);
    }

    return max_product;
}

int main() {
    std::vector<int> nums = {2, 3, -2, 4};
    int result = maxProduct(nums);
    std::cout << "The maximum product of a subarray is: " << result << std::endl;

    return 0;
}
Example Explanation
Consider the array: [2, 3, -2, 4].

Initialization:

max_product = 2 (first element)
current_max = 2
current_min = 2
Iterate Through the Array:

Element 3:
current_max = max(3, 2 * 3) = 6
current_min = min(3, 2 * 3) = 2
max_product = max(2, 6) = 6
Element -2:
Swap current_max and current_min: current_max = 2, current_min = 6
current_max = max(-2, 2 * -2) = -2
current_min = min(-2, 6 * -2) = -12
max_product = max(6, -2) = 6
Element 4:
current_max = max(4, -2 * 4) = 4
current_min = min(4, -12 * 4) = -48
max_product = max(6, 4) = 6
Final Result:

The maximum product of any subarray is 6, which comes from the subarray [2, 3].
Time Complexity
The time complexity of this algorithm is O(n), where ( n ) is the number of elements in the array. We make a single pass through the array.
Space Complexity
The space complexity is O(1), as we are using a constant amount of extra space for the variables max_product, current_max, and current_min.
This approach efficiently finds the maximum product subarray by leveraging the properties of multiplication and the effects of negative numbers.

//20. Count all numbers with unique digits for a given number of digits. Write its algorithm, 
program. Find its time and space complexities. Explain with suitable example.

//20.  Count all numbers with unique digits for a given number of digits. Write its algorithm, 
program. Find its time and space complexities. Explain with suitable example.

//20.Algorithm
Base Cases:

If ( n = 0 ), there is 1 number (the empty number).
If ( n = 1 ), there are 10 numbers (0 through 9).
Count Unique Digit Numbers:

For ( n \geq 2 ):
The first digit can be any digit from 1 to 9 (9 options).
The second digit can be any digit from 0 to 9 except the first digit (9 options).
The third digit can be any digit from 0 to 9 except the first two digits (8 options).
Continue this pattern until you reach ( n ) digits.
The formula for counting unique digit numbers for ( n ) digits can be expressed as:
For ( n = 2 ): ( 9 \times 9 )
For ( n = 3 ): ( 9 \times 9 \times 8 )
For ( n = 4 ): ( 9 \times 9 \times 8 \times 7 )
And so on...
Sum the Counts:

Sum the counts for all digit lengths from 1 to ( n ).
C++ Implementation
cpp

#include <iostream>

int countNumbersWithUniqueDigits(int n) {
    if (n == 0) return 1; // Only the empty number
    if (n == 1) return 10; // Digits 0-9

    int count = 10; // Start with 1-digit numbers
    int uniqueDigits = 9; // First digit can be 1-9
    int availableDigits = 9; // Remaining digits can be 0-9 excluding the first digit

    for (int i = 2; i <= n; i++) {
        uniqueDigits *= availableDigits; // Calculate unique digits for the current length
        count += uniqueDigits; // Add to the total count
        availableDigits--; // Decrease available digits for the next position
    }

    return count;
}

int main() {
    int n = 3; // Example: Count numbers with unique digits for 3 digits
    int result = countNumbersWithUniqueDigits(n);
    std::cout << "Count of numbers with unique digits for " << n << " digits is: " << result << std::endl;

    return 0;
}
Example Explanation
Let's consider ( n = 3 ):

Base Cases:

For ( n = 0 ): 1 (the empty number).
For ( n = 1 ): 10 (0 through 9).
Count for ( n = 2 ):

First digit: 9 options (1-9).
Second digit: 9 options (0-9 excluding the first digit).
Total for 2 digits: ( 9 \times 9 = 81 ).
Count for ( n = 3 ):

First digit: 9 options (1-9).
Second digit: 9 options (0-9 excluding the first digit).
Third digit: 8 options (0-9 excluding the first two digits).
Total for 3 digits: ( 9 \times 9 \times 8 = 648 ).
Final Count:

Total count for ( n = 3 ): ( 10 + 81 + 648 = 739 ).
Time Complexity
The time complexity of this algorithm is O(n), where ( n ) is the number of digits. We iterate from 2 to ( n ) to calculate the counts.
Space Complexity
The space complexity is O(1), as we are using a constant amount of extra space for the variables.
This approach efficiently counts the numbers with unique digits by leveraging combinatorial counting principles.

//21.How to count the number of 1s in the binary representation of numbers from 0 to n. 
Write its algorithm, program. Find its time and space complexities. Explain with 
suitable example

//21.Algorithm
Iterate Through Each Number:

For each number from 0 to ( n ), convert the number to its binary representation and count the number of 1s.
Count 1s Using Bit Manipulation:

For each number, use the bitwise AND operation to check each bit.
Right shift the number until it becomes 0, counting the number of 1s encountered.
Efficient Approach Using Dynamic Programming
We can also use a dynamic programming approach to count the number of 1s in binary representations from 0 to ( n ):

Create an Array:

Create an array count where count[i] will store the number of 1s in the binary representation of ( i ).
Fill the Array:

For each number ( i ) from 1 to ( n ):
Use the relation: count[i] = count[i >> 1] + (i & 1).
This means the number of 1s in ( i ) is the same as the number of 1s in ( i/2 ) (which is ( i >> 1 )) plus 1 if the least significant bit is 1.
Sum the Counts:

Sum all values in the count array to get the total number of 1s from 0 to ( n ).
C++ Implementation
Here’s the implementation of the efficient approach:

cpp

#include <iostream>
#include <vector>

int countBits(int n) {
    std::vector<int> count(n + 1, 0);
    int totalCount = 0;

    for (int i = 1; i <= n; i++) {
        count[i] = count[i >> 1] + (i & 1); // Count 1s using the relation
        totalCount += count[i]; // Sum the counts
    }

    return totalCount;
}

int main() {
    int n = 5; // Example: Count number of 1s from 0 to 5
    int result = countBits(n);
    std::cout << "The total number of 1s in binary representations from 0 to " << n << " is: " << result << std::endl;

    return 0;
}
Example Explanation
Let's consider ( n = 5 ):

Binary Representations:

0: 0 (0 ones)
1: 1 (1 one)
2: 10 (1 one)
3: 11 (2 ones)
4: 100 (1 one)
5: 101 (2 ones)
Count of 1s:

Total number of 1s from 0 to 5:
0 (0) + 1 (1) + 1 (2) + 2 (3) + 1 (4) + 2 (5) = 7
Time Complexity
The time complexity of this algorithm is O(n), where ( n ) is the input number. We iterate through all numbers from 1 to ( n ) and perform constant time operations for each.
Space Complexity
The space complexity is O(n) due to the storage of the count array. However, if we only need the total count and not the individual counts, we can optimize the space to O(1) by using a single integer to keep track of the total count.
This approach efficiently counts the number of 1s in the binary representations of numbers from 0 to ( n ) using dynamic programming principles.

//22. How to check if a number is a power of two using bit manipulation. Write its algorithm, 
program. Find its time and space complexities. Explain with suitable example.

//22.Algorithm
Check for Non-Positive Numbers:

If ( n ) is less than or equal to 0, it cannot be a power of two.
Use Bit Manipulation:

Use the expression ( n & (n - 1) ):
If ( n ) is a power of two, this expression will be 0.
This works because a power of two in binary has exactly one bit set (e.g., ( 1 ) is 0001, ( 2 ) is 0010, ( 4 ) is 0100, etc.). Subtracting 1 from it flips all the bits after the rightmost set bit, including that bit itself.
Return the Result:

If ( n > 0 ) and ( n & (n - 1) == 0 ), then ( n ) is a power of two.
C++ Implementation
Here’s the implementation of the algorithm:

cpp

#include <iostream>

bool isPowerOfTwo(int n) {
    // Check if n is greater than 0 and if n & (n - 1) is 0
    return n > 0 && (n & (n - 1)) == 0;
}

int main() {
    int n = 16; // Example: Check if 16 is a power of two
    if (isPowerOfTwo(n)) {
        std::cout << n << " is a power of two." << std::endl;
    } else {
        std::cout << n << " is not a power of two." << std::endl;
    }

    return 0;
}
Example Explanation
Let's consider ( n = 16 ):

Binary Representation:

The binary representation of ( 16 ) is 10000, which has exactly one bit set.
Check Using the Algorithm:

Calculate ( n - 1 ): ( 16 - 1 = 15 ) (binary 01111).
Perform the bitwise AND: ( 16 & 15 = 10000 & 01111 = 00000 ).
Since the result is 0, and ( n ) is greater than 0, we conclude that ( 16 ) is a power of two.
Time Complexity
The time complexity of this algorithm is O(1), as it performs a constant number of operations regardless of the size of the input.
Space Complexity
The space complexity is O(1), as we are using a constant amount of space for the variables.
This method is efficient and leverages the properties of binary numbers to determine if a number is a power of two using bit manipulation.

//23. How to find the maximum XOR of two numbers in an array. Write its algorithm, 
program. Find its time and space complexities. Explain with suitable example.

//23.Algorithm
Build a Trie:

Create a trie where each node represents a bit (0 or 1).
Insert each number from the array into the trie, bit by bit, starting from the most significant bit (MSB) to the least significant bit (LSB).
Calculate Maximum XOR:

For each number in the array, traverse the trie to find the number that gives the maximum XOR.
For each bit in the number, try to go in the opposite direction (i.e., if the current bit is 0, try to go to 1, and vice versa) to maximize the XOR.
Return the Maximum XOR: Keep track of the maximum XOR found during the traversal.

C++ Implementation
Here’s the implementation of the algorithm:

cpp

#include <iostream>
#include <vector>

class TrieNode {
public:
    TrieNode* children[2]; // Two children for 0 and 1
    TrieNode() {
        children[0] = nullptr;
        children[1] = nullptr;
    }
};

class Trie {
public:
    TrieNode* root;

    Trie() {
        root = new TrieNode();
    }

    void insert(int num) {
        TrieNode* node = root;
        for (int i = 31; i >= 0; i--) { // Assuming 32-bit integers
            int bit = (num >> i) & 1;
            if (!node->children[bit]) {
                node->children[bit] = new TrieNode();
            }
            node = node->children[bit];
        }
    }

    int findMaxXOR(int num) {
        TrieNode* node = root;
        int maxXOR = 0;
        for (int i = 31; i >= 0; i--) {
            int bit = (num >> i) & 1;
            // Try to go to the opposite bit to maximize XOR
            if (node->children[1 - bit]) {
                maxXOR |= (1 << i); // Set the i-th bit of maxXOR
                node = node->children[1 - bit];
            } else {
                node = node->children[bit];
            }
        }
        return maxXOR;
    }
};

int findMaximumXOR(const std::vector<int>& nums) {
    Trie trie;
    for (int num : nums) {
        trie.insert(num);
    }

    int maxXOR = 0;
    for (int num : nums) {
        maxXOR = std::max(maxXOR, trie.findMaxXOR(num));
    }
    return maxXOR;
}

int main() {
    std::vector<int> nums = {3, 10, 5, 25, 2, 8};
    int result = findMaximumXOR(nums);
    std::cout << "The maximum XOR of two numbers in the array is: " << result << std::endl;

    return 0;
}
Example Explanation
Consider the array: [3, 10, 5, 25, 2, 8].

Insert Numbers into the Trie:

Convert each number to its binary representation and insert it into the trie.
For example, the binary representation of 3 is 00000000000000000000000000000011, 10 is 00000000000000000000000000001010, and so on.
Calculate Maximum XOR:

For each number, traverse the trie to find the number that gives the maximum XOR.
For 3, we try to find a number that has the opposite bits at each position to maximize the XOR.
The maximum XOR for 3 is found with 10, resulting in 3 XOR 10 = 9.
Repeat this for all numbers in the array.
Final Result:

The maximum XOR found during the process is 28, which is the result of 5 XOR 25.
Time Complexity
The time complexity of this algorithm is O(n * b), where ( n ) is the number of elements in the array and ( b ) is the number of bits in the integers (32 for standard integers). This is because we insert each number into the trie and then find the maximum XOR for each number.
Space Complexity
The space complexity is O(n * b), where ( n ) is the number of elements in the array and .

//24. Explain the concept of bit manipulation and its advantages in algorithm design

//24.Concept of Bit Manipulation
Bit manipulation refers to the act of algorithmically manipulating bits or binary digits, which are the most basic units of data in computing. Each bit can be either a 0 or a 1, and by using various bitwise operations, we can perform a wide range of tasks efficiently.

Common bitwise operations include:

AND (&): Compares each bit of two numbers and returns a new number where each bit is set to 1 if both bits are 1.

Example: 5 & 3 (binary 0101 & 0011 results in 0001, which is 1).
OR (|): Compares each bit of two numbers and returns a new number where each bit is set to 1 if at least one of the bits is 1.

Example: 5 | 3 (binary 0101 | 0011 results in 0111, which is 7).
XOR (^): Compares each bit of two numbers and returns a new number where each bit is set to 1 if the bits are different.

Example: 5 ^ 3 (binary 0101 ^ 0011 results in 0110, which is 6).
NOT (~): Inverts all bits of a number.

Example: ~5 (binary 0101 becomes 1010, which is -6 in two's complement representation).
Left Shift (<<): Shifts all bits of a number to the left by a specified number of positions, filling in with zeros from the right.

Example: 5 << 1 (binary 0101 becomes 1010, which is 10).
Right Shift (>>): Shifts all bits of a number to the right by a specified number of positions.

Example: 5 >> 1 (binary 0101 becomes 0010, which is 2).
Advantages of Bit Manipulation in Algorithm Design
Efficiency:

Bitwise operations are generally faster than arithmetic operations because they operate directly on the binary representation of numbers. This can lead to significant performance improvements, especially in algorithms that require a large number of operations.
Memory Usage:

Bit manipulation allows for compact data representation. For example, a single integer can represent multiple boolean values (flags) using individual bits, reducing memory overhead.
Simplification of Logic:

Many problems can be solved more elegantly using bit manipulation. For example, checking if a number is a power of two can be done with a simple bitwise operation, which is often more intuitive than using division or logarithmic functions.
Direct Control:

Bit manipulation provides direct control over individual bits, which is useful in low-level programming, graphics, cryptography, and network protocols where precise control over data representation is required.
Algorithmic Techniques:

Many algorithms, such as those for finding subsets, counting bits, or performing fast multiplications, can be implemented more efficiently using bit manipulation techniques. For example, the "Hamming weight" (counting the number of 1s in a binary representation) can be computed quickly using bitwise operations.
Reduced Complexity:

Certain problems can be solved with lower time complexity using bit manipulation. For instance, finding the maximum XOR of two numbers can be done in linear time using a trie structure based on bit manipulation.
Example Use Cases
Finding Unique Elements:

Using XOR to find a unique number in an array where every other number appears twice.
Swapping Values:

Swapping two numbers without using a temporary variable using XOR.
Counting Set Bits:

Efficiently counting the number of 1s in a binary representation using bitwise operations.
Masking:

Using bit masks to isolate specific bits in a number, which is useful in graphics programming and data compression.
Conclusion
Bit manipulation is a powerful tool in algorithm design that can lead to more efficient, elegant, and compact solutions. Understanding how to leverage bitwise operations can significantly enhance a programmer's ability to solve complex problems effectively.

//25. Solve the problem of finding the next greater element for each element in an array. 
Write its algorithm, program. Find its time and space complexities. Explain with 
suitable example.

//25.Problem Statement
Given an array of integers, for each element, find the next greater element to the right. If there is no greater element, return -1 for that element.

Algorithm
Initialize a Stack:

Use a stack to keep track of the indices of the elements for which we haven't found the next greater element yet.
Iterate Through the Array:

Traverse the array from left to right.
For each element:
While the stack is not empty and the current element is greater than the element at the index stored at the top of the stack:
Pop the index from the stack and set the next greater element for that index to the current element.
Push the current index onto the stack.
Handle Remaining Indices:

After the loop, any indices left in the stack will have no next greater element, so set their next greater element to -1.
Return the Result:

Return the array containing the next greater elements.
C++ Implementation
Here’s the implementation of the algorithm:

cpp

#include <iostream>
#include <vector>
#include <stack>

std::vector<int> nextGreaterElements(const std::vector<int>& nums) {
    int n = nums.size();
    std::vector<int> result(n, -1); // Initialize result array with -1
    std::stack<int> s; // Stack to store indices

    for (int i = 0; i < n; i++) {
        // While stack is not empty and the current element is greater than the element at the index stored at the top of the stack
        while (!s.empty() && nums[i] > nums[s.top()]) {
            result[s.top()] = nums[i]; // Set the next greater element
            s.pop(); // Remove the index from the stack
        }
        s.push(i); // Push the current index onto the stack
    }

    return result; // Return the result array
}

int main() {
    std::vector<int> nums = {4, 5, 2, 10, 8};
    std::vector<int> result = nextGreaterElements(nums);

    std::cout << "Next greater elements: ";
    for (int num : result) {
        std::cout << num << " ";
    }
    std::cout << std::endl;

    return 0;
}
Example Explanation
Consider the array: [4, 5, 2, 10, 8].

Initialization:

Result array: [-1, -1, -1, -1, -1]
Stack: []
Iteration:

Element 4 (index 0):
Stack: [0]
Element 5 (index 1):
5 > 4, pop index 0, set result[0] = 5
Stack: [], push index 1: [1]
Element 2 (index 2):
Stack: [1, 2]
Element 10 (index 3):
10 > 2, pop index 2, set result[2] = 10
10 > 5, pop index 1, set result[1] = 10
Stack: [], push index 3: [3]
Element 8 (index 4):
8 < 10, push index 4: [3, 4]
Final Stack:

The stack contains indices 3 and 4, which means result[3] and result[4] remain -1.
Final Result:

The result array is [5, 10, 10, -1, -1].
Time Complexity
The time complexity of this algorithm is O(n), where ( n ) is the number of elements in the array. Each element is pushed and popped from the stack at most once.
Space Complexity
The space complexity is O(n) in the worst case, where all elements are stored in the stack if they are in decreasing order.
This approach efficiently finds the next greater element for each element in the array using a stack, ensuring that we only traverse the array once.

//26. Remove the n-th node from the end of a singly linked list. Write its algorithm, program. 
Find its time and space complexities. Explain with suitable example.

//26.Algorithm
Initialize Two Pointers:

Create two pointers, first and second, both initially pointing to the head of the linked list.
Advance the First Pointer:

Move the first pointer n steps ahead in the list. This way, the distance between the first and second pointers will be n.
Move Both Pointers:

Move both pointers (first and second) one step at a time until the first pointer reaches the end of the list. At this point, the second pointer will be pointing to the node just before the n-th node from the end.
Remove the Node:

Change the next pointer of the second pointer to skip the n-th node from the end.
Handle Edge Cases:

If n is equal to the length of the list, it means we need to remove the head node.
C++ Implementation
Here’s the implementation of the algorithm:

cpp

#include <iostream>

struct ListNode {
    int val;
    ListNode* next;
    ListNode(int x) : val(x), next(nullptr) {}
};

class Solution {
public:
    ListNode* removeNthFromEnd(ListNode* head, int n) {
        ListNode* dummy = new ListNode(0); // Create a dummy node
        dummy->next = head;
        ListNode* first = dummy;
        ListNode* second = dummy;

        // Move first pointer n+1 steps ahead
        for (int i = 0; i <= n; i++) {
            first = first->next;
        }

        // Move both pointers until first reaches the end
        while (first != nullptr) {
            first = first->next;
            second = second->next;
        }

        // Remove the n-th node from the end
        second->next = second->next->next;

        return dummy->next; // Return the new head
    }
};

void printList(ListNode* head) {
    while (head != nullptr) {
        std::cout << head->val << " -> ";
        head = head->next;
    }
    std::cout << "nullptr" << std::endl;
}

int main() {
    // Create a linked list: 1 -> 2 -> 3 -> 4 -> 5
    ListNode* head = new ListNode(1);
    head->next = new ListNode(2);
    head->next->next = new ListNode(3);
    head->next->next->next = new ListNode(4);
    head->next->next->next->next = new ListNode(5);

    int n = 2; // Remove the 2nd node from the end
    Solution solution;
    head = solution.removeNthFromEnd(head, n);

    std::cout << "Updated linked list: ";
    printList(head);

    return 0;
}
Example Explanation
Consider the linked list: 1 -> 2 -> 3 -> 4 -> 5 and we want to remove the 2nd node from the end.

Initialization:

Create a dummy node pointing to the head: dummy -> 1 -> 2 -> 3 -> 4 -> 5.
Advance the First Pointer:

Move the first pointer 3 steps ahead (n + 1 = 3): first points to the node with value 3.
Move Both Pointers:

Move both pointers until first reaches the end:
After 1 step: first points to 4, second points to 1.
After 2 steps: first points to 5, second points to 2.
After 3 steps: first points to nullptr, second points to 3.
Remove the Node:

The second pointer is now at the node with value 3, which is just before the node we want to remove (4).
Set second->next to second->next->next, effectively removing the node with value 4.
Final List:

The updated linked list is 1 -> 2 -> 3 -> 5.
Time Complexity
The time complexity of this algorithm is O(L), where ( L ) is the length of the linked list. We traverse the list a constant number of times.

//27. Find the node where two singly linked lists intersect.  Write its algorithm, program. 
Find its time and space complexities. Explain with suitable example

//27.Algorithm
Calculate Lengths:

First, calculate the lengths of both linked lists.
Align the Start Points:

Determine the difference in lengths between the two lists.
Move the pointer of the longer list ahead by the difference in lengths. This ensures that both pointers are equidistant from the intersection point.
Traverse Both Lists:

Move both pointers one step at a time until they meet. The node where they meet is the intersection point.
Return the Intersection Node:

If the pointers meet, return the intersection node. If they reach the end without meeting, return nullptr.
C++ Implementation
Here’s the implementation of the algorithm:

cpp
#include <iostream>

struct ListNode {
    int val;
    ListNode* next;
    ListNode(int x) : val(x), next(nullptr) {}
};

class Solution {
public:
    ListNode* getIntersectionNode(ListNode* headA, ListNode* headB) {
        if (!headA || !headB) return nullptr;

        // Calculate the lengths of both lists
        ListNode* currentA = headA;
        ListNode* currentB = headB;
        int lenA = 0, lenB = 0;

        while (currentA) {
            lenA++;
            currentA = currentA->next;
        }

        while (currentB) {
            lenB++;
            currentB = currentB->next;
        }

        // Align the start points
        currentA = headA;
        currentB = headB;

        if (lenA > lenB) {
            for (int i = 0; i < lenA - lenB; i++) {
                currentA = currentA->next;
            }
        } else {
            for (int i = 0; i < lenB - lenA; i++) {
                currentB = currentB->next;
            }
        }

        // Traverse both lists to find the intersection
        while (currentA && currentB) {
            if (currentA == currentB) {
                return currentA; // Intersection found
            }
            currentA = currentA->next;
            currentB = currentB->next;
        }

        return nullptr; // No intersection
    }
};

// Helper function to create a linked list from an array
ListNode* createLinkedList(int arr[], int size) {
    if (size == 0) return nullptr;
    ListNode* head = new ListNode(arr[0]);
    ListNode* current = head;
    for (int i = 1; i < size; i++) {
        current->next = new ListNode(arr[i]);
        current = current->next;
    }
    return head;
}

int main() {
    // Create two linked lists that intersect
    ListNode* listA = createLinkedList(new int[3]{4, 1, 8}, 3);
    ListNode* listB = createLinkedList(new int[2]{5, 0}, 2);
    listB->next->next = listA->next->next; // Create intersection at node with value 8

    Solution solution;
    ListNode* intersectionNode = solution.getIntersectionNode(listA, listB);

    if (intersectionNode) {
        std::cout << "The intersection node value is: " << intersectionNode->val << std::endl;
    } else {
        std::cout << "There is no intersection." << std::endl;
    }

    return 0;
}
Example Explanation
Consider the following two linked lists:

List A: 4 -> 1 -> 8 -> 4 -> 5
List B: 5 -> 0 -> 1 -> 8 -> 4 -> 5
Lengths:

Length of List A: 5
Length of List B: 6
Align the Start Points:

The difference in lengths is 1. Move the pointer of List B ahead by 1 node:
List A pointer starts at 4.
List B pointer starts at 0.
Traverse Both Lists:

Move both pointers:
List A: 4 → 1 → 8
List B: 0 → 1 → 8
When both pointers reach 8, they meet, indicating the intersection point.
Time Complexity
The time complexity of this algorithm is O(A + B), where ( A ) is the length of List A and ( B ) is the length of List B. We traverse both lists.

//28.Implement two stacks in a single array. Write its algorithm, program. Find its time and 
space complexities. Explain with suitable example. 

//28.Algorithm
Initialize the Array:

Create an array of a fixed size to hold the elements of both stacks.
Maintain two pointers: one for the top of the first stack (top1) starting at the beginning of the array, and another for the top of the second stack (top2) starting at the end of the array.
Push Operation:

For Stack 1, increment top1 and place the new element at that index.
For Stack 2, decrement top2 and place the new element at that index.
Pop Operation:

For Stack 1, return the element at top1 and decrement top1.
For Stack 2, return the element at top2 and increment top2.
Check for Overflow:

Before pushing an element, check if top1 is equal to top2. If they are equal, it means there is no space left to push a new element.
Check for Underflow:

Before popping an element, check if top1 is less than 0 (for Stack 1) or if top2 is greater than or equal to the size of the array (for Stack 2).
C++ Implementation
Here’s the implementation of the algorithm:

cpp

#include <iostream>
#include <stdexcept>

class TwoStacks {
private:
    int* arr;      // Array to hold the elements of both stacks
    int size;      // Size of the array
    int top1;      // Index for the top of Stack 1
    int top2;      // Index for the top of Stack 2

public:
    TwoStacks(int s) {
        size = s;
        arr = new int[size];
        top1 = -1;          // Stack 1 starts from the beginning
        top2 = size;       // Stack 2 starts from the end
    }

    // Push operation for Stack 1
    void push1(int x) {
        if (top1 + 1 == top2) {
            throw std::overflow_error("Stack Overflow: Unable to push to Stack 1");
        }
        arr[++top1] = x;
    }

    // Push operation for Stack 2
    void push2(int x) {
        if (top2 - 1 == top1) {
            throw std::overflow_error("Stack Overflow: Unable to push to Stack 2");
        }
        arr[--top2] = x;
    }

    // Pop operation for Stack 1
    int pop1() {
        if (top1 < 0) {
            throw std::underflow_error("Stack Underflow: Unable to pop from Stack 1");
        }
        return arr[top1--];
    }

    // Pop operation for Stack 2
    int pop2() {
        if (top2 >= size) {
            throw std::underflow_error("Stack Underflow: Unable to pop from Stack 2");
        }
        return arr[top2++];
    }

    // Destructor to free allocated memory
    ~TwoStacks() {
        delete[] arr;
    }
};

int main() {
    TwoStacks stacks(10); // Create two stacks with a total size of 10

    // Push elements onto Stack 1
    stacks.push1(1);
    stacks.push1(2);
    stacks.push1(3);

    // Push elements onto Stack 2
    stacks.push2(5);
    stacks.push2(6);
    stacks.push2(7);

    // Pop elements from Stack 1
    std::cout << "Popped from Stack 1: " << stacks.pop1() << std::endl; // 3
    std::cout << "Popped from Stack 1: " << stacks.pop1() << std::endl; // 2

    // Pop elements from Stack 2
    std::cout << "Popped from Stack 2: " << stacks.pop2() << std::endl; // 7
    std::cout << "Popped from Stack 2: " << stacks.pop2() << std::endl; // 6

    return 0;
}
Example Explanation
Initialization:
We create an instance of TwoStacks with a size of 10. The array is initialized to hold up to 10 elements.
top1 starts at -1 (indicating Stack 1 is empty), and top2 starts at 10

//29. Write a program to check if an integer is a palindrome without converting it to a string. 
Write its algorithm, program. Find its time and space complexities. Explain with 
suitable example.

//29.Algorithm
Handle Negative Numbers:

If the integer is negative, it cannot be a palindrome (e.g., -121 is not the same as 121-).
Extract Digits and Reverse:

Initialize a variable to store the reversed number.
Use a loop to extract the last digit of the number and build the reversed number.
In each iteration, divide the original number by 10 to remove the last digit.
Compare:

After the loop, compare the reversed number with the original number.
Return the Result:

If they are equal, return true (it is a palindrome); otherwise, return false.
C++ Implementation
Here’s the implementation of the algorithm:

cpp

#include <iostream>

class Solution {
public:
    bool isPalindrome(int x) {
        // Negative numbers are not palindromes
        if (x < 0) return false;

        int original = x;
        int reversed = 0;

        while (x > 0) {
            int digit = x % 10; // Get the last digit
            reversed = reversed * 10 + digit; // Build the reversed number
            x /= 10; // Remove the last digit from x
        }

        return original == reversed; // Compare original and reversed
    }
};

int main() {
    Solution solution;
    int number = 121; // Example number to check

    if (solution.isPalindrome(number)) {
        std::cout << number << " is a palindrome." << std::endl;
    } else {
        std::cout << number << " is not a palindrome." << std::endl;
    }

    return 0;
}
Example Explanation
Consider the integer 121:

Initial Check:

The number is not negative, so we proceed.
Reverse the Number:

Start with original = 121 and reversed = 0.
In the first iteration:
digit = 121 % 10 = 1
reversed = 0 * 10 + 1 = 1
x = 121 / 10 = 12
In the second iteration:
digit = 12 % 10 = 2
reversed = 1 * 10 + 2 = 12
x = 12 / 10 = 1
In the third iteration:
digit = 1 % 10 = 1
reversed = 12 * 10 + 1 = 121
x = 1 / 10 = 0
The loop ends as x is now 0.
Comparison:

Compare original (121) with reversed (121). They are equal, so 121 is a palindrome.
Time Complexity
The time complexity of this algorithm is O(log10(n)), where ( n ) is the input integer. This is because we are effectively dividing the number by 10 in each iteration, which reduces the number of digits.
Space Complexity
The space complexity is O(1), as we are using a constant amount of space for the variables original, reversed, and digit.
This approach efficiently checks if an integer is a palindrome without converting it to a string, using basic arithmetic operations.

//30. Explain the concept of linked lists and their applications in algorithm design.

//30.Concept of Linked Lists
A linked list is a linear data structure where elements, called nodes, are stored in a sequence. Unlike arrays, linked lists do not require contiguous memory allocation; instead, each node contains a reference (or pointer) to the next node in the sequence. This structure allows for efficient insertion and deletion of elements.

Structure of a Linked List Node
A typical node in a singly linked list contains:

Data: The value or information stored in the node.
Next Pointer: A reference to the next node in the list.
For a doubly linked list, each node contains:

Data: The value stored in the node.
Next Pointer: A reference to the next node.
Previous Pointer: A reference to the previous node.
Types of Linked Lists
Singly Linked List: Each node points to the next node, and the last node points to null.
Doubly Linked List: Each node points to both the next and the previous nodes.
Circular Linked List: The last node points back to the first node, forming a circle. This can be singly or doubly linked.
Advantages of Linked Lists
Dynamic Size: Linked lists can grow and shrink in size dynamically, unlike arrays, which have a fixed size.
Efficient Insertions/Deletions: Inserting or deleting nodes can be done in constant time ( O(1) ) if the pointer to the node is known, as it does not require shifting elements like in arrays.
Disadvantages of Linked Lists
Memory Overhead: Each node requires additional memory for storing pointers, which can lead to higher memory usage compared to arrays.
Sequential Access: Linked lists do not allow random access to elements, making it slower to access elements compared to arrays, which provide constant time access.
Applications of Linked Lists in Algorithm Design
Dynamic Memory Allocation: Linked lists are used in scenarios where the size of the data structure is not known in advance, such as in dynamic memory allocation.

Implementing Data Structures:

Stacks and Queues: Linked lists can be used to implement stacks and queues, allowing for efficient push and pop operations.
Graphs: Adjacency lists for representing graphs are often implemented using linked lists, where each node points to its adjacent nodes.
Polynomial Representation: Linked lists can be used to represent polynomials, where each node contains a coefficient and an exponent.

Undo Functionality: In applications like text editors, linked lists can be used to implement undo functionality, where each node represents a state of the document.

Sparse Matrices: Linked lists can efficiently represent sparse matrices, where most of the elements are zero, by only storing non-zero elements.

Memory Management: Linked lists are used in memory management systems, such as free lists, where free memory blocks are linked together for efficient allocation.

Example of a Singly Linked List
Here’s a simple example of a singly linked list in C++:

cpp

#include <iostream>

struct Node {
    int data;
    Node* next;
    Node(int val) : data(val), next(nullptr) {}
};

class LinkedList {
private:
    Node* head;

public:
    LinkedList() : head(nullptr) {}

    // Insert a new node at the end
    void insert(int val) {
        Node* newNode = new Node(val);
        if (!head) {
            head = newNode;
            return;
        }
        Node* temp = head;
        while (temp->next) {
            temp = temp->next;
        }
        temp->next = newNode;
    }

    // Display the linked list
    void display() {
        Node* temp = head;
        while (temp) {
            std::cout << temp->data << " -> ";
            temp = temp->next;
        }
        std::cout << "nullptr" << std::endl;
    }

    // Destructor to free memory
    ~LinkedList() {
        Node* current = head;
        Node* nextNode;
        while (current) {
            nextNode = current->next;
            delete current;
            current = nextNode;
        }
    }
};

int main() {
    LinkedList list;
    list.insert(1);
    list.insert(2);
    list.insert(3);
    list.display(); // Output: 1 -> 2 -> 3 -> nullptr

    return 0;
}
Conclusion
Linked lists are a fundamental data structure in computer science, providing flexibility and efficiency for various applications. Their dynamic nature and ability to efficiently handle insertions and deletions make them suitable for implementing complex data structures and algorithms. Understanding linked lists is essential for algorithm design and problem-solving in programming.

//31. Use a deque to find the maximum in every sliding window of size K. Write its 
algorithm, program. Find its time and space complexities. Explain with suitable 
example. 

//31.Algorithm
Initialize a Deque:

Create a deque to store indices of array elements.
Iterate Through the Array:

For each element in the array:
Remove indices from the front of the deque if they are out of the bounds of the current window.
Remove indices from the back of the deque while the current element is greater than the elements at those indices. This ensures that the deque remains in decreasing order.
Add the current index to the back of the deque.
If the current index is greater than or equal to ( K - 1 ), the maximum for the current window is at the front of the deque.
Store the Maximums:

Store the maximums in a result array.
C++ Implementation
Here’s the implementation of the algorithm:

cpp

#include <iostream>
#include <vector>
#include <deque>

class Solution {
public:
    std::vector<int> maxSlidingWindow(std::vector<int>& nums, int k) {
        std::vector<int> result;
        std::deque<int> dq; // Deque to store indices

        for (int i = 0; i < nums.size(); i++) {
            // Remove indices that are out of the current window
            if (!dq.empty() && dq.front() == i - k) {
                dq.pop_front();
            }

            // Remove indices from the back while the current element is greater
            while (!dq.empty() && nums[dq.back()] < nums[i]) {
                dq.pop_back();
            }

            // Add the current index to the deque
            dq.push_back(i);

            // If we have filled at least k elements, add the maximum to the result
            if (i >= k - 1) {
                result.push_back(nums[dq.front()]);
            }
        }

        return result;
    }
};

int main() {
    Solution solution;
    std::vector<int> nums = {1, 3, -1, -3, 5, 3, 6, 7};
    int k = 3;

    std::vector<int> maxInWindows = solution.maxSlidingWindow(nums, k);

    std::cout << "Maximums in each sliding window of size " << k << ": ";
    for (int max : maxInWindows) {
        std::cout << max << " ";
    }
    std::cout << std::endl;

    return 0;
}
Example Explanation
Consider the array: [1, 3, -1, -3, 5, 3, 6, 7] with a sliding window size of ( K = 3 ).

Initialization:

Start with an empty deque and an empty result vector.
Iterate Through the Array:

Index 0: Element 1
Deque: [0] (only index 0)
Index 1: Element 3
Remove index 0 from the back (since 1 < 3).
Deque: [1] (only index 1)
Index 2: Element -1
Deque: [1, 2] (indices 1 and 2)
Result: [3] (maximum of the first window)
Index 3: Element -3
Deque: [1, 2, 3] (indices 1, 2, and 3)
Result: [3, 3] (maximum of the second window)
Index 4: Element 5
Remove indices 2 and 3 from the back (since -1 < 5 and -3 < 5).
Deque: [4] (only index 4)
Result: [3, 3, 5] (maximum of the third window)
Index 5: Element 3
Deque: [4, 5] (indices 4 and 5)
Result: [3, 3, 5, 5] (maximum of the fourth window)
Index 6: Element 6
Remove index 5 from the back (since 3 < 6).
Deque: [6] (only index 6)
Result: `[3, 3,].

//32.How to find the largest rectangle that can be formed in a histogram. Write its algorithm, 
program. Find its time and space complexities. Explain with suitable example. 

//32.Algorithm
Initialize a Stack:

Use a stack to keep track of the indices of the histogram bars.
Iterate Through the Histogram:

For each bar in the histogram:
While the stack is not empty and the current bar is shorter than the bar at the index stored at the top of the stack:
Pop the index from the stack.
Calculate the height of the rectangle using the height of the popped bar.
Determine the width of the rectangle:
If the stack is empty, the width is the current index.
If the stack is not empty, the width is the difference between the current index and the index of the new top of the stack minus one.
Calculate the area and update the maximum area if necessary.
Push the current index onto the stack.
Handle Remaining Bars in the Stack:

After iterating through the histogram, there may still be indices in the stack. Pop each index and calculate the area as described above.
Return the Maximum Area.

C++ Implementation
Here’s the implementation of the algorithm:

cpp

#include <iostream>
#include <vector>
#include <stack>

class Solution {
public:
    int largestRectangleArea(std::vector<int>& heights) {
        std::stack<int> s; // Stack to store indices
        int maxArea = 0;
        int n = heights.size();

        for (int i = 0; i < n; i++) {
            // While the current bar is shorter than the bar at the index stored at the top of the stack
            while (!s.empty() && heights[i] < heights[s.top()]) {
                int height = heights[s.top()];
                s.pop();
                int width = s.empty() ? i : i - s.top() - 1; // Calculate width
                maxArea = std::max(maxArea, height * width); // Update max area
            }
            s.push(i); // Push current index onto the stack
        }

        // Handle remaining bars in the stack
        while (!s.empty()) {
            int height = heights[s.top()];
            s.pop();
            int width = s.empty() ? n : n - s.top() - 1; // Calculate width
            maxArea = std::max(maxArea, height * width); // Update max area
        }

        return maxArea;
    }
};

int main() {
    Solution solution;
    std::vector<int> heights = {2, 1, 5, 6, 2, 3};

    int maxArea = solution.largestRectangleArea(heights);
    std::cout << "The largest rectangle area in the histogram is: " << maxArea << std::endl;

    return 0;
}
Example Explanation
Consider the histogram represented by the heights: [2, 1, 5, 6, 2, 3].

Initialization:

Start with an empty stack and maxArea = 0.
Iterate Through the Heights:

Index 0: Height 2
Stack: [0]
Index 1: Height 1
Pop index 0 (height 2).
Width = 1 (current index 1 - stack is empty).
Area = 2 * 1 = 2. Update maxArea = 2.
Stack: [1]
Index 2: Height 5
Stack: [1, 2]
Index 3: Height 6
Stack: [1, 2, 3]
Index 4: Height 2
Pop index 3 (height 6).
Width = 3 - 1 - 1 = 1.
Area = 6 * 1 = 6. Update maxArea = 6.
Pop index 2 (height 5).
Width = 3 - 1 - 1 = 1.
Area = 5 * 1 = 5. maxArea remains 6.
Stack: [1, 4]
Index 5: Height 3
Stack: [1, 4, 5]
Handle Remaining Bars in the Stack:

Pop index 5 (height 3).
Width = 6 - 4 - 1 = 1.

//33.Explain the sliding window technique and its applications in array problems

//33.Concept of Sliding Window Technique
Window Definition: The window can be defined by two pointers (or indices) that represent the start and end of the current subarray or subsequence. The window can be adjusted by moving these pointers based on certain conditions.

Expanding and Contracting:

Expand: Move the end pointer to include more elements in the window.
Contract: Move the start pointer to exclude elements from the window.
Conditions: The window is adjusted based on specific conditions related to the problem, such as the sum of elements, the number of unique elements, or other criteria.

Applications of Sliding Window Technique
The sliding window technique is widely used in various types of problems, including:

Finding Maximum/Minimum in Subarrays:

Problems that require finding the maximum or minimum value in every contiguous subarray of size ( K ).
Subarray Sum Problems:

Finding the smallest subarray with a sum greater than or equal to a given value.
Finding the longest subarray with a sum equal to a target value.
Longest Substring Problems:

Finding the longest substring without repeating characters.
Finding the longest substring with at most ( K ) distinct characters.
Count of Anagrams:

Counting occurrences of anagrams of a string within another string.
Sliding Window Maximum:

Finding the maximum value in every sliding window of size ( K ) in an array.
Example Problems
Maximum Sum of Subarray of Size K:

Given an array and a number ( K ), find the maximum sum of any contiguous subarray of size ( K ).
Algorithm:

Initialize the sum of the first ( K ) elements.
Slide the window by subtracting the element that is left behind and adding the next element in the array.
Longest Substring Without Repeating Characters:

Given a string, find the length of the longest substring without repeating characters.
Algorithm:

Use a hash set to track characters in the current window.
Expand the window by moving the end pointer and contract the window by moving the start pointer when a duplicate character is found.
Example Code: Maximum Sum of Subarray of Size K
Here’s a simple implementation of the maximum sum of a subarray of size ( K ) using the sliding window technique:

cpp

#include <iostream>
#include <vector>

class Solution {
public:
    int maxSumSubarray(std::vector<int>& nums, int k) {
        int maxSum = 0;
        int windowSum = 0;

        // Calculate the sum of the first window
        for (int i = 0; i < k; i++) {
            windowSum += nums[i];
        }
        maxSum = windowSum;

        // Slide the window
        for (int i = k; i < nums.size(); i++) {
            windowSum += nums[i] - nums[i - k]; // Add the next element and remove the first element of the previous window
            maxSum = std::max(maxSum, windowSum); // Update maxSum if needed
        }

        return maxSum;
    }
};

int main() {
    Solution solution;
    std::vector<int> nums = {2, 1, 5, 1, 3, 2};
    int k = 3;

    int maxSum = solution.maxSumSubarray(nums, k);
    std::cout << "Maximum sum of subarray of size " << k << " is: " << maxSum << std::endl;

    return 0;
}
Conclusion
The sliding window technique is a versatile and efficient approach for solving a variety of problems involving arrays and strings. By maintaining a dynamic window that adjusts based on specific conditions, it allows for optimal solutions that avoid the inefficiencies of nested loops. Understanding and applying this technique can significantly enhance problem-solving skills in algorithm design.

//34. Solve the problem of finding the subarray sum equal to K using hashing. Write its 
algorithm, program. Find its time and space complexities. Explain with suitable 
example. 

//34.Algorithm
Initialize Variables:

Create a hash map to store the cumulative sums and their frequencies.
Initialize a variable to keep track of the cumulative sum and a counter for the number of subarrays that sum to ( K ).
Iterate Through the Array:

For each element in the array:
Update the cumulative sum by adding the current element.
Check if the cumulative sum equals ( K ). If it does, increment the counter.
Check if there exists a cumulative sum that, when subtracted from the current cumulative sum, equals ( K ). This can be done by checking if cumulative_sum - K exists in the hash map. If it does, add its frequency to the counter.
Update the hash map with the current cumulative sum, incrementing its frequency.
Return the Counter:

After iterating through the array, return the counter, which represents the number of subarrays that sum to ( K ).
C++ Implementation
Here’s the implementation of the algorithm:

cpp

#include <iostream>
#include <vector>
#include <unordered_map>

class Solution {
public:
    int subarraySum(std::vector<int>& nums, int k) {
        std::unordered_map<int, int> cumulativeSumCount;
        int cumulativeSum = 0;
        int count = 0;

        // Initialize the map with the cumulative sum of 0
        cumulativeSumCount[0] = 1;

        for (int num : nums) {
            cumulativeSum += num; // Update the cumulative sum

            // Check if there is a subarray (ending at the current index) that sums to k
            if (cumulativeSumCount.find(cumulativeSum - k) != cumulativeSumCount.end()) {
                count += cumulativeSumCount[cumulativeSum - k]; // Add the frequency of (cumulativeSum - k)
            }

            // Update the frequency of the current cumulative sum
            cumulativeSumCount[cumulativeSum]++;
        }

        return count; // Return the total count of subarrays that sum to k
    }
};

int main() {
    Solution solution;
    std::vector<int> nums = {1, 1, 1};
    int k = 2;

    int count = solution.subarraySum(nums, k);
    std::cout << "Number of subarrays that sum to " << k << " is: " << count << std::endl;

    return 0;
}
Example Explanation
Consider the array: [1, 1, 1] and ( K = 2 ).

Initialization:

Cumulative sum = 0
Count = 0
Hash map: {0: 1} (to account for subarrays that sum to ( K ) starting from index 0)
Iterate Through the Array:

Index 0: Element 1

Cumulative sum = 0 + 1 = 1
Check if 1 - 2 = -1 exists in the hash map (it does not).
Update the hash map: {0: 1, 1: 1}
Index 1: Element 1

Cumulative sum = 1 + 1 = 2
Check if 2 - 2 = 0 exists in the hash map (it does, with frequency 1).
Increment count by 1 (count = 1).
Update the hash map: {0: 1, 1: 1, 2: 1}
Index 2: Element 1

Cumulative sum = 2 + 1 = 3
Check if 3 - 2 = 1 exists in the hash map (it does, with frequency 1).
Increment count by 1 (count = 2).
Update the hash map: {0: 1, 1: 1, 2: 1, 3: 1}
Final Count:

The total number of subarrays that sum to ( K = 2 ) is 2. The subarrays are:
[1, 1] (from index 0 to 1)
[1, 1] (from index 1 to 2)
Time Complexity
The time complexity of this algorithm is ( O(n) ).




