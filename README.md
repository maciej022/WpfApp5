<Window x:Class="WpfApp3.MainWindow"
        xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
        xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
        xmlns:d="http://schemas.microsoft.com/expression/blend/2008"
        xmlns:mc="http://schemas.openxmlformats.org/markup-compatibility/2006"
        xmlns:local="clr-namespace:WpfApp3"
        mc:Ignorable="d"
        Title="Edytor tekstu" Height="600" Width="800">
    <Grid>
        <Grid.RowDefinitions>
            <RowDefinition Height="Auto"/>
            <RowDefinition Height="*"/>
            <RowDefinition Height="Auto"/>
        </Grid.RowDefinitions>

        <StackPanel Orientation="Horizontal" Grid.Row="0" Margin="10">
            <CheckBox x:Name="PogrubienieCheckBox" Content="Pogrubienie" FontWeight="Bold" Margin="5" Click="PogrubienieCheckBox_Click"/>
            <CheckBox x:Name="KursywaCheckBox" Content="Kursywa" FontStyle="Italic" Margin="5" Click="KursywaCheckBox_Click"/>
            <CheckBox x:Name="PodkreslenieCheckBox" Content="Podkreślenie" Margin="5" Click="PodkreslenieCheckBox_Click"/>
            <Slider x:Name="RozmiarCzcionkiSlider" Minimum="8" Maximum="48" Value="12" Width="100" Orientation="Vertical" Height="55" ValueChanged="RozmiarCzcionkiSlider_ValueChanged"/>
            <TextBlock Text="Rozmiar" VerticalAlignment="Center" Margin="5"/>
            
            <RadioButton x:Name="CzarnyKolor" Content="Czarny" Margin="5" Click="KolorRadioButton_Click"/>
            <RadioButton x:Name="CzerwonyKolor" Content="Czerwony" Foreground="Red" Margin="5" Click="KolorRadioButton_Click"/>
            <RadioButton x:Name="NiebieskiKolor" Content="Niebieski" Foreground="Blue" Margin="5" Click="KolorRadioButton_Click"/>

            <ComboBox x:Name="KrojCzcionkiComboBox" Width="150" Margin="5" SelectionChanged="KrojCzcionkiComboBox_SelectionChanged">
                <ComboBoxItem Content="Arial"/>
                <ComboBoxItem Content="Times New Roman"/>
                <ComboBoxItem Content="Calibri"/>
            </ComboBox>
        </StackPanel>

        <RichTextBox x:Name="EdytorTekstu" Grid.Row="1" Margin="10">
            <RichTextBox.Background>
                <LinearGradientBrush StartPoint="0,0" EndPoint="1,1">
                    <GradientStop Color="LightGray" Offset="0.0"/>
                    <GradientStop Color="White" Offset="1.0"/>
                </LinearGradientBrush>
            </RichTextBox.Background>
        </RichTextBox>

        <ProgressBar x:Name="PasekPostepu" Grid.Row="2" Height="20" Margin="10" Maximum="6"/>
    </Grid>
</Window>
