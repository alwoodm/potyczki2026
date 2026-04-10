# Potyczki Młodych Adminów: Finał 2026

## Wstęp

Tegoroczne zadania będą testem nie tylko znajomości Kubernetes i Ranchera, ale też zdolności do zachowania poczytalności w obliczu absurdalnych wymagań. Witamy w piekle na ziemi, jakim są darmowe praktyki w firmie-krzak stereotypowego polskiego przedsiębiorcy!

Powodzenia!

---

### System oceniania
Najlepiej napisany program i najlepiej wdrożony system jest tykającą bombą bez odpowiedniej dokumentacji. Nikt nie lubi jej pisać, ale jest kluczowa dla łatwości późniejszego utrzymywania i efektywnej współpracy - a także do sprawdzania zadań! Dlatego udokumentuj wszystkie zadania, co najmniej oznaczając te które zostały wykonane, bo **tylko te zostaną sprawdzone**. Wymagany sposób na przedstawienie dokumentacji to utworzenie repozytorium GitHub w formie forka tego repozytorium.

Opisz kroki wykonane w celu realizacji zadania, szczególnie lokalizacje zasobów, użyte opcje i komendy - nie musisz tego robić bardzo dokładnie, ale w razie wątpliwości będą one działać na twoją korzyść. Na przykład jeśli zadanie nie zostało do końca wykonane, ale znacząca część kroków jest opisana poprawnie, zaliczymy za to częściowe punkty. Albo jeśli zadanie zostało wykonane, ale nie w sposób jakiego oczekiwaliśmy, to opis będzie kluczem do uzyskania za nie punktów. To, co nie jest opisane, a nie jest oczywiste z interfejsu Ranchera, będzie rozstrzygane na twoją niekorzyść! Wszystkie zadania wykonujemy na klastrze **potyczki**.


**Wstęp:**
Gratulacje! Zostałeś przyjęty na prestiżowy, acz bezpłatny staż w prężnie rozwijającym się przedsiębiorstwie wielobranżowym Krzak-Pol S.A. Główny informatyk, Pan Wiesio, wyjechał na ryby w Bieszczady i zapomniał zabrać telefonu. Prezes Janusz właśnie wpadł do serwerowni z wypiekami na twarzy i listą pilnych zadań. 

Twoim narzędziem pracy jest nowoczesny klaster K3s z panelem Rancher. Prezes nie znosi sprzeciwu, a każda sekunda to dla niego utrata zysków. Uratuj firmę, a może dostaniesz referencje! Czas ucieka. Powodzenia!

---

## CZĘŚĆ 1: Pierwsze kroki w Krzak-Polu

### Misja 1: "Młody, w internecie nas nie widać!" (10 pkt)
> *"Młody, szwagier założył firmę i ma stronę. My nie mamy! Zrób mi tu szybko taką wizytówkę, żeby ładnie wyglądało w internecie. Tylko nie kupuj żadnych domen, bo na to nie mamy budżetu. Wymyśl coś za darmo, przecież znasz te swoje sztuczki!"*

**Zadania do wykonania:**
* [1 pkt] Utwórz nową przestrzeń nazw (Namespace) o nazwie `krzak-pol-web`.
* [3 pkt] Uruchom w niej Deployment z obrazem `nginx:alpine` działający w 2 replikach.
* [2 pkt] Wystaw aplikację wewnątrz klastra za pomocą serwisu typu `ClusterIP`.
* [4 pkt] Skonfiguruj zasób `Ingress` tak, aby strona była dostępna z zewnątrz pod darmowym adresem domenowym rozwiązującym się na IP klastra (np. z wykorzystaniem usług `nip.io` lub `sslip.io`).

### Misja 2: "Panie, gdzie są moje faktury?!" (10 pkt)
> *"Wczoraj wrzuciłem skany najważniejszych faktur na ten nowy serwer. Potem Wiesio wyciągnął wtyczkę od serwera, bo potrzebował gniazdka do odkurzacza. Włączam dzisiaj i pusto! Jakie efemeryczne kontenery?! Zainstaluj mi ten cały system Długi Róg (Longhorn), o którym pisali w gazecie biznesowej, i zrób tak, żeby moje pliki tam siedziały na twardo!"*

