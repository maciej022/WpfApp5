<Window x:Class="TextEditorApp.MainWindow"
        xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
        xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
        Title="Edytor Tekstu" Height="600" Width="800">
    <Grid>
        <Grid.RowDefinitions>
            <RowDefinition Height="Auto"/>
            <RowDefinition Height="*"/>
            <RowDefinition Height="Auto"/>
        </Grid.RowDefinitions>
        
        <StackPanel Orientation="Horizontal" Grid.Row="0" Margin="10">
            <CheckBox x:Name="PogrubienieCheckBox" Content="Pogrubienie" FontWeight="Bold" Margin="5" Checked="ZmienFormat" Unchecked="ZmienFormat"/>
            <CheckBox x:Name="KursywaCheckBox" Content="Kursywa" FontStyle="Italic" Margin="5" Checked="ZmienFormat" Unchecked="ZmienFormat"/>
            <CheckBox x:Name="PodkreslenieCheckBox" Content="Podkreślenie" TextDecorations="Underline" Margin="5" Checked="ZmienFormat" Unchecked="ZmienFormat"/>
            
            <Slider x:Name="RozmiarCzcionkiSlider" Minimum="8" Maximum="48" Value="12" Width="100" Margin="5" ValueChanged="RozmiarCzcionkiSlider_Zmieniono"/>
            <TextBlock Text="Rozmiar" VerticalAlignment="Center" Margin="5"/>
            
            <RadioButton x:Name="CzarnyKolor" Content="Czarny" Margin="5" Checked="ZmienKolor"/>
            <RadioButton x:Name="CzerwonyKolor" Content="Czerwony" Foreground="Red" Margin="5" Checked="ZmienKolor"/>
            <RadioButton x:Name="NiebieskiKolor" Content="Niebieski" Foreground="Blue" Margin="5" Checked="ZmienKolor"/>
            
            <ComboBox x:Name="KrojCzcionkiComboBox" Width="150" Margin="5" SelectionChanged="KrojCzcionkiComboBox_Zmieniono">
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
