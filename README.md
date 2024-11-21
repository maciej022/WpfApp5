using System;
using System.Windows;
using System.Windows.Controls;
using System.Windows.Media.Imaging;

namespace GraWKosci
{
    public partial class MainWindow : Window
    {
        private int wynikCalkowity = 0;

        public MainWindow()
        {
            InitializeComponent();
            sliderLiczbaKosci.ValueChanged += SliderLiczbaKosci_ValueChanged;
            sliderLiczbaScian.ValueChanged += SliderLiczbaScian_ValueChanged;
        }

        private void SliderLiczbaKosci_ValueChanged(object sender, RoutedPropertyChangedEventArgs<double> e)
        {
            labelLiczbaKosci.Text = ((int)sliderLiczbaKosci.Value).ToString();
        }

        private void SliderLiczbaScian_ValueChanged(object sender, RoutedPropertyChangedEventArgs<double> e)
        {
            labelLiczbaScian.Text = ((int)sliderLiczbaScian.Value).ToString();
        }

        private void buttonRzuc_Click(object sender, RoutedEventArgs e)
        {
            int liczbaKosci = (int)sliderLiczbaKosci.Value;
            int liczbaScian = (int)sliderLiczbaScian.Value;

            Random random = new Random();
            int wynikRzutu = 0;

            panelObrazow.Children.Clear(); // Wyczyść poprzednie obrazy

            for (int i = 0; i < liczbaKosci; i++)
            {
                int rzut = random.Next(1, liczbaScian + 1);
                wynikRzutu += rzut;

                // Wyświetlanie obrazka wyniku rzutu
                Image obraz = new Image();
                obraz.Width = 50;
                obraz.Height = 50;

                try
                {
                    // Wczytaj obraz z folderu "Images"
                    obraz.Source = new BitmapImage(new Uri($"pack://application:,,,/Images/{rzut}.png"));
                }
                catch
                {
                    // Jeśli obraz nie istnieje, wyświetl znak zapytania
                    obraz.Source = new BitmapImage(new Uri($"pack://application:,,,/Images/question.png"));
                }

                panelObrazow.Children.Add(obraz);
            }

            wynikCalkowity += wynikRzutu;
            labelWynik.Text = $"Suma rzutów: {wynikRzutu}\nWynik całkowity: {wynikCalkowity}";
        }

        private void buttonResetuj_Click(object sender, RoutedEventArgs e)
        {
            wynikCalkowity = 0;
            labelWynik.Text = "Wynik: 0";
            panelObrazow.Children.Clear();
        }
    }
}

