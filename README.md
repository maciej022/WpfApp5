using System;
using System.Windows;
using System.Windows.Controls;
using System.Windows.Media.Imaging;

namespace GraWKosci
{
    public partial class MainWindow : Window
    {
        private Random losowaLiczba = new Random(); // Generator liczb losowych
        private int wynikCalkowity = 0; // Wynik całkowity gry

        public MainWindow()
        {
            InitializeComponent();

            // Aktualizacja etykiet przy zmianie wartości na suwakach
            SuwakLiczbaKosci.ValueChanged += AktualizujEtykieteLiczbaKosci;
            SuwakLiczbaScian.ValueChanged += AktualizujEtykieteLiczbaScian;
        }

        // Aktualizacja etykiety dla liczby kości
        private void AktualizujEtykieteLiczbaKosci(object sender, RoutedPropertyChangedEventArgs<double> e)
        {
            EtykietaLiczbaKosci.Text = ((int)SuwakLiczbaKosci.Value).ToString();
        }

        // Aktualizacja etykiety dla liczby ścian
        private void AktualizujEtykieteLiczbaScian(object sender, RoutedPropertyChangedEventArgs<double> e)
        {
            EtykietaLiczbaScian.Text = ((int)SuwakLiczbaScian.Value).ToString();
        }

        // Obsługa przycisku "Rzuć Kośćmi"
        private void PrzyciskRzut_Click(object sender, RoutedEventArgs e)
        {
            PanelWynikiKosci.Children.Clear(); // Czyszczenie panelu z obrazami kości
            int liczbaKosci = (int)SuwakLiczbaKosci.Value;
            int liczbaScian = (int)SuwakLiczbaScian.Value;

            int sumaRzutu = 0; // Suma oczek w aktualnym rzucie
            for (int i = 0; i < liczbaKosci; i++)
            {
                int wynikKosci = losowaLiczba.Next(1, liczbaScian + 1);
                sumaRzutu += wynikKosci;

                // Dodanie obrazu kości
                var obrazKosci = new Image
                {
                    Source = new BitmapImage(new Uri($"pack://application:,,,/Images/dice_{wynikKosci}.png")),
                    Width = 50,
                    Height = 50,
                    Margin = new Thickness(5)
                };
                PanelWynikiKosci.Children.Add(obrazKosci);
            }

            wynikCalkowity += sumaRzutu; // Dodanie sumy rzutu do wyniku całkowitego
            WynikAktualnegoRzutu.Text = $"Wynik tego losowania: {sumaRzutu}";
            WynikCalkowityGry.Text = $"Wynik gry: {wynikCalkowity}";
        }

        // Obsługa przycisku "Resetuj Wynik"
        private void PrzyciskReset_Click(object sender, RoutedEventArgs e)
        {
            wynikCalkowity = 0; // Reset wyniku całkowitego
            WynikAktualnegoRzutu.Text = "Wynik tego losowania: 0";
            WynikCalkowityGry.Text = "Wynik gry: 0";
            PanelWynikiKosci.Children.Clear(); // Czyszczenie panelu z obrazami kości
        }
    }
}
