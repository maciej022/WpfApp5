using System.Text;
using System.Windows;
using System.Windows.Controls;
using System.Windows.Data;
using System.Windows.Documents;
using System.Windows.Input;
using System.Windows.Media;
using System.Windows.Media.Imaging;
using System.Windows.Navigation;
using System.Windows.Shapes;

namespace WpfApp3
{
    /// <summary>
    /// Interaction logic for MainWindow.xaml
    /// </summary>
    public partial class MainWindow : Window
    {
        public MainWindow()
        {
            InitializeComponent();
        }
        private string MaleiDuzeLitery;
        private string znakiSpecjalne;
        private string cyfry;
        private string haslo;
        Random losuj = new Random();
        private void generuj_btn_Click(object sender, RoutedEventArgs e)
        {
            /* string haslo;
             MaleiDuzeLitery = "abcdefgshijklmoprstuwxyzABCDEFGHIJKLMNOPRSTUWXYZ";
             znakiSpecjalne = "!@#$%^&*";
             int[] cyfry = new int[10];
             int ile = 0;
             ileznaow_txt.Text = ile.ToString();
             if(malelitery_check.IsChecked == true)
             {
                 //Random rnd = new Random(ile);

             }
             if (cyfry_check.IsChecked == true)
             {

             }
             if (specjalne_check.IsChecked == true)
             {

             }
             Random rnd = new Random();
            // for (int i = 0; i < Cyfry.Length; i++)

             */
            MaleiDuzeLitery = "abcdefgshijklmoprstuwxyzABCDEFGHIJKLMNOPRSTUWXYZ";
            znakiSpecjalne = "!@#$%^&*";
            cyfry = "1234567890";
            if (malelitery_check.IsChecked == true) 
            {
           //     if (!int.TryParse(ileznaow_txt.Text)
               
            /*    string wybrane = MaleiDuzeLitery;
                if (malelitery_check.IsChecked != true)
                {
                    wybrane += malelitery_check;
                }
            */
           // Random losuj = new Random();
                losuj.Next(MaleiDuzeLitery.Length);
                
            }
            if (cyfry_check.IsChecked == true)
            {
                losuj.Next(cyfry.Length);
            }
            if(specjalne_check.IsChecked == true)
            {
                losuj.Next(znakiSpecjalne.Length);
               // znakiSpecjalne == haslo.
            }

        }

        private void Zatwierdź_btn_Click(object sender, RoutedEventArgs e)
        {
            MessageBox.Show($"Dane pracownika:{imie_txt.Text} {nazwisko_txt.Text} {Stanowisko_combo.SelectedItem.ToString()} Hasło:");
        }
    }
}
