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
