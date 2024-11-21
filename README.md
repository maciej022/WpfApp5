<Window x:Class="GraWKosci.MainWindow"
        xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
        xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
        Title="Gra w Kości" Height="450" Width="800">
    <Grid Background="#F5F5DC">
        <TextBlock Text="Gra w Kości. Autor: 000000000" 
                   Foreground="#A52A2A" FontSize="20" 
                   HorizontalAlignment="Center" VerticalAlignment="Top" Margin="0,10,0,0"/>

        <StackPanel HorizontalAlignment="Center" VerticalAlignment="Top" Margin="0,50,0,0">
            <TextBlock Text="Ustawienia:" FontSize="16"/>
            <StackPanel Orientation="Horizontal" Margin="0,10">
                <TextBlock Text="Liczba kości:" Margin="0,0,10,0"/>
                <Slider x:Name="SuwakLiczbaKosci" Minimum="1" Maximum="6" Value="1" Width="100"/>
                <TextBlock x:Name="EtykietaLiczbaKosci" Text="1" Margin="10,0,0,0"/>
            </StackPanel>
            <StackPanel Orientation="Horizontal" Margin="0,10">
                <TextBlock Text="Liczba ścian:" Margin="0,0,10,0"/>
                <Slider x:Name="SuwakLiczbaScian" Minimum="4" Maximum="10" Value="6" Width="100"/>
                <TextBlock x:Name="EtykietaLiczbaScian" Text="6" Margin="10,0,0,0"/>
            </StackPanel>
        </StackPanel>

        <Button Content="Rzuć Kośćmi" 
                x:Name="PrzyciskRzut" 
                Background="#D2691E" Foreground="White" 
                HorizontalAlignment="Center" VerticalAlignment="Top" 
                Width="150" Margin="0,180,0,0" Click="PrzyciskRzut_Click"/>

        <StackPanel HorizontalAlignment="Center" VerticalAlignment="Top" Margin="0,250,0,0">
            <StackPanel x:Name="PanelWynikiKosci" Orientation="Horizontal" Margin="0,10"/>
            <TextBlock x:Name="WynikAktualnegoRzutu" Text="Wynik tego losowania: 0" Margin="0,10"/>
            <TextBlock x:Name="WynikCalkowityGry" Text="Wynik gry: 0" Margin="0,10"/>
        </StackPanel>

        <Button Content="Resetuj Wynik" 
                x:Name="PrzyciskReset" 
                Background="#D2691E" Foreground="White" 
                HorizontalAlignment="Center" VerticalAlignment="Bottom" 
                Width="150" Margin="0,10,0,10" Click="PrzyciskReset_Click"/>
    </Grid>
</Window>
