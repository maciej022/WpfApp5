using System;

class Program
{
    static void Main()
    {
        Console.Write("Podaj liczbę wierszy: ");
        int rows = int.Parse(Console.ReadLine());

        Console.Write("Podaj liczbę kolumn: ");
        int cols = int.Parse(Console.ReadLine());

        Random rand = new Random();
        int[,] array = new int[rows, cols];

        for (int i = 0; i < rows; i++)
        {
            for (int j = 0; j < cols; j++)
            {
                array[i, j] = i % 2 == 0 ? rand.Next(0, 101) : rand.Next(-100, 1);
            }
        }

        Console.WriteLine("\nWygenerowana tablica:");
        double[] rowAverages = new double[rows];

        for (int i = 0; i < rows; i++)
        {
            int sum = 0;
            for (int j = 0; j < cols; j++)
            {
                Console.Write(array[i, j] + "\t");
                sum += array[i, j];
            }
            rowAverages[i] = (double)sum / cols;
            Console.WriteLine($"| Średnia: {rowAverages[i]:F2}");
        }

        Console.WriteLine("\nLiczby parzyste większe od średniej w swoim wierszu:");
        for (int i = 0; i < rows; i++)
        {
            Console.Write($"Wiersz {i}: ")
            
