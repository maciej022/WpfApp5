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

        private void PogrubienieCheckBox_Checked(object sender, RoutedEventArgs e)
        {
            var zakresTekstu = new TextRange(EdytorTekstu.Document.ContentStart, EdytorTekstu.Document.ContentEnd);
            zakresTekstu.ApplyPropertyValue(TextElement.FontWeightProperty, FontWeights.Bold);
            AktualizujPasekPostepu();
        }

        private void PogrubienieCheckBox_Unchecked(object sender, RoutedEventArgs e)
        {
            var zakresTekstu = new TextRange(EdytorTekstu.Document.ContentStart, EdytorTekstu.Document.ContentEnd);
            zakresTekstu.ApplyPropertyValue(TextElement.FontWeightProperty, FontWeights.Normal);
            AktualizujPasekPostepu();
        }

        private void KursywaCheckBox_Checked(object sender, RoutedEventArgs e)
        {
            var zakresTekstu = new TextRange(EdytorTekstu.Document.ContentStart, EdytorTekstu.Document.ContentEnd);
            zakresTekstu.ApplyPropertyValue(TextElement.FontStyleProperty, FontStyles.Italic);
            AktualizujPasekPostepu();
        }

        private void KursywaCheckBox_Unchecked(object sender, RoutedEventArgs e)
        {
            var zakresTekstu = new TextRange(EdytorTekstu.Document.ContentStart, EdytorTekstu.Document.ContentEnd);
            zakresTekstu.ApplyPropertyValue(TextElement.FontStyleProperty, FontStyles.Normal);
            AktualizujPasekPostepu();
        }

        private void PodkreslenieCheckBox_Checked(object sender, RoutedEventArgs e)
        {
            var zakresTekstu = new TextRange(EdytorTekstu.Document.ContentStart, EdytorTekstu.Document.ContentEnd);
            zakresTekstu.ApplyPropertyValue(Inline.TextDecorationsProperty, TextDecorations.Underline);
            AktualizujPasekPostepu();
        }

        private void PodkreslenieCheckBox_Unchecked(object sender, RoutedEventArgs e)
        {
            var zakresTekstu = new TextRange(EdytorTekstu.Document.ContentStart, EdytorTekstu.Document.ContentEnd);
            zakresTekstu.ApplyPropertyValue(Inline.TextDecorationsProperty, null);
            AktualizujPasekPostepu();
        }

        private void RozmiarCzcionkiSlider_ValueChanged(object sender, RoutedPropertyChangedEventArgs<double> e)
        {
            var zakresTekstu = new TextRange(EdytorTekstu.Document.ContentStart, EdytorTekstu.Document.ContentEnd);
            zakresTekstu.ApplyPropertyValue(TextElement.FontSizeProperty, RozmiarCzcionkiSlider.Value);
            AktualizujPasekPostepu();
        }

        private void CzarnyKolor_Checked(object sender, RoutedEventArgs e)
        {
            var zakresTekstu = new TextRange(EdytorTekstu.Document.ContentStart, EdytorTekstu.Document.ContentEnd);
            zakresTekstu.ApplyPropertyValue(TextElement.ForegroundProperty, Brushes.Black);
            AktualizujPasekPostepu();
        }

        private void CzerwonyKolor_Checked(object sender, RoutedEventArgs e)
        {
            var zakresTekstu = new TextRange(EdytorTekstu.Document.ContentStart, EdytorTekstu.Document.ContentEnd);
            zakresTekstu.ApplyPropertyValue(TextElement.ForegroundProperty, Brushes.Red);
            AktualizujPasekPostepu();
        }

        private void NiebieskiKolor_Checked(object sender, RoutedEventArgs e)
        {
            var zakresTekstu = new TextRange(EdytorTekstu.Document.ContentStart, EdytorTekstu.Document.ContentEnd);
            zakresTekstu.ApplyPropertyValue(TextElement.ForegroundProperty, Brushes.Blue);
            AktualizujPasekPostepu();
        }

        private void KrojCzcionkiComboBox_SelectionChanged(object sender, SelectionChangedEventArgs e)
        {
            var zakresTekstu = new TextRange(EdytorTekstu.Document.ContentStart, EdytorTekstu.Document.ContentEnd);
            zakresTekstu.ApplyPropertyValue(TextElement.FontFamilyProperty, new FontFamily((KrojCzcionkiComboBox.SelectedItem as ComboBoxItem)?.Content.ToString()));
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
