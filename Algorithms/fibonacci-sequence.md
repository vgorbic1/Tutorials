## Fibonacci Sequence
*Each element is a sum of two previous elements.*

F<sub>n</sub> = F<sub>n-1</sub> + F<sub>n-2</sub> | F<sub>0</sub> = 0 and F<sub>1</sub> = 1.
```
0, 1, 1, 2, 3, 5, 8, 13, 21, 34, 55, 89, 144,...
```
Write a function that returns F<sub>n</sub> (takes a position of the element in the Fibonacci Sequesnce
and returns the number of the sequence that corresponds to this position).
```c++
int getFibonacciElement(int n)
{
    // Declare and array to store Fibonacci Sequence
    int f[n+1];
    int i;

    // First and second elements of Fibonacci Sequence
    f[0] = 0;
    f[1] = 1;

    for (i = 2; i <= n; i++)
        // Add the previous 2 numbers in the series
        f[i] = f[i - 1] + f[i - 2];

    return f[n];
}
```
Write a function that represents the Fibonacci Sequence of the given number of elements.
```c++
void fib(int n)
{
    // Declare an array of n elements
    int f[n];
    int i;
    // First and second elements of Fibonacci Sequence
    f[0] = 0;
    f[1] = 1;

    for (i = 2; i < n; i++)
        // Add the previous 2 numbers in the series
        f[i] = f[i - 1] + f[i - 2];

    // Display the sequence
    for (int j = 0; j < n; j++)
        cout << f[j] << " ";
}
```
