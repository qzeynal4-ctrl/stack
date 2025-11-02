using System;
using System.Collections.Generic;

class Program
{
    static void Main()
    {
        string[] input = Console.ReadLine().Split();
        int n = int.Parse(input[0]);
        long a = long.Parse(input[1]);
        long b = long.Parse(input[2]);
        long c = long.Parse(input[3]);
        long x = long.Parse(input[4]);

        Stack<long> stack = new Stack<long>();
        // Minimumları effektiv tapmaq üçün ayrıca minStack istifadə edirik
        Stack<long> minStack = new Stack<long>();

        long result = 0;

        for (int i = 0; i < n; i++)
        {
            // Yeni x hesablanır
            x = (a * x * x + b * x + c) / 100 % 1000000;

            if (x % 5 < 2)
            {
                // Pop əməliyyatı
                if (stack.Count > 0)
                {
                    stack.Pop();
                    minStack.Pop();
                }
            }
            else
            {
                // Push əməliyyatı
                stack.Push(x);
                if (minStack.Count == 0)
                    minStack.Push(x);
                else
                    minStack.Push(Math.Min(x, minStack.Peek()));
            }

            // Hər əməliyyatdan sonra stek boş deyilsə minimumu əlavə edirik
            if (stack.Count > 0)
                result += minStack.Peek();
        }

        Console.WriteLine(result);
    }
}

