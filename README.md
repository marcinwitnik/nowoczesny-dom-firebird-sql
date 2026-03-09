<h1 align="center">
  <img src="https://img.icons8.com/ios-filled/50/FFFFFF/home.png" height="22px" />
  Struktura Danych Nowoczesnego Domu Jednorodzinnego w Firebird SQL
</h1>

Projekt przedstawia kompletną relacyjną strukturę danych dla nowoczesnego, inteligentnego domu jednorodzinnego, zaprojektowaną z myślą o zarządzaniu energią, komfortem, bezpieczeństwem oraz automatyką budynkową. System obejmuje m.in. obsługę urządzeń, czujników, pomieszczeń, fotowoltaiki, magazynu energii, taryf, reguł decyzyjnych oraz danych historycznych i prognostycznych.

Modelowany obiekt to parterowy dom jednorodzinny z garażem w bryle, zamieszkały przez 4 osoby, o powierzchni około 100 m², zlokalizowany w Tomaszowie Bolesławieckim. Projekt został przygotowany jako koncepcyjno–inżynierski model danych pod przyszłą implementację systemu EMS (*Energy Management System*).

---

## <img src="https://img.icons8.com/pastel-glyph/64/FFFFFF/code--v2.png" height="22px" /> Technologie i środowisko

- **Baza danych:** [![Firebird SQL](https://img.shields.io/badge/Firebird-SQL-E76F00?style=flat&logoColor=white)](https://firebirdsql.org/)
- **Środowisko projektowe:** [![IBExpert](https://img.shields.io/badge/IBExpert-DB%20Designer-1D70B8?style=flat&logoColor=white)](https://www.ibexpert.net/)
- **Język zapytań:** [![SQL](https://img.shields.io/badge/SQL-336791?style=flat&logo=postgresql&logoColor=white)](https://en.wikipedia.org/wiki/SQL)
- **Model danych:** [![Model relacyjny](https://img.shields.io/badge/Model-Relacyjny-2E7D32?style=flat&logoColor=white)](https://pl.wikipedia.org/wiki/Relacyjny_model_danych)
- **Podejście projektowe:**  
  - [![Normalizacja](https://img.shields.io/badge/Normalizacja-Baz%20Danych-8E44AD?style=flat&logoColor=white)](https://pl.wikipedia.org/wiki/Normalizacja_bazy_danych) – uporządkowanie struktury tabel i ograniczenie redundancji  
  - [![Klucze główne i obce](https://img.shields.io/badge/Klucze-PK%20%2F%20FK-1565C0?style=flat&logoColor=white)](https://en.wikipedia.org/wiki/Foreign_key) – zachowanie spójności relacyjnej między encjami  
  - [![Projekt koncepcyjny](https://img.shields.io/badge/Projekt-Koncepcyjno--In%C5%BCynierski-AD1457?style=flat&logoColor=white)](#) – realistyczny model danych przygotowany pod wdrożenie EMS  

---

## <img src="https://img.icons8.com/ios-filled/50/FFFFFF/pin.png" height="22px" /> Główne założenia projektu

Projekt został zaprojektowany tak, aby system mógł:

- monitorować zużycie energii elektrycznej w domu,
- rejestrować dane z czujników środowiskowych i bezpieczeństwa,
- obsługiwać instalację fotowoltaiczną oraz magazyn energii,
- zarządzać ogrzewaniem, CWU, chłodzeniem i buforami cieplnymi,
- uwzględniać dynamiczne ceny energii i taryfy,
- przechowywać prognozy pogody i prognozy produkcji PV,
- definiować scenariusze, harmonogramy i reguły działania,
- analizować historię decyzji systemu automatyki.

---

<details>
  <summary><img src="https://img.icons8.com/ios-filled/50/FFFFFF/pin.png" height="22px"/> Funkcje programu / struktury danych (kliknij, aby rozwinąć)</summary>

---

<details>
  <summary><strong><span style="color:#4a90e2">DOM</span></strong> – główna encja projektu (kliknij, aby rozwinąć)</summary>

Tabela nadrzędna całego systemu. Opisuje konkretny budynek i stanowi punkt odniesienia dla większości pozostałych tabel. Przechowuje podstawowe informacje o domu, takie jak nazwa, lokalizacja, współrzędne GPS, powierzchnia, liczba mieszkańców oraz moc przyłączeniowa.

</details>

---

<details>
  <summary><strong><span style="color:#27ae60">BATERIA</span></strong> – konfiguracja magazynu energii (kliknij, aby rozwinąć)</summary>

Tabela opisuje magazyn energii elektrycznej zainstalowany w domu. Zawiera dane techniczne baterii, takie jak pojemność, maksymalna moc ładowania i rozładowania, zakres SoC, sprawność oraz domyślną strategię pracy.

</details>

---

<details>
  <summary><strong><span style="color:#8e44ad">STAN_BATERII</span></strong> – bieżący i historyczny stan baterii (kliknij, aby rozwinąć)</summary>

Przechowuje historyczne i aktualne stany pracy magazynu energii. Zawiera poziom naładowania, moce ładowania i rozładowania, źródło ładowania oraz tryb pracy baterii w czasie.

</details>

---

<details>
  <summary><strong><span style="color:#e67e22">BILANS_ENERGII</span></strong> – zagregowany bilans energetyczny domu (kliknij, aby rozwinąć)</summary>

Tabela analityczna służąca do zapisu bilansu energetycznego w czasie. Pozwala określić, ile energii pobrano z sieci, oddano do sieci, wyprodukowano z PV, przekazano do baterii oraz jaki był całkowity koszt energii.

</details>

---

<details>
  <summary><strong><span style="color:#d35400">BUFOR_CIEPLA</span></strong> – konfiguracja magazynu ciepła (kliknij, aby rozwinąć)</summary>

Opisuje bufory ciepła wykorzystywane w domu, np. bufor CO, CWU lub podłogówki. Zawiera informacje o typie bufora, pojemności, temperaturach granicznych i możliwości wcześniejszego nagrzewania.

</details>

---

<details>
  <summary><strong><span style="color:#16a085">BUFOR_CIEPLA_POMIAR</span></strong> – pomiary temperatury i energii bufora (kliknij, aby rozwinąć)</summary>

Tabela przechowuje historyczne pomiary stanu bufora ciepła. Rejestruje temperaturę oraz szacowaną ilość zgromadzonej energii cieplnej.

</details>

---

<details>
  <summary><strong><span style="color:#2c3e50">TARYFA_STATYCZNA</span></strong> – definicje taryf energetycznych (kliknij, aby rozwinąć)</summary>

Tabela słownikowa zawierająca rodzaje taryf energetycznych, np. G11, G12 lub taryfę dynamiczną. Oddziela definicję taryfy od konkretnych cen godzinowych.

</details>

---

<details>
  <summary><strong><span style="color:#c0392b">CENA_ENERGII_GODZINOWA</span></strong> – godzinowe ceny energii (kliknij, aby rozwinąć)</summary>

Przechowuje ceny zakupu i sprzedaży energii dla konkretnej taryfy, daty i godziny. Tabela jest kluczowa dla optymalizacji kosztów pracy urządzeń oraz strategii ładowania baterii.

</details>

---

<details>
  <summary><strong><span style="color:#2980b9">CWU_POMIAR</span></strong> – parametry ciepłej wody użytkowej (kliknij, aby rozwinąć)</summary>

Służy do rejestrowania temperatury i zużycia ciepłej wody użytkowej. Pozwala analizować komfort domowników oraz zapotrzebowanie energetyczne systemu CWU.

</details>

---

<details>
  <summary><strong><span style="color:#9b59b6">REGULA</span></strong> – logika decyzyjna systemu (kliknij, aby rozwinąć)</summary>

Tabela przechowuje reguły sterujące inteligentnym domem. Definiuje warunki logiczne, akcje do wykonania oraz aktywność danej reguły.

</details>

---

<details>
  <summary><strong><span style="color:#f39c12">HISTORIA_DECYZJI</span></strong> – historia decyzji automatyki (kliknij, aby rozwinąć)</summary>

Rejestruje decyzje podejmowane przez system na podstawie reguł. Umożliwia analizę działania automatyki, audyt oraz debugowanie zachowania systemu.

</details>

---

<details>
  <summary><strong><span style="color:#f1c40f">INSTALACJA_PV</span></strong> – konfiguracja instalacji fotowoltaicznej (kliknij, aby rozwinąć)</summary>

Opisuje parametry techniczne instalacji PV, takie jak moc, liczba paneli, orientacja, kąt nachylenia, model falownika oraz data uruchomienia.

</details>

---

<details>
  <summary><strong><span style="color:#3498db">PRODUKCJA_PV</span></strong> – rzeczywiste pomiary produkcji PV (kliknij, aby rozwinąć)</summary>

Przechowuje dane historyczne dotyczące pracy instalacji fotowoltaicznej. Rejestruje chwilową moc DC i AC oraz energię dzienną i całkowitą.

</details>

---

<details>
  <summary><strong><span style="color:#7f8c8d">PROGNOZA_PV</span></strong> – prognozowana produkcja energii z PV (kliknij, aby rozwinąć)</summary>

Tabela zawiera prognozowaną moc i energię produkowaną przez instalację fotowoltaiczną. Umożliwia planowanie pracy urządzeń i optymalizację autokonsumpcji.

</details>

---

<details>
  <summary><strong><span style="color:#e74c3c">LICZNIK_GLOWNY</span></strong> – konfiguracja głównego licznika energii (kliknij, aby rozwinąć)</summary>

Opisuje główny licznik energii elektrycznej domu. Przechowuje dane identyfikacyjne, moc przyłączeniową oraz typ taryfy.

</details>

---

<details>
  <summary><strong><span style="color:#34495e">ZUZYCIE_DOMU</span></strong> – zużycie energii całego budynku (kliknij, aby rozwinąć)</summary>

Tabela rejestruje rzeczywiste zużycie energii elektrycznej przez cały dom. Zawiera dane o mocy chwilowej, imporcie i eksporcie energii.

</details>

---

<details>
  <summary><strong><span style="color:#5d6d7e">PROGNOZA_POGODY</span></strong> – dane prognostyczne pogody (kliknij, aby rozwinąć)</summary>

Przechowuje prognozowane warunki pogodowe dla domu, m.in. temperaturę, wilgotność, zachmurzenie, wiatr, opady i nasłonecznienie. Dane te są wykorzystywane np. do prognoz PV i sterowania ogrzewaniem.

</details>

---

<details>
  <summary><strong><span style="color:#1abc9c">DOMOWNIK</span></strong> – użytkownicy domu (kliknij, aby rozwinąć)</summary>

Opisuje mieszkańców domu i ich podstawowe cechy, takie jak imię, wiek i typ domownika. Tabela wspiera modelowanie obecności, komfortu i profilu zużycia energii.

</details>

---

<details>
  <summary><strong><span style="color:#2e86c1">POMIESZCZENIE</span></strong> – opis pomieszczeń domu (kliknij, aby rozwinąć)</summary>

Przechowuje informacje o wszystkich pomieszczeniach w budynku. Obejmuje nazwę, typ, powierzchnię, wysokość, kubaturę, klasę izolacji oraz priorytet komfortu.

</details>

---

<details>
  <summary><strong><span style="color:#5dade2">OKNO_KOMFORTU</span></strong> – warunki komfortu w czasie (kliknij, aby rozwinąć)</summary>

Definiuje przedziały czasowe oraz dopuszczalne zakresy temperatury i wilgotności w konkretnych pomieszczeniach. Wykorzystywane do sterowania komfortem cieplnym.

</details>

---

<details>
  <summary><strong><span style="color:#d35400">OGRZEWANIE_CONFIG</span></strong> – konfiguracja systemu ogrzewania (kliknij, aby rozwinąć)</summary>

Opisuje logiczną konfigurację źródeł ogrzewania w domu, np. pompy ciepła i grzałki elektrycznej. Stanowi podstawę dla dalszego sterowania systemem grzewczym.

</details>

---

<details>
  <summary><strong><span style="color:#2874a6">URZADZENIE</span></strong> – urządzenia działające w domu (kliknij, aby rozwinąć)</summary>

Centralna tabela opisująca wszystkie urządzenia w systemie, np. AGD, urządzenia grzewcze, wykonawcze i energochłonne. Zawiera parametry techniczne, sposób sterowania, interfejs komunikacyjny i priorytety działania.

</details>

---

<details>
  <summary><strong><span style="color:#af7ac5">GRUPA_URZADZEN</span></strong> – grupowanie urządzeń (kliknij, aby rozwinąć)</summary>

Tabela służy do logicznego grupowania urządzeń w kategorie, np. AGD, ogrzewanie czy oświetlenie. Ułatwia raportowanie i sterowanie całymi grupami.

</details>

---

<details>
  <summary><strong><span style="color:#f5b041">TYP_URZADZENIA</span></strong> – słownik typów urządzeń (kliknij, aby rozwinąć)</summary>

Przechowuje klasyfikację urządzeń według ich funkcji i charakteru pracy. Ułatwia rozszerzanie systemu oraz porządkowanie danych.

</details>

---

<details>
  <summary><strong><span style="color:#ec7063">ZUZYCIE_URZADZENIA</span></strong> – zużycie energii przez urządzenia (kliknij, aby rozwinąć)</summary>

Tabela zawiera zagregowane dane o zużyciu energii przez poszczególne urządzenia w określonych przedziałach czasu. Umożliwia analizę energochłonności sprzętu.

</details>

---

<details>
  <summary><strong><span style="color:#7d3c98">URZADZENIE_PARAMETR</span></strong> – parametry konfiguracyjne urządzeń (kliknij, aby rozwinąć)</summary>

Tabela typu key–value przechowująca dodatkowe parametry urządzeń, które są zmienne, opcjonalne lub zależne od modelu. Pozwala elastycznie rozszerzać konfigurację urządzeń.

</details>

---

<details>
  <summary><strong><span style="color:#5d6d7e">PLAN_STEROWANIA</span></strong> – zaplanowane akcje dla urządzeń (kliknij, aby rozwinąć)</summary>

Przechowuje konkretne zaplanowane działania sterujące dla urządzeń: moment startu, stopu, preferowane źródło energii oraz szacowany koszt wykonania.

</details>

---

<details>
  <summary><strong><span style="color:#c0392b">HARMONOGRAM_URZADZENIA</span></strong> – powtarzalne zasady pracy urządzeń (kliknij, aby rozwinąć)</summary>

Tabela opisuje cykliczne harmonogramy działania urządzeń w wybranych dniach tygodnia i godzinach. Może uwzględniać np. minimalny poziom naładowania baterii.

</details>

---

<details>
  <summary><strong><span style="color:#2980b9">SCENARIUSZ_DNIA</span></strong> – scenariusze funkcjonowania domu (kliknij, aby rozwinąć)</summary>

Definiuje gotowe tryby działania domu, np. dzień roboczy, weekend lub nieobecność. Scenariusze wpływają na urządzenia, reguły i harmonogramy.

</details>

---

<details>
  <summary><strong><span style="color:#16a085">SCENARIUSZ_OBECNOSC</span></strong> – model obecności domowników (kliknij, aby rozwinąć)</summary>

Opisuje przedziały czasowe obecności lub nieobecności mieszkańców w ramach konkretnego scenariusza dnia. Dane te wpływają na komfort, bezpieczeństwo i oszczędność energii.

</details>

---

<details>
  <summary><strong><span style="color:#2e4053">CZUJNIK</span></strong> – konfiguracja czujników (kliknij, aby rozwinąć)</summary>

Centralna tabela warstwy pomiarowej. Opisuje wszystkie czujniki w systemie: środowiskowe, energetyczne i bezpieczeństwa, wraz z ich lokalizacją, jednostką i interfejsem komunikacji.

</details>

---

<details>
  <summary><strong><span style="color:#5dade2">ODCZYT_CZUJNIKA</span></strong> – historyczne odczyty z czujników (kliknij, aby rozwinąć)</summary>

Przechowuje właściwe dane pomiarowe zbierane z czujników w czasie. Umożliwia analizę zmian parametrów środowiskowych, bezpieczeństwa i zużycia energii.

</details>

---

<details>
  <summary><strong><span style="color:#7f8c8d">TYP_CZUJNIKA</span></strong> – słownik rodzajów czujników (kliknij, aby rozwinąć)</summary>

Tabela definiuje typy czujników, np. temperatura, ruch, zalanie czy dym. Zapewnia spójność opisu i interpretacji danych pomiarowych.

</details>

---

<details>
  <summary><strong><span style="color:#e74c3c">STREFA_ALARMOWA</span></strong> – logiczne strefy systemu alarmowego (kliknij, aby rozwinąć)</summary>

Opisuje podział domu na strefy alarmowe, np. garaż, parter czy ogród. Ułatwia grupowanie zdarzeń oraz konfigurację systemu bezpieczeństwa.

</details>

---

<details>
  <summary><strong><span style="color:#8e44ad">STREFA_CZUJNIK</span></strong> – przypisanie czujników do stref alarmowych (kliknij, aby rozwinąć)</summary>

Tabela łącznikowa przypisująca konkretne czujniki do wybranych stref alarmowych. Dzięki niej system wie, które sensory należą do której strefy.

</details>

---

<details>
  <summary><strong><span style="color:#34495e">ZDARZENIE_ALARMOWE</span></strong> – historia zdarzeń alarmowych (kliknij, aby rozwinąć)</summary>

Przechowuje log zdarzeń alarmowych wykrytych w domu. Rejestruje czas, strefę, czujnik, typ zdarzenia, status obsługi i dodatkowy opis.

</details>

</details>

---

## <img src="https://img.icons8.com/ios-filled/50/FFFFFF/brick-wall.png" height="22px" /> Cechy projektu

- modularna i czytelna struktura relacyjna,
- logiczne powiązania między encjami,
- przygotowanie pod EMS i automatykę domową,
- możliwość rozbudowy o nowe urządzenia, czujniki i scenariusze,
- obsługa danych historycznych oraz prognostycznych,
- możliwość dalszej implementacji algorytmów optymalizacyjnych.

---

## <img src="https://img.icons8.com/ios-filled/50/FFFFFF/folder-invoices--v1.png" height="22px" /> Przykładowe obszary modelu danych

Projekt obejmuje między innymi:

- zarządzanie domem i jego parametrami,
- zarządzanie pomieszczeniami i komfortem,
- rejestrację danych z czujników,
- sterowanie urządzeniami,
- bilans energetyczny,
- fotowoltaikę i magazyn energii,
- system alarmowy,
- scenariusze i reguły automatyki,
- prognozy pogody i prognozy PV.

---

<details>
  <summary><img src="https://img.icons8.com/ios-filled/50/FFFFFF/camera.png" height="22px"/> Podgląd projektu domu (kliknij, aby rozwinąć)</summary>

Poniżej znajdują się materiały graficzne powiązane z projektem:

### Schemat relacyjny bazy danych
![Schemat relacyjny bazy danych](NOWOCZESNY_DOM.FDB.png)

### Rzut i wizualizacja przykładowego nowoczesnego domu
![Przykładowy schemat nowoczesnego domu](Przykładowy_schemat_nowoczesnego_domu100m2.jpg)

</details>
