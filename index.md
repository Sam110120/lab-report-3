## The buggy code from week 4's lab:

```
  static void reverseInPlace(int[] arr) {
      for(int i = 0; i < arr.length; i += 1) {
        arr[i] = arr[arr.length - i - 1];
      }
    }
```

**A failure-inducing input for the buggy program, as a JUnit test and any associated code:**
```
  @Test
  public void test1(){
    int[] input = {1,2,3,4,5,6};
    int[] output = {6,5,4,3,2,1};
    ArrayExamples.reverseInPlace(input);
    assertArrayEquals(output, input);
  }
```

**An input that doesn’t induce a failure, as a JUnit test and any associated code:**
```
  @Test
  public void testReverseInPlace() {
    int[] input1 = {2};
    ArrayExamples.reverseInPlace(input1);
    assertArrayEquals(new int[]{2}, input1);
  }
```

**The symptom, as the output of running the tests**
<img width="766" alt="image" src="https://github.com/Sam110120/lab-report-3/assets/71369089/cdd73e45-2d29-4c0c-85a3-39d2b9f9ba6e">

**The bug, as the before-and-after code change required to fix it:**
```
static void reverseInPlace(int[] arr) {
    for(int i = 0; i < arr.length/2; i += 1) {
      int temp = arr[i];
      arr[i] = arr[arr.length - i - 1];
      arr[arr.length - i - 1] = temp;
    }
  }
```

**Briefly describe why the fix addresses the issue.**
Before the code is fixed...
