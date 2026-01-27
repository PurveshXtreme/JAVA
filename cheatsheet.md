## 🔹 Java Array — Cheatsheet (Operations & Syntax)

| Function / Operation | Short Syntax (Java) |
|--------------------|--------------------|
| Declare array | ```java int[] arr = new int[5]; ``` |
| Initialize array | ```java int[] arr = {1, 2, 3}; ``` |
| Access element | ```java arr[i] ``` |
| Get array size | ```java arr.length ``` |
| Iterate over array | ```java for(int x : arr)``` or ```java for(int i=0;i<arr.length;i++)``` |
| Sort array | ```java Arrays.sort(arr); ``` |
| Reverse array | ```java Collections.reverse(Arrays.asList(arr)); ``` *(for Integer[])* |
| Find max element | ```java Arrays.stream(arr).max().getAsInt(); ``` |
| Find min element | ```java Arrays.stream(arr).min().getAsInt(); ``` |
| Sum of elements | ```java Arrays.stream(arr).sum(); ``` |
| Binary search | ```java Arrays.binarySearch(arr, val); ``` |
| Copy array | ```java Arrays.copyOf(arr, n); ``` |
| Compare arrays | ```java Arrays.equals(a, b); ``` |
| Fill with value | ```java Arrays.fill(arr, val); ``` |
| Convert to string | ```java Arrays.toString(arr); ``` |

---

## 🔹 Java ArrayList — Cheatsheet (Operations & Syntax)

| Function / Operation | Short Syntax (Java) |
|--------------------|--------------------|
| Declare ArrayList | ```java ArrayList<Integer> v = new ArrayList<>(); ``` |
| Initialize ArrayList | ```java ArrayList<Integer> v = new ArrayList<>(List.of(1,2,3)); ``` |
| Size of ArrayList | ```java v.size() ``` |
| Access element | ```java v.get(i) ``` |
| Modify element | ```java v.set(i, x) ``` |
| Add element at end | ```java v.add(x); ``` |
| Remove last element | ```java v.remove(v.size()-1); ``` |
| Insert at position | ```java v.add(i, x); ``` |
| Erase at position | ```java v.remove(i); ``` |
| Erase range | ```java v.subList(i, j).clear(); ``` |
| Clear all elements | ```java v.clear(); ``` |
| Check if empty | ```java v.isEmpty(); ``` |
| Sort ArrayList | ```java Collections.sort(v); ``` |
| Reverse ArrayList | ```java Collections.reverse(v); ``` |
| Find max element | ```java Collections.max(v); ``` |
| Find min element | ```java Collections.min(v); ``` |
| Sum of elements | ```java v.stream().mapToInt(i->i).sum(); ``` |
| Binary search | ```java Collections.binarySearch(v, val); ``` |
| Lower bound (approx) | ```java Collections.binarySearch(v, val) ``` |
| Count occurrences | ```java Collections.frequency(v, val); ``` |
| Fill with value | ```java Collections.fill(v, val); ``` |
| Resize ArrayList | ```java v.subList(n, v.size()).clear(); ``` |
| Iterate (for-each) | ```java for(int x : v) ``` |
| Swap elements | ```java Collections.swap(v, i, j); ``` |
