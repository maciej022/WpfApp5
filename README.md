document.getElementById("przycisk").addEventListener("click", function() {
    let waga = parseFloat(document.getElementById("waga").value);
    let wzrost = parseFloat(document.getElementById("wzrost").value) / 100; // Zamiana cm na metry

    if (!waga || !wzrost || wzrost <= 0 || waga <= 0) {
        pokazWynik("Podaj poprawne dane!", "red");
        return;
    }

    let bmi = waga / (wzrost * wzrost);
    let kategoria = okreslKategorie(bmi);

    pokazWynik(`Twoje BMI: ${bmi.toFixed(2)} (${kategoria})`, "black");
});

function okreslKategorie(bmi) {
    if (bmi < 18.5) return "Niedowaga";
    if (bmi < 24.9) return "Prawidłowa waga";
    if (bmi < 29.9) return "Nadwaga";
    return "Otyłość";
}

function pokazWynik(tekst, kolor) {
    let wynik = document.getElementById("wynik");
    wynik.innerText = tekst;
    wynik.style.color = kolor;
}
