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
            UaktualnijKostki(); // Inicjalizuj wyświetlanie kostek
        }

        private void SliderLiczbaKosci_ValueChanged(object sender, RoutedPropertyChangedEventArgs<double> e)
        {
            labelLiczbaKosci.Text = ((int)sliderLiczbaKosci.Value).ToString();
            UaktualnijKostki();
        }

        private void UaktualnijKostki()
        {
            int liczbaKosci = (int)sliderLiczbaKosci.Value;

            // Wyczyszczenie poprzednich obrazów
            panelObrazow.Children.Clear();

            // Dodawanie obrazów
            for (int i = 0; i < liczbaKosci; i++)
            {
                Image obraz = new Image
                {
                    Width = 80,
                    Height = 80,
                    Margin = new Thickness(5),
                    Source = new BitmapImage(new Uri("pack://application:,,,/Images/kostkanieznane.png")) // Obraz dla stanu początkowego
                };
                panelObrazow.Children.Add(obraz);
            }
        }

        private void buttonRzuc_Click(object sender, RoutedEventArgs e)
        {
            int liczbaKosci = (int)sliderLiczbaKosci.Value;
            Random random = new Random();
            int wynikRzutu = 0;

            for (int i = 0; i < panelObrazow.Children.Count; i++)
            {
                int rzut = random.Next(1, 7); // Losuje wynik od 1 do 6
                wynikRzutu += rzut;

                // Aktualizuj obraz kości na podstawie wyniku
                if (panelObrazow.Children[i] is Image kostka)
                {
                    kostka.Source = new BitmapImage(new Uri($"pack://application:,,,/Images/kostka{rzut}.png"));
                }
            }

            wynikCalkowity += wynikRzutu;
            labelWynik.Text = $"Wynik rzutu: {wynikRzutu}\nWynik całkowity: {wynikCalkowity}";
        }
    }
}