**Zadania do wykonania:**
* [3 pkt] Zainstaluj system storage Longhorn na swoim klastrze (możesz wykorzystać wbudowane mechanizmy Ranchera).
* [3 pkt] Utwórz PersistentVolumeClaim (PVC) o wielkości 2GB w przestrzeni nazw `krzak-pol-magazyn`, używając `storageClassName: longhorn`.
* [4 pkt] Wdróż dowolny prosty Pod/Deployment (np. `busybox` z pętlą `sleep`), który będzie miał podmontowany ten wolumen pod ścieżkę `/dane_prezesa`.

### Misja 3: "Awaria systemu księgowego" (10 pkt)
> *"Wiesio przed wyjazdem wdrażał nowy system do wyliczania premii. Niestety, księgowa Grażynka dzwoni, że nic nie działa. Kod jest już wrzucony do systemu (Namespace: `ksiegowosc-prod`), ale rzuca jakimiś błędami. Napraw to, bo jutro wypłaty i muszę wiedzieć, ile komu uciąć z pensji!"*

**Zadania do wykonania:**
Organizator wdrożył zepsute zasoby w przestrzeni `ksiegowosc-prod`. Twoim zadaniem jest znalezienie i poprawienie wszystkich błędów w definicjach YAML.
* [5 pkt] Napraw błędy uniemożliwiające poprawne uruchomienie Poda aplikacji.
* [5 pkt] Napraw błędy konfiguracyjne w zasobie Service, tak aby ruch prawidłowo trafiał do aplikacji.

### Misja 4: "Atak hakerów i RODO" (10 pkt)
> *"Dzwonił szwagier, mówi, że konkurencja Pędzi-Wiatr wykradła komuś dane! A w telewizji straszyli jakimiś karami za RODO. Młody, musimy się odgrodzić! Zainstaluj to nowe zabezpieczenie, NeuVector. Zrób tak, żeby z tej naszej nowej strony nikt nie mógł wejść do systemu księgowego. Księgowość to świętość!"*

**Zadania do wykonania:**
* [5 pkt] Zainstaluj system bezpieczeństwa NeuVector na klastrze.
* [5 pkt] Skonfiguruj w NeuVector regułę sieciową (Network Rule), która jawnie zablokuje wszelki ruch z przestrzeni `krzak-pol-web` do przestrzeni `ksiegowosc-prod`.

### Misja 5: "Black Friday u Janusza" (10 pkt)
> *"Młody, wykupiłem baner na lokalnym portalu i zaraz ruszy do nas fala klientów! Podkręć tę naszą wizytówkę, niech działa na pełnych obrotach. Ale uwaga! Zrób limity na ten system księgowy z Misji 3. Grażynka jak zacznie liczyć te premie, to znowu wywali korki w całej serwerowni, a ja nie będę płacił za prąd!"*

**Zadania do wykonania:**
* [3 pkt] Przeskaluj wizytówkę firmy (`krzak-pol-web` z Misji 1) do 5 replik.
* [7 pkt] Zabezpiecz serwer przed księgowością: nałóż na Deployment z przestrzeni `ksiegowosc-prod` twarde limity zasobów: Limit CPU = `150m`, Limit RAM = `128Mi`.

---

## CZĘŚĆ 2: Prezes wchodzi na wyższe obroty

### Misja 6: "Strona premium i magiczna kłódeczka" (15 pkt)
> *"Młody, wizytówka działa, ale szwagier się śmieje, że w przeglądarce pisze "Niezabezpieczona". Chcę mieć tam zieloną kłódeczkę! Poza tym, widziałem fajny tekst na stronie u konkurencji. Wiesio mi tłumaczył, że w tym Kuber-coś-tam można zrobić taki mały, początkowy kontener, który przed startem głównej strony skopiuje plik z zewnątrz. Zrób to!"*

**Zadania do wykonania:**
* [5 pkt] Zmodyfikuj wizytówkę: dodaj `InitContainer`, który za pomocą prostego polecenia (np. `wget` lub `curl`) pobierze plik `index.html` z dowolnego zewnętrznego adresu (możesz użyć np. surowego pliku z GitHub/Gist).
* [5 pkt] Podepnij współdzielony wolumen typu `emptyDir` między InitContainerem a głównym Nginxem, aby główny serwer mógł wyświetlić pobrany plik.
* [5 pkt] Wygeneruj własny certyfikat (Self-Signed), zapisz go jako `Secret` typu TLS w klastrze i podepnij pod Ingress z Misji 1, zapewniając dostęp po HTTPS.

