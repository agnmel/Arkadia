# Arkadia
Skrypty, które tu publikuję, nie były tworzone z myślą o wygodnym graniu od razu po instalacji. Nie zawierają mapy, dostosowanych kolorów ani fontu. Ilość wprowadzonych bindów, podświetlonych kluczy i artefaktów również jest niekompletna i wymaga uzupełnienia. Są jednak według mnie dobrą podstawą do wygodnego rozszerzenia we własnym zakresie. Mogą również posłużyć jako źródło przykładów, jak napisać dany fragment skryptu w programie CMUD. Można je określić jako sporą modyfikację paczki udostępnionej przez Zurwena, od której zaczynałam je pisać. Niektóre sygnały dźwiękowe zapożyczyłam z paczki stworzonej przez Cerdina. Starałam się, aby każda funkcjonalność mieściła się w odrębnym folderze, ale pomimo tego istnieją wyjątki, które reagują np. z funkcjami umieszczonymi w *obsłudze okna kondycji*. Kod nie zawiera żadnych fragmentów zapisanych w jezyku programowania Lua.
## Instalacja
1. Ściągnij i rozpakuj repozytorium
2. Stwórz nową sesję w programie CMUD. *Title* nie ma znaczenia, wybierz coś jeszcze nie stworzonego (np. Skrypty_Agi). Host: arkadia.rpg.pl, Port 23. W zakładce *Package Files* zwróć uwagę na utworzoną ścieżkę (*Path*) - w następnych krokach wrzucisz tam dwa foldery
3. Otworz sesje offline
4. W *Options* -> *General* -> *Protocols* dodaj poniższe linie (całość powinna prezentować się w taki sposób):
```
Core 1
Char 1
Room 1
Comm 1
IRE.Composer 1
Objects 1
Mail 1
```
5. W *Settings* -> *File* -> *Import XML* wybierz plik `Skrypty_Agi.xml` z rozpakowanego repozytorium
6. Otwórz folder sesji (czyli wcześniejszą wypisaną ścieżkę w kreatorze sesji) i dodaj do niego folder /Dzwieki z rozpakowanego repozytorium oraz stwórz pusty folder /Logi
7. Wybierz *File* -> *Reconnect* aby połączyć się z grą. Po zalogowaniu się powinno pojawić się dodatkowe okno kondycji osób na lokacji
## Zawartość
### Atak
Przycisk `A`/`AW`/`AWR`/`AWRP` (atak, wskazanie, rozkaz, przedstawienie) znajdujący się na panelu wpływa na działanie aliasu `z [kogo]` dodając wcześniej wymienione komendy.

Wymagania: `alias z zabij` ustawiony w grze.

Uwagi: Podczas pisania listu (bądź innej interakcji z samotną literą "z" jako pierwszą w komendzie) polecam zmienić przycisk na sam atak. Dzięki temu skrypt nie doda niepożądanych komend.
### Bind
Klawisz `F12` reagujący na sugestywny tekst w grze typu "Ktoś przeciska się przez krzaki". Treść znajdująca się pod tym przyciskiem wyświetli się w głównym oknie oraz na panelu poniżej. Po wciśnięciu bindu jego zawartość zostaje skasowana.

Uwagi: Aby dodać kolejny bind, który jest jedną komendą, wystarczy w triggerze napisać: `dodaj_bind "treść bindu"`. Jeśli jednak bind ma zawierać więcej komend, polecam skorzystać ze wzoru:
```
#say {%ansi(15) >> F12 - co robi bind}
#key F12 {wykonanie komendy1;wykonanie komendy2;#key f12 {#say {%ansi(15) ">> F12 - Pusty bind"}};F12 = "Pusto!"}
```
### Alias q
Celem komendy `alias q treść komendy` jest utworzenie szybkiego skrótu potrzebnego w tymczasowej sytuacji. Dlatego też to, co pod nim się kryje, wyświetlane jest na pasku stanu po pierwszej zmianie tego aliasu.

### Poruszanie się
Zwykłe poruszanie się klawiaturą numeryczną. Przemykanie pod przyciskami `ALT` + `KLAWIATURA NUMERYCZNA`. Podążanie mapy przy użyciu automatycznej komendy `idz [jak?]`, podróży z prowadzącym drużynę, jazdy na wozie oraz przenoszeniu klatki. Cofanie ruchu na mapie poprzez sugestywny tekst w grze. Aby dodać nowy wyjątek cofania ruchu, stwórz trigger z treścią `#move @rewers`

Uwagi: Cofanie działa poprawnie tylko przy poruszaniu się klawiaturą numeryczną.
### Sygnały dźwiękowe
- atak na twoją postać
- próba blokady twojej postaci
- próba blokady innej postaci niż twoja
- walka twojej postaci bez dobytej broni
- nowa poczta
- zmiana kondycji na: złą kondycje, ciężko ranną, ledwo żywą
- pęknięcie broni
- rozpad zbroi
- przełamanie zasłony
- wytrącenie broni z rąk twojej postaci
- dopłynięcie statku do portu
- wskazanie celu
- śmierć

Wymagania: Dodanie folderu /Dzwieki z repozytorium do folderu sesji gry

