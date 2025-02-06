using System;

class Program
{
    static void Main()
    {
        Console.Write("Podaj tekst: ");
        string input = Console.ReadLine();

        if (string.IsNullOrEmpty(input))
        {
            Console.WriteLine("Liczba samogłosek: 0");
            Console.WriteLine("Tekst po usunięciu powtórzeń: ");
            return;
        }

        char[] vowels = { 'a', 'ą', 'e', 'ę', 'i', 'o', 'u', 'y', 'A', 'Ą', 'E', 'Ę', 'I', 'O', 'U', 'Y' };
        int vowelCount = 0;

        // Liczenie samogłosek
        foreach (char c in input)
        {
            foreach (char v in vowels)
            {
                if (c == v)
                {
                    vowelCount++;
                    break;
                }
            }
        }

        // Usuwanie powtórzeń znaków obok siebie
        char[] result = new char[input.Length];
        int index = 0;

        result[index++] = input[0];

        for (int i = 1; i < input.Length; i++)
        {
            if (input[i] != input[i - 1])
            {
                result[index++] = input[i];
            }
        }

        string cleanedText = new string(result, 0, index);

        Console.WriteLine($"Liczba samogłosek: {vowelCount}");
        Console.WriteLine($"Tekst po usunięciu powtórzeń: {cleanedText}");
    }
}
