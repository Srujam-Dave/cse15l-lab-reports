# Lab Report 3

### Part 1: Testing ArrayExamples.Reversed()
- Failure Inducing Test:
```
@Test
public void testReservedNotEmpty() {
  int[] input1 = {1, 2, 3, 4};
  int[] output1 = ArrayExamples.reversed(input1);
  assertArrayEquals(new int[]{4, 3, 2, 1}, output1);
  assertFalse(output1 == input1);
}
```
This test checks both if the output array is reversed properly, and if the output array is different from the input array (since reversed() is not meant to act on the input array). The
program fails on the first test. 

- Test that doesn't fail: 
```
@Test
public void testReservedZero() {
  int[] input1 = {0};
  int[] output1 = ArrayExamples.reversed(input1);
  assertArrayEquals(new int[]{0}, output1);
}
```
- Failed Test Symptoms:

```
ArrayTests.java:27: error: method testReservedNotEmpty() is already defined in class ArrayTests
  public void testReservedNotEmpty() {
              ^
1 error
PS C:\Users\sruja\OneDrive\Documents\GitHub\lab3> java -cp ".;lib/junit-4.13.2.jar;lib/hamcrest-core-1.3.jar"
org.junit.runner.JUnitCore ArrayTests
JUnit version 4.13.2
..E.
Time: 0.028
There was 1 failure:
1) testReservedNotEmpty(ArrayTests)
arrays first differed at element [0]; expected:<4> but was:<0>
        at org.junit.internal.ComparisonCriteria.arrayEquals(ComparisonCriteria.java:78)
        at org.junit.internal.ComparisonCriteria.arrayEquals(ComparisonCriteria.java:28)
        at org.junit.Assert.internalArrayEquals(Assert.java:534)
        at org.junit.Assert.assertArrayEquals(Assert.java:418)
        at org.junit.Assert.assertArrayEquals(Assert.java:429)
        at ArrayTests.testReservedNotEmpty(ArrayTests.java:23)
        ... 32 trimmed
Caused by: java.lang.AssertionError: expected:<4> but was:<0>
        at org.junit.Assert.fail(Assert.java:89)
        at org.junit.Assert.failNotEquals(Assert.java:835)
        at org.junit.Assert.assertEquals(Assert.java:120)
        at org.junit.Assert.assertEquals(Assert.java:146)
        at org.junit.internal.ExactComparisonCriteria.assertElementsEqual(ExactComparisonCriteria.java:8)
        at org.junit.internal.ComparisonCriteria.arrayEquals(ComparisonCriteria.java:76)
        ... 38 more

FAILURES!!!
Tests run: 3,  Failures: 1
```
- Bug Before Code Change:
```
static int[] reversed(int[] arr) {
  int[] newArray = new int[arr.length];
  for(int i = 0; i < arr.length; i += 1) {
    arr[i] = newArray[arr.length - i - 1];
  }
  return arr;
}
```
- Bug After Code Change:
```
static int[] reversed(int[] arr) {
  int[] newArray = new int[arr.length];
  for(int i = 0; i < arr.length; i += 1) {
    newArray[i] = arr[arr.length - i - 1];
  }
  return newArray;
}
```
Before, the `reversed` method modified and returned the array that was passed in as the `arr` parameter. This incorrect in two ways: first, the 'reversed' method is supposed to return 
a new array instead of modifying the original array, and secondly, because the different elements in `arr` are replaced by elements in `newArray`, which is empty. The new version of 
`reversed` places the elements of `arr` in `newArray` in reverse order, then returns `newArray`, which is correct. 

### Part 2: Researching Commands
- Command: The find command

- 1st Flag: -user

The `-user` flag modifies the output of the find command so that it only outputs the files owned by a certain user.

Source: Biswas, Supriyo. “A Guide to the Linux ‘Find’ Command.” Boolean World, 9 May 2018, www.booleanworld.com/guide-linux-find-command/. 

Example 1: 
```
srujamdave@penguin:~/docsearch$ find technical/biomed -user srujamdave
technical/biomed
technical/biomed/1468-6708-3-1.txt
technical/biomed/1468-6708-3-10.txt
technical/biomed/1468-6708-3-3.txt
technical/biomed/1468-6708-3-4.txt
technical/biomed/1468-6708-3-7.txt
...
```

Example 2:
```
srujamdave@penguin:~/docsearch$ find technical/plos -user srujamdave
technical/plos
technical/plos/journal.pbio.0020001.txt
technical/plos/journal.pbio.0020010.txt
technical/plos/journal.pbio.0020012.txt
technical/plos/journal.pbio.0020013.txt
technical/plos/journal.pbio.0020019.txt
technical/plos/journal.pbio.0020028.txt
technical/plos/journal.pbio.0020035.txt
technical/plos/journal.pbio.0020040.txt
technical/plos/journal.pbio.0020042.txt
technical/plos/journal.pbio.0020043.txt
technical/plos/journal.pbio.0020046.txt
```

- 2nd Flag: -size

The `-size` flag limits the output of the find command to files above or below a certain size. The size can be specified in bytes, kilobytes, gigabytes,
or megabytes. For example, `10c` looks for files over ten bytes, `5G` looks for files over 5 gigabytes, and `1k` looks for files over a kilobyte.

Source: Biswas, Supriyo. “A Guide to the Linux ‘Find’ Command.” Boolean World, 9 May 2018, www.booleanworld.com/guide-linux-find-command/. 

Example 1: 
```
srujamdave@penguin:~/docsearch$ find technical/biomed -size 11k
technical/biomed/1471-2156-2-8.txt
technical/biomed/1471-230X-2-17.txt
technical/biomed/1471-2350-2-8.txt
```

Example 2: 
```
srujamdave@penguin:~/docsearch$ find technical/plos -size 10k
technical/plos
technical/plos/journal.pbio.0020042.txt
technical/plos/journal.pbio.0020073.txt
technical/plos/journal.pbio.0020156.txt
technical/plos/journal.pbio.0020215.txt
technical/plos/journal.pbio.0020224.txt
technical/plos/journal.pbio.0020297.txt
technical/plos/journal.pbio.0030131.txt
technical/plos/pmed.0020005.txt
technical/plos/pmed.0020075.txt
```

- 3rd Flag: -name

This flag filters the output of the find command by the names of the files that are passed in.

Source: Biswas, Supriyo. “A Guide to the Linux ‘Find’ Command.” Boolean World, 9 May 2018, www.booleanworld.com/guide-linux-find-command/. 

Example 1: 
```
srujamdave@penguin:~/docsearch$ find technical/biomed -name '1471-2350-2-8.txt'
technical/biomed/1471-2350-2-8.txt
```

Example 2: 
```
srujamdave@penguin:~/docsearch$ find technical/plos -name 'journal.pbio.0030131.txt'
technical/plos/journal.pbio.0030131.txt
```

- 4th Flag: -empty

This flag filters the output of the find command such that it only outputs empty files.

Source: Biswas, Supriyo. “A Guide to the Linux ‘Find’ Command.” Boolean World, 9 May 2018, www.booleanworld.com/guide-linux-find-command/. 

Example 1: 
```
srujamdave@penguin:~/docsearch$ find technical/plos -empty
technical/plos/empty-example-file-i-made.txt
```

Example 2:
```
srujamdave@penguin:~/docsearch$ find technical/biomed -empty
technical/biomed/another-emmpty-example-file.txt
```