Uwagi: Polecam przetestowanie działania sygnałów dźwiękowych poprzez komendę: `test_dzwiekow`
### Lokalizowanie postaci na mapie poprzez protokół GMCP
Poprzez komendę `gps_tworz` przypisujesz bądź nadpisujesz istniejące powiązanie między lokacją wskaźnika na mapie a danymi lokacji z protokołu GMCP. Kiedy takie powiązanie zaistnieje, komenda `zlok` przestawi wskaźnik na powiązaną lokacje (jeśli znajduje się gdzieś indziej). Czyli aby komenda `zlok` działa na traktach i miastach twojej mapy, musisz na każdej takiej lokacji wysłać komendę `gps_tworz`, która utworzy bazę danych odpowiadającą twojej mapie.
### Klawisze
- `DIV` stan
- `F1` zabij cel ataku
- `F2` przełamanie zasłoniętego celu ataku
-  `KEY5` zerknij
-  `MULT` k wszystkich
-  `` ` `` przestań zasłaniać
### Wyróżniony tekst innym kolorem niż wysyłany z gry
- Przedmioty magiczne (jasnozielony)
- Klucze do skarbców (pomarańczowy)

Uwagi: Zbiór nie posiada wszystkich możliwych przedmiotów. Jedynie te, które osobiście spotkałam w grze.
### Licznik postępów
Oblicza czas, jaki upłynął między zmianą postępu (albo obecnego czasu po wpisaniu komendy: `postepy` bądź kliknięciu na pasek statusu *Postepy*) a wcześniejszym postępem. Każde wbicie następnego postępu zapisuje go wraz z datą i uzyskanym czasem jako rekord w bazie danych w zmiennej *@postepy*. Komenda: `moje_postepy` wyświetla całą historię uzyskanych postępów w grze.

Wymagania: `opcje wyswietlanie skrocone` lub `opcje wyswietlanie rozszerzone` (Chociaż nie trudno przerobić na przechwytywanie informacji z protokołu GMCP)
### Przeliczanie miedzi na wyższe nominały
Przy ocenie przedmiotu dodaje na końcu zdania informacje przeliczonej wartości. Przykład:
```
Wydaje ci sie, ze jest warta okolo 310 miedziakow = [ 1zl 5sr 10md ]
```
### Okno kondycji
Wyświetla wszystkie osoby oraz NPC znajdujących się na lokacji. Dzieli je na twoją drużynę, wrogów związanych walką oraz pozostałych. Po kliknięciu prawym przyciskiem myszy na imię postaci dostępne są akcje typu: obejrzyj, zaatakuj, porównaj itp. Numeruje osoby znajdujące się w twojej drużynie (wykorzystanie tej numeracji opisałam w segmencie *Zasłanianie i wycofywanie się*)
### Pasek stanów
Graficzne wyświetlanie poziomów stanów (komendy `stan`) wysyłanych protokołem GMCP na pasku powyżej linii komend.
### Ocena ekwipunku
Ocena jakości i wytrzymałości zbroi i broni w skali liczbowej przy ocenie przedmiotu. Przykład:
```
Ciezka zbroja. Chroni dosc dobrze (8/12) przed obrazeniami klutymi i cietymi oraz doskonale (11/12) przed obuchowymi.
```
```
Jak na topor jest bardzo dobrze wywazony (11/14) i wyjatkowo skuteczny (12/14).
```
### Poczta
Wyświetlanie statusu poczty, przeczytanej bądź nie, na pasku powyżej linii komend.
### Rysowanie wyjść
Po wciśnieciu przycisku z obrazkiem kierunków świata skrypt rysuje dostępne kierunki świata plus kierunki w górę i w dół. Kierunki rysowane są poprzez odczytanie ich z protokołu GMCP, ale rysowanie wyzwala się po natrafieniu na sugestywną część w treści lokacji. Przykład:
```
nw
Karczma 'U Rudolfa'.
Jest tutaj piec widocznych wyjsc: dol, poludniowy-wschod, polnoc, gora i wschod.
  |   U
  O - 
    \ D
Masywna marmurowa plansza.
```
### Zasłanianie i wycofywanie się
Klawisze `ALT` + `LICZBA` zasłaniają osobę, do której dana liczba jest przypisana w oknie kondycji. Możliwość zasłoniecia w ten sposób kończy się na dziewiątej osobie. Każda liczba jest obsługiwana również za pomocą aliasu `za [liczba]`, która nie ma wcześniej wspomnianego limitu. Jednocześnie działa obsługa komendy `za [osobe]`, która zadziała w ten sam sposób, czyli zasłaniając wskazaną osobę. Alias nie przeszkadza podczas pisania listów.

Wymagania: `alias za zaslon`

Klawisze `CTRL` + `LICZBA` powodują wycofanie się za osobę, do której dana liczba jest przypisana w oknie kondycji. 
### Zasłony grupowe
Klawisze `F5`, `F6`, `F7`, `F8` odpowiadają kolejno komendzie: `opcje grupa 1, 2, 3, 4`. Po przełączeniu zasłony, na pasku stanu pojawi się zaktualizowana informacja o tym, która opcja jest obecnie włączona. 
### Logi
Zapisywanie wszystkich danych wejściowych dostarczanych przez grę (czyli treści głównego ekranu) w pliku o nazwie *rok*-*miesiąc*-*dzień*.

Wymagania: Folder /Logi w folderze sesji gry.

Uwagi: Pliki będą zawierać ujawnione hasło do konta, jeśli było wpisywane ręcznie **(!!!)** Automatyczne logowanie tego nie powoduje.
## Kontakt
Uwagi oraz ewentualną pomoc możesz kierować do mnie na discordzie: **Aga#7991** 
