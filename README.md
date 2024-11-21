<Window x:Class="GraWKosci.MainWindow"
        xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
        xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
        Title="Gra w Kości" Height="600" Width="800" Background="#F5F5DC">
    <Grid Margin="10">
        <!-- Tytuł -->
        <TextBlock Text="Gra w kości" FontSize="24" FontWeight="Bold" Foreground="#A52A2A"
                   HorizontalAlignment="Center" Margin="0,10,0,0"/>

        <!-- Suwak -->
        <StackPanel Orientation="Vertical" HorizontalAlignment="Center" Margin="0,50,0,0">
            <TextBlock Text="Liczba kości:" FontSize="14" Margin="0,5"/>
            <Slider x:Name="sliderLiczbaKosci" Minimum="1" Maximum="6" Value="1" TickFrequency="1" IsSnapToTickEnabled="True"
                    ValueChanged="SliderLiczbaKosci_ValueChanged"/>
            <TextBlock x:Name="labelLiczbaKosci" Text="1" FontSize="14" Margin="0,5" HorizontalAlignment="Center"/>
        </StackPanel>

        <!-- Kostki -->
        <WrapPanel x:Name="panelObrazow" HorizontalAlignment="Center" VerticalAlignment="Top" Margin="0,150,0,0"/>

        <!-- Wyniki i Przycisk Rzutu -->
        <StackPanel Orientation="Vertical" HorizontalAlignment="Center" VerticalAlignment="Bottom" Margin="0,0,0,20">
            <Button x:Name="buttonRzuc" Content="Rzuć kośćmi" Width="150" Height="40" Background="#D2691E" Foreground="White" Click="buttonRzuc_Click"/>
            <TextBlock x:Name="labelWynik" Text="Wynik: 0" FontSize="18" Margin="10,20,10,0" HorizontalAlignment="Center"/>
        </StackPanel>
    </Grid>
</Window>
