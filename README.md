using System.Windows;
using System.Windows.Controls;
using System.Windows.Documents;
using System.Windows.Media;

namespace WpfApp3
{
    public partial class MainWindow : Window
    {
        private TextRange _zakresTekstu;

        public MainWindow()
        {
            InitializeComponent();

            // Sprawdzamy, czy EdytorTekstu jest gotowy do użycia
            this.Loaded += (sender, e) =>
            {
                if (EdytorTekstu != null && EdytorTekstu.Document != null)
                {
                    _zakresTekstu = new TextRange(EdytorTekstu.Document.ContentStart, EdytorTekstu.Document.ContentEnd);
                }
                else
                {
                    MessageBox.Show("Edytor tekstu nie został poprawnie zainicjalizowany.");
                }

                // Ustawienie początkowego wyboru w ComboBox
                KrojCzcionkiComboBox.SelectedIndex = 0;
            };
        }

        private void PogrubienieCheckBox_Click(object sender, RoutedEventArgs e)
        {
            ZmienFormatowanie();
        }

        private void KursywaCheckBox_Click(object sender, RoutedEventArgs e)
        {
            ZmienFormatowanie();
        }

        private void PodkreslenieCheckBox_Click(object sender, RoutedEventArgs e)
        {
            ZmienFormatowanie();
        }

        private void RozmiarCzcionkiSlider_ValueChanged(object sender, RoutedPropertyChangedEventArgs<double> e)
        {
            ZmienFormatowanie();
        }

        private void KolorRadioButton_Click(object sender, RoutedEventArgs e)
        {
            ZmienKolorCzcionki();
        }

        private void KrojCzcionkiComboBox_SelectionChanged(object sender, SelectionChangedEventArgs e)
        {
            ZmienFormatowanie();
        }

        private void ZmienFormatowanie()
        {
            // Zabezpieczenie przed null
            if (_zakresTekstu != null)
            {
                // Pogrubienie
                _zakresTekstu.ApplyPropertyValue(TextElement.FontWeightProperty, PogrubienieCheckBox.IsChecked == true ? FontWeights.Bold : FontWeights.Normal);
                // Kursywa
                _zakresTekstu.ApplyPropertyValue(TextElement.FontStyleProperty, KursywaCheckBox.IsChecked == true ? FontStyles.Italic : FontStyles.Normal);
                // Podkreślenie
                _zakresTekstu.ApplyPropertyValue(Inline.TextDecorationsProperty, PodkreslenieCheckBox.IsChecked == true ? TextDecorations.Underline : null);
                // Rozmiar czcionki
                _zakresTekstu.ApplyPropertyValue(TextElement.FontSizeProperty, RozmiarCzcionkiSlider.Value);
                // Krój czcionki
                var wybranaCzcionka = (KrojCzcionkiComboBox.SelectedItem as ComboBoxItem)?.Content.ToString();
                if (wybranaCzcionka != null)
                {
                    _zakresTekstu.ApplyPropertyValue(TextElement.FontFamilyProperty, new FontFamily(wybranaCzcionka));
                }
            }
            else
            {
                MessageBox.Show("Zakres tekstu nie został poprawnie zainicjalizowany.");
            }

            AktualizujPasekPostepu();
        }

        private void ZmienKolorCzcionki()
        {
            // Zabezpieczenie przed null
            if (_zakresTekstu != null)
            {
                if (CzarnyKolor.IsChecked == true)
                    _zakresTekstu.ApplyPropertyValue(TextElement.ForegroundProperty, Brushes.Black);
                else if (CzerwonyKolor.IsChecked == true)
                    _zakresTekstu.ApplyPropertyValue(TextElement.ForegroundProperty, Brushes.Red);
                else if (NiebieskiKolor.IsChecked == true)
                    _zakresTekstu.ApplyPropertyValue(TextElement.ForegroundProperty, Brushes.Blue);
            }
            else
            {
                MessageBox.Show("Zakres tekstu nie został poprawnie zainicjalizowany.");
            }

            AktualizujPasekPostepu();
        }

        private void AktualizujPasekPostepu()
        {
            int ustawieniaUzyte = 0;

            if (PogrubienieCheckBox.IsChecked == true) ustawieniaUzyte++;
            if (KursywaCheckBox.IsChecked == true) ustawieniaUzyte++;
            if (PodkreslenieCheckBox.IsChecked == true) ustawieniaUzyte++;
            if (RozmiarCzcionkiSlider.Value != 12) ustawieniaUzyte++;
            if (CzarnyKolor.IsChecked == true || CzerwonyKolor.IsChecked == true || NiebieskiKolor.IsChecked == true) ustawieniaUzyte++;
            if (KrojCzcionkiComboBox.SelectedIndex != 0) ustawieniaUzyte++;

            PasekPostepu.Value = ustawieniaUzyte;
        }
    }
}
