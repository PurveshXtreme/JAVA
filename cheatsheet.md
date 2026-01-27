## 🔹 Java Array — Cheatsheet (Operations & Syntax)

| Function / Operation | Short Syntax |
|--------------------|-------------|
| Declare array | ``` int[] arr = new int[5]; ``` |
| Initialize array | ``` int[] arr = {1, 2, 3}; ``` |
| Access element | ``` arr[i] ``` |
| Get array size | ``` arr.length ``` |
| Iterate over array | ``` for(int x : arr)``` or ``` for(int i=0;i<arr.length;i++)``` |
| Sort array | ``` Arrays.sort(arr); ``` |
| Reverse array | ``` Collections.reverse(Arrays.asList(arr)); ``` *(for Integer[])* |
| Find max element | ``` Arrays.stream(arr).max().getAsInt(); ``` |
| Find min element | ``` Arrays.stream(arr).min().getAsInt(); ``` |
| Sum of elements | ``` Arrays.stream(arr).sum(); ``` |
| Binary search | ``` Arrays.binarySearch(arr, val); ``` |
| Copy array | ``` Arrays.copyOf(arr, n); ``` |
| Compare arrays | ``` Arrays.equals(a, b); ``` |
| Fill with value | ``` Arrays.fill(arr, val); ``` |
| Convert to string | ``` Arrays.toString(arr); ``` |

---

## 🔹 Java ArrayList — Cheatsheet (Operations & Syntax)

| Function / Operation | Short Syntax |
|--------------------|-------------|
| Declare ArrayList | ``` ArrayList<Integer> v = new ArrayList<>(); ``` |
| Initialize ArrayList | ``` ArrayList<Integer> v = new ArrayList<>(List.of(1,2,3)); ``` |
| Size of ArrayList | ``` v.size() ``` |
| Access element | ``` v.get(i) ``` |
| Modify element | ``` v.set(i, x) ``` |
| Add element at end | ``` v.add(x); ``` |
| Remove last element | ``` v.remove(v.size()-1); ``` |
| Insert at position | ``` v.add(i, x); ``` |
| Erase at position | ``` v.remove(i); ``` |
| Erase range | ``` v.subList(i, j).clear(); ``` |
| Clear all elements | ``` v.clear(); ``` |
| Check if empty | ``` v.isEmpty(); ``` |
| Sort ArrayList | ``` Collections.sort(v); ``` |
| Reverse ArrayList | ``` Collections.reverse(v); ``` |
| Find max element | ``` Collections.max(v); ``` |
| Find min element | ``` Collections.min(v); ``` |
| Sum of elements | ``` v.stream().mapToInt(i->i).sum(); ``` |
| Binary search | ``` Collections.binarySearch(v, val); ``` |
| Lower bound (approx) | ``` Collections.binarySearch(v, val) ``` |
| Count occurrences | ``` Collections.frequency(v, val); ``` |
| Fill with value | ``` Collections.fill(v, val); ``` |
| Resize ArrayList | ``` v.subList(n, v.size()).clear(); ``` |
| Iterate (for-each) | ``` for(int x : v) ``` |
| Swap elements | ``` Collections.swap(v, i, j); ``` |

---
---

## 🔹 Scanner — Cheatsheet (Input Operations & Syntax)

| Function / Operation | Short Syntax |
|--------------------|-------------|
| Import Scanner | ``` import java.util.Scanner; ``` |
| Create Scanner object | ``` Scanner sc = new Scanner(System.in); ``` |
| Read integer | ``` sc.nextInt(); ``` |
| Read long | ``` sc.nextLong(); ``` |
| Read float | ``` sc.nextFloat(); ``` |
| Read double | ``` sc.nextDouble(); ``` |
| Read boolean | ``` sc.nextBoolean(); ``` |
| Read single word | ``` sc.next(); ``` |
| Read full line | ``` sc.nextLine(); ``` |
| Read character | ``` sc.next().charAt(0); ``` |
| Check next int | ``` sc.hasNextInt(); ``` |
| Check next token | ``` sc.hasNext(); ``` |
| Skip token | ``` sc.skip(pattern); ``` |
| Set delimiter | ``` sc.useDelimiter(","); ``` |
| Close Scanner | ``` sc.close(); ``` |
| Read until end | ``` while(sc.hasNext()) ``` |
| Handle mixed input | ``` sc.nextLine(); // clear buffer ``` |

---
