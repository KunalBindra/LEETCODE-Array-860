# LEETCODE-Array-860
Let’s dry run the `lemonadeChange` method in the `Solution` class using a few example inputs to understand how it works. This method is designed to determine whether a vendor can provide change for each customer given their bills.

### Understanding the Logic
1. **Initial Counts**:
   - `count5`: Tracks the number of $5 bills.
   - `count10`: Tracks the number of $10 bills.

2. **Customer Transactions**:
   - If a customer pays with a $5 bill, we simply increment `count5`.
   - If they pay with a $10 bill, we need to provide $5 change, so we decrement `count5` and increment `count10`.
   - If they pay with a $20 bill, we prefer to give one $10 and one $5 bill if possible. If not, we attempt to give three $5 bills.

3. **Failure Condition**:
   - If at any point `count5` becomes negative, it means we cannot provide the necessary change, and the method returns `false`.

### Example Dry Run
Let's dry run the function with the following input:
```java
int[] bills = {5, 5, 5, 10, 20};
```

#### Step-by-step Execution
1. **Input**: `{5, 5, 5, 10, 20}`
   - `count5 = 0`
   - `count10 = 0`
   
2. **Processing `5`**:
   - `bill = 5`
   - Action: `++count5` → `count5 = 1`
   - State: `count5 = 1`, `count10 = 0`

3. **Processing `5`**:
   - `bill = 5`
   - Action: `++count5` → `count5 = 2`
   - State: `count5 = 2`, `count10 = 0`

4. **Processing `5`**:
   - `bill = 5`
   - Action: `++count5` → `count5 = 3`
   - State: `count5 = 3`, `count10 = 0`

5. **Processing `10`**:
   - `bill = 10`
   - Action: `--count5` (need to give $5 change) and `++count10`
   - New values: `count5 = 2`, `count10 = 1`
   - State: `count5 = 2`, `count10 = 1`

6. **Processing `20`**:
   - `bill = 20`
   - Action: Since `count10 > 0`, we give one $10 and one $5.
   - `--count10` and `--count5` → `count10 = 0`, `count5 = 1`
   - State: `count5 = 1`, `count10 = 0`

### Final State
- After processing all bills, we have:
  - `count5 = 1`
  - `count10 = 0`
- Since `count5` is not negative at any point, we can return `true`.

### Additional Test Cases
Let’s consider another case:
```java
int[] bills = {5, 5, 10, 10, 20};
```
#### Dry Run
1. **Input**: `{5, 5, 10, 10, 20}`
   - Start: `count5 = 0`, `count10 = 0`
2. **Processing `5`**: `count5 = 1`
3. **Processing `5`**: `count5 = 2`
4. **Processing `10`**: `count5 = 1`, `count10 = 1`
5. **Processing `10`**: `count5 = 0`, `count10 = 2`
6. **Processing `20`**: `count10 > 0`, give change → `count5 = -1`, `count10 = 1` (fails)

### Result
- For this input, the method would return `false`.

### Conclusion
The `lemonadeChange` method is efficient and works correctly to determine if the vendor can give change for each customer based on the bills provided. It correctly tracks the number of $5 and $10 bills and ensures that sufficient change is available when required.
