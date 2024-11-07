using System.Windows;
using System.Windows.Controls;
using System.Windows.Documents;
using System.Windows.Media;

namespace WpfApp3
{
    public partial class MainWindow : Window
    {
        // Deklaracja zmiennych dla zakresu tekstu i innych właściwości
        private TextRange _zakresTekstu;
        
        public MainWindow()
        {
            InitializeComponent();
            KrojCzcionkiComboBox.SelectedIndex = 0;

            // Inicjalizacja zmiennej dla zakresu tekstu
            _zakresTekstu = new TextRange(EdytorTekstu.Document.ContentStart, EdytorTekstu.Document.ContentEnd);
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
            // Korzystamy ze zmiennej _zakresTekstu
            _zakresTekstu.ApplyPropertyValue(TextElement.FontWeightProperty, PogrubienieCheckBox.IsChecked == true ? FontWeights.Bold : FontWeights.Normal);
            _zakresTekstu.ApplyPropertyValue(TextElement.FontStyleProperty, KursywaCheckBox.IsChecked == true ? FontStyles.Italic : FontStyles.Normal);
            _zakresTekstu.ApplyPropertyValue(Inline.TextDecorationsProperty, PodkreslenieCheckBox.IsChecked == true ? TextDecorations.Underline : null);
            _zakresTekstu.ApplyPropertyValue(TextElement.FontSizeProperty, RozmiarCzcionkiSlider.Value);
            _zakresTekstu.ApplyPropertyValue(TextElement.FontFamilyProperty, new FontFamily((KrojCzcionkiComboBox.SelectedItem as ComboBoxItem)?.Content.ToString()));

            AktualizujPasekPostepu();
        }

        private void ZmienKolorCzcionki()
        {
            // Korzystamy ze zmiennej _zakresTekstu
            if (CzarnyKolor.IsChecked == true)
                _zakresTekstu.ApplyPropertyValue(TextElement.ForegroundProperty, Brushes.Black);
            else if (CzerwonyKolor.IsChecked == true)
                _zakresTekstu.ApplyPropertyValue(TextElement.ForegroundProperty, Brushes.Red);
            else if (NiebieskiKolor.IsChecked == true)
                _zakresTekstu.ApplyPropertyValue(TextElement.ForegroundProperty, Brushes.Blue);

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
