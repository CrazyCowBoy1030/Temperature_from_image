# Temperature_from_image
TFI jest szybkim sposobem na zmierzenie temperatury spalania.
Narzędzie to działa w przeglądarce i pozwala wczytać obraz, powiększać go, przesuwać widok oraz estymować temperaturę wybranego miejsca na podstawie średniego koloru z obszaru 5x5 pikseli.
 White balance podaje się jednym polem w kelwinach, a aplikacja przelicza tę wartość na przybliżony kolor bieli RGB używany do kompensacji pomiaru.

Co robi aplikacja
Aplikacja umożliwia lokalne wczytanie obrazu bez backendu i analizę pikseli przez Canvas API dostępne w przeglądarce.
 Po kliknięciu punktu liczy średnią z obszaru 5x5 px, dzięki czemu wynik jest stabilniejszy niż dla pojedynczego piksela.

Temperatura nie jest mierzona bezpośrednio jak w kamerze termowizyjnej, tylko estymowana przez dopasowanie barwy zmierzonego obszaru do modelu temperatury barwowej ciała czarnego.
 Oznacza to, że wynik ma charakter orientacyjny, szczególnie dla zwykłych zdjęć RGB i scen z dominującym światłem odbitym.

Najważniejsze funkcje
Wczytywanie zdjęcia z dysku lokalnego przez przeglądarkę.

Zoom kółkiem myszy oraz przesuwanie obrazu na canvasie.

Pomiar temperatury na podstawie uśrednienia z obszaru 5x5 px.

Jedno pole WB [K], na przykład 5000 K, zamiast ręcznych mnożników R/G/B.

Podgląd pozycji punktu, aktualnego zoomu i jakości dopasowania.

Ograniczenia
To narzędzie nie zastępuje kamery termicznej, ponieważ zwykłe zdjęcie RGB nie zawiera pełnej informacji o promieniowaniu cieplnym obiektu.
 Wynik zależy od balansu bieli, charakterystyki sensora, kompresji obrazu, oświetlenia sceny i tego, czy obiekt rzeczywiście emituje światło zgodne z przybliżeniem ciała czarnego.

Najlepsze efekty można uzyskać dla obiektów gorących, świecących lub takich, dla których kolor silnie koreluje z temperaturą.
 Dla zwykłych powierzchni w temperaturze pokojowej wynik należy traktować wyłącznie jako wizualną lub względną estymację.

Wymagania
Do uruchomienia wystarczy nowoczesna przeglądarka internetowa obsługująca Canvas API i odczyt danych pikseli przez getImageData().
 Aplikacja działa lokalnie jako pojedynczy plik HTML i nie wymaga instalacji bibliotek ani serwera.

Jak uruchomić
Pobierz plik HTML z aplikacją.

Otwórz plik w przeglądarce.

Wczytaj obraz z dysku lokalnego.

Ustaw WB [K], na przykład 5000.

Przybliż interesujący fragment obrazu.

Kliknij punkt, który chcesz zmierzyć.

Sterowanie
Kółko myszy — zoom.

Prawy przycisk myszy lub spacja + przeciąganie — przesuwanie widoku.

Lewy klik — pomiar temperatury w wybranym miejscu.

Przycisk Dopasuj lub Resetuj widok — powrót do widoku całego obrazu.

Interpretacja wyniku
Aplikacja pokazuje środek pomiaru, obszar 5x5 px, średnie RGB, wartość WB, skorygowane RGB oraz temperaturę dopasowaną do modelu.
 Pokazywany błąd dopasowania informuje, jak dobrze kolor badanego obszaru pasuje do koloru przewidywanego przez model temperatury barwowej.

Mniejszy błąd oznacza lepsze dopasowanie, ale nie gwarantuje poprawnej temperatury fizycznej obiektu.
 Nawet dobre dopasowanie może być mylące, jeśli obraz był mocno obrabiany albo kolor wynika głównie z oświetlenia zewnętrznego.

Jak działa white balance w tej wersji
Pole WB [K] przyjmuje temperaturę barwową źródła światła lub ustawionego balansu bieli, na przykład 5000 K.
 Kod zamienia tę wartość na przybliżony kolor RGB, korzystając z popularnej aproksymacji temperatury barwowej do RGB, a następnie tworzy współczynniki kompensacji dla kanałów.

To uproszczenie jest wygodniejsze niż ręczne wpisywanie trzech mnożników, ale nadal pozostaje tylko przybliżeniem, ponieważ rzeczywiste współczynniki white balance zależą od konkretnego sensora i przetwarzania obrazu.

Struktura działania algorytmu
Wczytanie obrazu do canvas i pobranie danych pikseli.

Kliknięcie punktu i wyznaczenie obszaru 5x5 px wokół środka.

Uśrednienie wartości R, G i B z tego obszaru.

Wyliczenie przybliżonych współczynników kompensacji z pola WB [K].

Przeszukanie zadanego zakresu temperatur i znalezienie temperatury, której kolor najlepiej pasuje do zmierzonego koloru.

Pokazanie najlepszego dopasowania i błędu.

Przykładowy workflow
Jeżeli zdjęcie było wykonane przy balansie bieli 5000 K, można pozostawić WB [K] = 5000 i kliknąć rozgrzany obszar obrazu.
 Następnie warto porównać kilka punktów i obserwować, czy temperatura rośnie lub maleje względnie pomiędzy obszarami, zamiast ufać bezwzględnej wartości pojedynczego pomiaru.

Kiedy wynik ma większy sens
Wynik jest bardziej użyteczny, gdy analizowany obiekt jest bardzo gorący, świeci sam z siebie albo kolor emisji jest realnie związany z temperaturą.
 W praktyce aplikacja może być bardziej przydatna do porównań względnych między fragmentami obrazu niż do absolutnej metrologii temperatury.

Możliwe rozwinięcia
Lupa pikselowa wokół kursora.

Heatmapa temperatury dla całego obrazu.

Eksport pomiarów do CSV.

Kalibracja względem punktów referencyjnych o znanej temperaturze.

Uśrednianie większych obszarów, na przykład 7x7 lub 9x9 px, gdy obraz jest zaszumiony.

Uwagi końcowe
Aplikacja została zaprojektowana jako wygodne narzędzie eksperymentalne do analizy obrazu w przeglądarce, a nie jako certyfikowany przyrząd pomiarowy.
 Jeśli celem jest rzeczywisty pomiar temperatury z dużą dokładnością, potrzebna jest kamera termiczna albo skalibrowany układ pyrometryczny.
