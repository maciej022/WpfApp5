using System.Windows;
using System.Windows.Controls;
using System.Windows.Documents;
using System.Windows.Media;

namespace TextEditorApp
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
            var zakresTekstu = new TextRange(EdytorTekstu.Document.ContentStart, EdytorTekstu.Document.ContentEnd);
            zakresTekstu.ApplyPropertyValue(TextElement.FontWeightProperty, PogrubienieCheckBox.IsChecked == true ? FontWeights.Bold : FontWeights.Normal);
            AktualizujPasekPostepu();
        }

        private void KursywaCheckBox_Click(object sender, RoutedEventArgs e)
        {
            var zakresTekstu = new TextRange(EdytorTekstu.Document.ContentStart, EdytorTekstu.Document.ContentEnd);
            zakresTekstu.ApplyPropertyValue(TextElement.FontStyleProperty, KursywaCheckBox.IsChecked == true ? FontStyles.Italic : FontStyles.Normal);
            AktualizujPasekPostepu();
        }

        private void PodkreslenieCheckBox_Click(object sender, RoutedEventArgs e)
        {
            var zakresTekstu = new TextRange(EdytorTekstu.Document.ContentStart, EdytorTekstu.Document.ContentEnd);
            zakresTekstu.ApplyPropertyValue(Inline.TextDecorationsProperty, PodkreslenieCheckBox.IsChecked == true ? TextDecorations.Underline : null);
            AktualizujPasekPostepu();
        }

        private void RozmiarCzcionkiSlider_ValueChanged(object sender, RoutedPropertyChangedEventArgs<double> e)
        {
            var zakresTekstu = new TextRange(EdytorTekstu.Document.ContentStart, EdytorTekstu.Document.ContentEnd);
            zakresTekstu.ApplyPropertyValue(TextElement.FontSizeProperty, RozmiarCzcionkiSlider.Value);
            AktualizujPasekPostepu();
        }

        private void CzarnyKolor_Click(object sender, RoutedEventArgs e)
        {
            ZmienKolorCzcionki(Brushes.Black);
            AktualizujPasekPostepu();
        }

        private void CzerwonyKolor_Click(object sender, RoutedEventArgs e)
        {
            ZmienKolorCzcionki(Brushes.Red);
            AktualizujPasekPostepu();
        }

        private void NiebieskiKolor_Click(object sender, RoutedEventArgs e)
        {
            ZmienKolorCzcionki(Brushes.Blue);
            AktualizujPasekPostepu();
        }

        private void KrojCzcionkiComboBox_SelectionChanged(object sender, SelectionChangedEventArgs e)
        {
            var zakresTekstu = new TextRange(EdytorTekstu.Document.ContentStart, EdytorTekstu.Document.ContentEnd);
            zakresTekstu.ApplyPropertyValue(TextElement.FontFamilyProperty, new FontFamily((KrojCzcionkiComboBox.SelectedItem as ComboBoxItem)?.Content.ToString()));
            AktualizujPasekPostepu();
        }

        private void ZmienKolorCzcionki(Brush kolor)
        {
            var zakresTekstu = new TextRange(EdytorTekstu.Document.ContentStart, EdytorTekstu.Document.ContentEnd);
            zakresTekstu.ApplyPropertyValue(TextElement.ForegroundProperty, kolor);
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
