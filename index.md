# Part 1 - Bugs

**The buggy code from week 4's lab:**

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

**The symptom, as the output of running the tests:**
<img width="766" alt="image" src="https://github.com/Sam110120/lab-report-3/assets/71369089/cdd73e45-2d29-4c0c-85a3-39d2b9f9ba6e">

**The bug, as the before-and-after code change required to fix it:**

* The code before change:
```
  static void reverseInPlace(int[] arr) {
      for(int i = 0; i < arr.length; i += 1) {
        arr[i] = arr[arr.length - i - 1];
      }
    }
```

* The code after change:
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

Before the code is fixed, the function reversInPlace would only reverse half of the ArrayList because it will for loop all the elements in the ArrayList. It will only change the first half elements and the second half will just be the same as the original ArrayList since we have overwritten the first half. So if I have an ArrayList with element {1,2,3,4}, the result of running the function would be {4,3,3,4}. The fixed code addresses the issue by making the number of for loop in half and creating a temporary variable that will hold the element that will be switched. So each element in the first half will be replaced by the second part from the end, and each element in the second part will be replaced by the variable that holds the element from the first part.

# Part 2 - Researching Commands (find)

By asking Chatgpt the prompt: "For the command-line "find", give 4 alternate ways to use the command and write a sentence or two about what it's doing and why it's useful."

**The output from Chatgpt with my own words:**

* Basic File Search:

```
  find /path/to/search -name "filename"
```

**Two examples of input/output:**

```
  zijieqiu@Zijies-MacBook-Pro docsearch % find technical/911report -name "chapter-1.txt"
  technical/911report/chapter-1.txt
  zijieqiu@Zijies-MacBook-Pro docsearch % find technical/911report -name "*.txt"        
  technical/911report/chapter-13.4.txt
  technical/911report/chapter-13.5.txt
  ...
  technical/911report/chapter-12.txt
  technical/911report/chapter-10.txt
  technical/911report/chapter-11.txt
```
* The code from the example above is taken directly from the week 5 lab.
  * [Github Link](https://github.com/ucsd-cse15l-s23/docsearch)

**This command searches for a specific file named "filename" within the directory specified by /path/to/search and its subdirectories. It's useful for quickly locating a particular file when you know its name.**

* Searching for Files/Directories:
  
```
  find /path/to/search -type f -name "*.txt"
```

**Two examples of input/output:**

```
  zijieqiu@Zijies-MacBook-Pro docsearch % find technical/911report -type f -name "*.txt"
  technical/911report/chapter-13.4.txt
  technical/911report/chapter-13.5.txt
  technical/911report/chapter-13.1.txt
  technical/911report/chapter-13.2.txt
  technical/911report/chapter-13.3.txt
  ...
  technical/911report/preface.txt
  technical/911report/chapter-12.txt
  technical/911report/chapter-10.txt
  technical/911report/chapter-11.txt
  zijieqiu@Zijies-MacBook-Pro docsearch % find technical/ -type d -name "biomed"
  technical//biomed
```
* The code from the example above is taken directly from the week 5 lab.
  * [Github Link](https://github.com/ucsd-cse15l-s23/docsearch)

**This command searches for files with the ".txt" extension within the specified directory and its
  subdirectories. It's helpful for locating files by their extension, which can be useful for filtering
  and processing specific file types. It could also be used to find the directories.**

* Searching for Files by Modification Time (mtime):

```
  find /path/to/search -mtime -7
```

**Two examples of input/output:**

```
  zijieqiu@Zijies-MacBook-Pro Cse 15L % find docsearch -mtime -1
  docsearch
  docsearch/new_file.txt
  zijieqiu@Zijies-MacBook-Pro Cse 15L % find docsearch -mtime -6
  ...
  docsearch/technical/911report/chapter-5.txt
  docsearch/technical/911report/chapter-6.txt
  docsearch/technical/911report/chapter-7.txt
  docsearch/technical/911report/chapter-9.txt
  docsearch/technical/911report/chapter-8.txt
  docsearch/technical/911report/preface.txt
  docsearch/technical/911report/chapter-12.txt
  docsearch/technical/911report/chapter-10.txt
  docsearch/technical/911report/chapter-11.txt
```
* The code from the example above is taken directly from the week 5 lab.
  * [Github Link](https://github.com/ucsd-cse15l-s23/docsearch)

**The -mtime option is useful when you want to search for files that have been modified within a specific timeframe.
  This can be helpful for tasks like locating recently edited files for backup or cleanup purposes.**

* Searching for Files by Size (size):


```
  find /path/to/search -size +10M
```

**Two examples of input/output:**

```
  zijieqiu@Zijies-MacBook-Pro Cse 15L % find docsearch/technical/911report -size +0M
  docsearch/technical/911report
  docsearch/technical/911report/chapter-13.4.txt
  docsearch/technical/911report/chapter-13.5.txt
  docsearch/technical/911report/chapter-13.1.txt
  ...
  docsearch/technical/911report/preface.txt
  docsearch/technical/911report/chapter-12.txt
  docsearch/technical/911report/chapter-10.txt
  docsearch/technical/911report/chapter-11.txt
  zijieqiu@Zijies-MacBook-Pro Cse 15L % find docsearch/technical -size +0M
  docsearch/technical/biomed/gb-2002-3-5-research0023.txt
  docsearch/technical/biomed/1472-6793-2-18.txt
  docsearch/technical/biomed/1471-2156-2-17.txt
  docsearch/technical/biomed/1471-2369-4-1.txt
  ...
  docsearch/technical/911report/chapter-8.txt
  docsearch/technical/911report/preface.txt
  docsearch/technical/911report/chapter-12.txt
  docsearch/technical/911report/chapter-10.txt
  docsearch/technical/911report/chapter-11.txt
```
* The code from the example above is taken directly from the week 5 lab.
  * [Github Link](https://github.com/ucsd-cse15l-s23/docsearch)

**The -size option is valuable for finding files of a particular size, which is useful for managing disk space,
  especially when you need to identify and potentially remove large or small files that are consuming space.**
