It is not default quicksort algorithm.
The pivot resorted in this sort algorithm and so it is inefficient.

```solidity
        if (lastUnsortedInd > left) {
            sort(arr, left, lastUnsortedInd - 1);
        }
        sort(arr, lastUnsortedInd, right);
```

Please correct it as follows to avoid resorting.
https://github.com/code-423n4/2024-07-karak/blob/main/src/utils/CommonUtils.sol#L23-L26

```diff
        if (lastUnsortedInd > left) {
            sort(arr, left, lastUnsortedInd - 1);
        }
-        sort(arr, lastUnsortedInd, right);
+        sort(arr, lastUnsortedInd + 1, right);
```

