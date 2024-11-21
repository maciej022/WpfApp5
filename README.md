<Window x:Class="GraWKosci.MainWindow"
        xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
        xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
        Title="Gra w Kości" Height="600" Width="800" Background="#F5F5DC">
    <Grid Margin="10">
        <!-- Tytuł -->
        <TextBlock Text="Gra w kości" FontSize="24" FontWeight="Bold" Foreground="#A52A2A"
                   HorizontalAlignment="Center" Margin="0,10,0,0"/>

        <!-- Suwaki -->
        <StackPanel Orientation="Vertical" Margin="10,50,10,0">
            <TextBlock Text="Liczba kości:" FontSize="14" Margin="0,5"/>
            <Slider x:Name="sliderLiczbaKosci" Minimum="1" Maximum="6" Value="1" TickFrequency="1" IsSnapToTickEnabled="True"/>
            <TextBlock x:Name="labelLiczbaKosci" Text="1" FontSize="14" Margin="0,5"/>

            <TextBlock Text="Liczba ścian na kości:" FontSize="14" Margin="0,15"/>
            <Slider x:Name="sliderLiczbaScian" Minimum="4" Maximum="10" Value="6" TickFrequency="1" IsSnapToTickEnabled="True"/>
            <TextBlock x:Name="labelLiczbaScian" Text="6" FontSize="14" Margin="0,5"/>
        </StackPanel>

        <!-- Przycisk i Wyniki -->
        <StackPanel Orientation="Vertical" HorizontalAlignment="Center" VerticalAlignment="Top" Margin="0,150,0,0">
            <Button x:Name="buttonRzuc" Content="Rzuć kośćmi" Width="150" Height="40" Background="#D2691E" Foreground="White" Click="buttonRzuc_Click"/>
            <TextBlock x:Name="labelWynik" Text="Wynik: " FontSize="18" Margin="0,20,0,0"/>
            <Button Content="Zresetuj wynik" Width="150" Height="40" Margin="0,10,0,0" Click="buttonResetuj_Click"/>
        </StackPanel>

        <!-- Miejsce na obrazy -->
        <WrapPanel x:Name="panelObrazow" HorizontalAlignment="Center" VerticalAlignment="Bottom" Margin="0,20,0,0"/>
    </Grid>
</Window>
