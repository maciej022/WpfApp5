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

        private void ZmienFormat(object sender, RoutedEventArgs e)
        {
            AktualizujFormatowanieTekstu();
        }

        private void RozmiarCzcionkiSlider_Zmieniono(object sender, RoutedPropertyChangedEventArgs<double> e)
        {
            AktualizujFormatowanieTekstu();
        }

        private void ZmienKolor(object sender, RoutedEventArgs e)
        {
            AktualizujFormatowanieTekstu();
        }

        private void KrojCzcionkiComboBox_Zmieniono(object sender, SelectionChangedEventArgs e)
        {
            AktualizujFormatowanieTekstu();
        }

        private void AktualizujFormatowanieTekstu()
        {
            var zakresTekstu = new TextRange(EdytorTekstu.Document.ContentStart, EdytorTekstu.Document.ContentEnd);
            zakresTekstu.ApplyPropertyValue(TextElement.FontSizeProperty, RozmiarCzcionkiSlider.Value);
            zakresTekstu.ApplyPropertyValue(TextElement.FontFamilyProperty, new FontFamily((KrojCzcionkiComboBox.SelectedItem as ComboBoxItem)?.Content.ToString()));

            if (PogrubienieCheckBox.IsChecked == true)
                zakresTekstu.ApplyPropertyValue(TextElement.FontWeightProperty, FontWeights.Bold);
            else
                zakresTekstu.ApplyPropertyValue(TextElement.FontWeightProperty, FontWeights.Normal);

            if (KursywaCheckBox.IsChecked == true)
                zakresTekstu.ApplyPropertyValue(TextElement.FontStyleProperty, FontStyles.Italic);
            else
                zakresTekstu.ApplyPropertyValue(TextElement.FontStyleProperty, FontStyles.Normal);

            if (PodkreslenieCheckBox.IsChecked == true)
                zakresTekstu.ApplyPropertyValue(Inline.TextDecorationsProperty, TextDecorations.Underline);
            else
                zakresTekstu.ApplyPropertyValue(Inline.TextDecorationsProperty, null);

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
