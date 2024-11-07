using System.Windows;
using System.Windows.Controls;
using System.Windows.Documents;
using System.Windows.Media;

namespace WpfApp3
{
    public partial class MainWindow : Window
    {
        public MainWindow()
        {
            InitializeComponent();
            KrojCzcionkiComboBox.SelectedIndex = 0;
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
            var zakresTekstu = new TextRange(EdytorTekstu.Document.ContentStart, EdytorTekstu.Document.ContentEnd);

            // Pogrubienie
            zakresTekstu.ApplyPropertyValue(TextElement.FontWeightProperty, PogrubienieCheckBox.IsChecked == true ? FontWeights.Bold : FontWeights.Normal);

            // Kursywa
            zakresTekstu.ApplyPropertyValue(TextElement.FontStyleProperty, KursywaCheckBox.IsChecked == true ? FontStyles.Italic : FontStyles.Normal);

            // Podkreślenie
            zakresTekstu.ApplyPropertyValue(Inline.TextDecorationsProperty, PodkreslenieCheckBox.IsChecked == true ? TextDecorations.Underline : null);

            // Rozmiar czcionki
            zakresTekstu.ApplyPropertyValue(TextElement.FontSizeProperty, RozmiarCzcionkiSlider.Value);

            // Krój czcionki
            zakresTekstu.ApplyPropertyValue(TextElement.FontFamilyProperty, new FontFamily((KrojCzcionkiComboBox.SelectedItem as ComboBoxItem)?.Content.ToString()));

            AktualizujPasekPostepu();
        }

        private void ZmienKolorCzcionki()
        {
            var zakresTekstu = new TextRange(EdytorTekstu.Document.ContentStart, EdytorTekstu.Document.ContentEnd);

            if (CzarnyKolor.IsChecked == true)
                zakresTekstu.ApplyPropertyValue(TextElement.ForegroundProperty, Brushes.Black);
            else if (CzerwonyKolor.IsChecked == true)
                zakresTekstu.ApplyPropertyValue(TextElement.ForegroundProperty, Brushes.Red);
            else if (NiebieskiKolor.IsChecked == true)
                zakresTekstu.ApplyPropertyValue(TextElement.ForegroundProperty, Brushes.Blue);

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
