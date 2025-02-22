
---

### **1. Two Sum**

```go
func findTwoSum(nums []int, target int) []int {
    valueIndexMap := make(map[int]int)
    for index, value := range nums {
        complement := target - value
        if complementIndex, exists := valueIndexMap[complement]; exists {
            return []int{complementIndex, index}
        }
        valueIndexMap[value] = index
    }
    return nil
}
```

---

### **2. Best Time to Buy and Sell Stock**

```go
func maxProfitFromStock(prices []int) int {
    minPrice := int(^uint(0) >> 1) // Maximum int value
    maxProfit := 0
    for _, currentPrice := range prices {
        if currentPrice < minPrice {
            minPrice = currentPrice
        } else if currentPrice-minPrice > maxProfit {
            maxProfit = currentPrice - minPrice
        }
    }
    return maxProfit
}
```

---

### **3. Contains Duplicate**

```go
func hasDuplicate(nums []int) bool {
    seenNumbers := make(map[int]struct{})
    for _, number := range nums {
        if _, exists := seenNumbers[number]; exists {
            return true
        }
        seenNumbers[number] = struct{}{}
    }
    return false
}
```

---

### **4. Product of Array Except Self**

```go
func calculateProductExceptSelf(nums []int) []int {
    length := len(nums)
    result := make([]int, length)
    
    leftProduct := 1
    for i := 0; i < length; i++ {
        result[i] = leftProduct
        leftProduct *= nums[i]
    }
    
    rightProduct := 1
    for i := length - 1; i >= 0; i-- {
        result[i] *= rightProduct
        rightProduct *= nums[i]
    }
    
    return result
}
```

---

### **5. Maximum Subarray**

```go
func findMaxSubArray(nums []int) int {
    currentSum := nums[0]
    maxSum := nums[0]
    for i := 1; i < len(nums); i++ {
        currentSum = max(nums[i], currentSum+nums[i])
        maxSum = max(maxSum, currentSum)
    }
    return maxSum
}

func max(a, b int) int {
    if a > b {
        return a
    }
    return b
}
```

---

### **6. Maximum Product Subarray**

```go
func findMaxProductSubArray(nums []int) int {
    maxProduct := nums[0]
    minProduct := nums[0]
    globalMaxProduct := nums[0]
    for i := 1; i < len(nums); i++ {
        current := nums[i]
        if current < 0 {
            maxProduct, minProduct = minProduct, maxProduct
        }
        maxProduct = max(current, maxProduct*current)
        minProduct = min(current, minProduct*current)
        globalMaxProduct = max(globalMaxProduct, maxProduct)
    }
    return globalMaxProduct
}

func min(a, b int) int {
    if a < b {
        return a
    }
    return b
}
```

---

### **7. Find Minimum in Rotated Sorted Array**

```go
func findMinimumInRotatedArray(nums []int) int {
    left, right := 0, len(nums)-1
    for left < right {
        mid := left + (right-left)/2
        if nums[mid] > nums[right] {
            left = mid + 1
        } else {
            right = mid
        }
    }
    return nums[left]
}
```

---

### **8. Search in Rotated Sorted Array**

```go
func searchInRotatedArray(nums []int, target int) int {
    left, right := 0, len(nums)-1
    for left <= right {
        mid := left + (right-left)/2
        if nums[mid] == target {
            return mid
        }
        if nums[left] <= nums[mid] {
            if target >= nums[left] && target < nums[mid] {
                right = mid - 1
            } else {
                left = mid + 1
            }
        } else {
            if target > nums[mid] && target <= nums[right] {
                left = mid + 1
            } else {
                right = mid - 1
            }
        }
    }
    return -1
}
```

---

### **9. 3 Sum**

```go
func findThreeSum(nums []int) [][]int {
    sort.Ints(nums)
    result := [][]int{}
    for i := 0; i < len(nums)-2; i++ {
        if i > 0 && nums[i] == nums[i-1] {
            continue
        }
        left, right := i+1, len(nums)-1
        for left < right {
            sum := nums[i] + nums[left] + nums[right]
            if sum == 0 {
                result = append(result, []int{nums[i], nums[left], nums[right]})
                left++
                right--
                for left < right && nums[left] == nums[left-1] {
                    left++
                }
                for left < right && nums[right] == nums[right+1] {
                    right--
                }
            } else if sum < 0 {
                left++
            } else {
                right--
            }
        }
    }
    return result
}
```

---

### **10. Container With Most Water**

```go
func calculateMaxWaterContainer(heights []int) int {
    left, right := 0, len(heights)-1
    maxWater := 0
    for left < right {
        currentHeight := min(heights[left], heights[right])
        maxWater = max(maxWater, currentHeight*(right-left))
        if heights[left] < heights[right] {
            left++
        } else {
            right--
        }
    }
    return maxWater
}
```

---