### Misja 7: "Baza klientów na wieki wieków" (10 pkt)
> *"Grażynka ma bazę prestiżowych klientów w Excelu. Każą nam to przenieść do jakiejś prawdziwej bazy, żeby było 'stanowo'. I najważniejsze: jak znowu Wiesio wyrwie kable, to dysk z danymi ma zostać nieruszony! Jakieś zasady Retain czy coś, nie znam się na tym, ale ma działać!"*

**Zadania do wykonania:**
* [4 pkt] Utwórz własną klasę pamięci (`StorageClass`) o nazwie `krzak-longhorn-retain`, bazującą na zainstalowanym Longhornie, wymuszającą politykę `reclaimPolicy: Retain`.
* [6 pkt] W nowej przestrzeni `klienci-premium` wdróż instancję bazy danych (np. MariaDB, PostgreSQL) używając zasobu `StatefulSet`. Użyj `volumeClaimTemplates` skonfigurowanego do użycia nowej klasy pamięci.

### Misja 8: "Pendrive Wiesia" (10 pkt)
> *"Znalazłem pendrive w biurku Wiesia. Mówił, że to nowy Panel Kierownictwa. Próbowałem to odpalić z tego pliku YAML, ale wszystko świeci na czerwono. Grażynka płacze, ja nie mam podglądu w zyski. Napraw ten kod, niech to ruszy!"*

**Zadania do wykonania:**
W głównym katalogu tego repozytorium znajdziesz plik `pendrive.yaml`. Wdróż go w swoim klastrze, a następnie zdiagnozuj i napraw błędy, które uniemożliwiają jego działanie.
* [5 pkt] Napraw błędy związane z RBAC (InitContainer nie ma uprawnień do odpytywania API Kubernetes).
* [5 pkt] Napraw błędy konfiguracyjne powodujące nieskończone restarty Poda (`CrashLoopBackOff`).

### Misja 9: "Paranoja i Twierdza Krzak-Pol" (10 pkt)
> *"Wiesio ściągał najnowsze oprogramowanie (tag 'latest') i potem w piątek po południu pół firmy nie działało! Skonfiguruj ten cały NeuVector tak, żeby już NIKT nie mógł wdrażać niczego z 'latest'. A ta baza danych dla prestiżowych klientów z Misji 7? Zablokuj do niej dostęp WSZYSTKIM, poza naszą stroną internetową z Misji 6!"*

**Zadania do wykonania:**
* [5 pkt] Utwórz regułę **Admission Control** w NeuVector, która zablokuje wdrażanie jakichkolwiek podów korzystających z obrazów z tagiem `:latest`. (Upewnij się, że w innych misjach używasz konkretnych wersji!).
* [5 pkt] Utwórz zasób `NetworkPolicy` w K8s dla przestrzeni `klienci-premium`, który zablokuje cały ruch do bazy danych, z wyjątkiem połączeń przychodzących wyłącznie z namespace'u `krzak-pol-web`.

### Misja 10: "Elitarny serwer dla Prezesa" (5 pkt)
> *"Młody, kupiłem dzisiaj ekskluzywny serwer do naszej klastrowej farmy. Niemiec płakał, jak sprzedawał! Nazwałem go "Złoto". Wiem, że fizycznie wygląda tak samo jak stary i stoi w tej samej obudowie, ale to nowa jakość! Baza danych (Misja 7) ma działać TYLKO na tym "złotym" serwerze! I pamiętaj, że jak sprzątaczka odkurza w serwerowni, to musi działać bez przerw przynajmniej 80% kopii naszej wizytówki z Misji 6!"*

**Zadania do wykonania:**
* [1 pkt] Oznacz węzeł w swoim klastrze specjalną etykietą `tier=zloto`. 
* [2 pkt] Zmodyfikuj zasób bazy danych z Misji 7, dodając w nim wymóg uruchamiania (twarde **Node Affinity**) wyłącznie na węźle z przypisaną nową etykietą.
* [2 pkt] Utwórz zasób `PodDisruptionBudget` dla wizytówki, wymuszając nieprzerwaną pracę co najmniej 4 instancji (replik) aplikacji podczas operacji administracyjnych.


