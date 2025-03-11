using System;
using System.Text;
using System.Windows;
using System.Windows.Input;

namespace PasswordGenerator
{
    public partial class MainWindow : Window
    {
        private string lowercaseLetters;
        private string uppercaseLetters;
        private string numbers;
        private string specialCharacters;

        public MainWindow()
        {
            InitializeComponent();

            // Inicjalizacja zmiennych zamiast const
            lowercaseLetters = "abcdefghijklmnopqrstuvwxyz";
            uppercaseLetters = "ABCDEFGHIJKLMNOPQRSTUVWXYZ";
            numbers = "0123456789";
            specialCharacters = "!@#$%^&*()-_=+[]{}|;:,.<>?/";
        }

        private void GeneratePassword_Click(object sender, RoutedEventArgs e)
        {
            if (!int.TryParse(PasswordLengthTextBox.Text, out int passwordLength) || passwordLength < 4)
            {
                MessageBox.Show("Podaj poprawną długość hasła (min. 4 znaki)", "Błąd", MessageBoxButton.OK, MessageBoxImage.Warning);
                return;
            }

            string characterSet = lowercaseLetters;
            if (IncludeUppercaseCheckBox.IsChecked == true) characterSet += uppercaseLetters;
            if (IncludeNumbersCheckBox.IsChecked == true) characterSet += numbers;
            if (IncludeSpecialCharsCheckBox.IsChecked == true) characterSet += specialCharacters;

            if (string.IsNullOrEmpty(characterSet))
            {
                MessageBox.Show("Wybierz przynajmniej jeden zestaw znaków!", "Błąd", MessageBoxButton.OK, MessageBoxImage.Warning);
                return;
            }

            Random random = new Random();
            StringBuilder password = new StringBuilder();

            for (int i = 0; i < passwordLength; i++)
            {
                password.Append(characterSet[random.Next(characterSet.Length)]);
            }

            GeneratedPasswordTextBox.Text = password.ToString();
        }

        private void PasswordLengthTextBox_PreviewTextInput(object sender, TextCompositionEventArgs e)
        {
            e.Handled = !int.TryParse(e.Text, out _); // Zapobiega wpisywaniu liter
        }

        private void CopyPassword_Click(object sender, RoutedEventArgs e)
        {
            if (!string.IsNullOrEmpty(GeneratedPasswordTextBox.Text))
            {
                Clipboard.SetText(GeneratedPasswordTextBox.Text);
                MessageBox.Show("Hasło skopiowane do schowka!", "Informacja", MessageBoxButton.OK, MessageBoxImage.Information);
            }
        }
    }
}
