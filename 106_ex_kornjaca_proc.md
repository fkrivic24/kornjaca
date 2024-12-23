# Programiranje s kornjačom

"Kornjača" je alat za učenje programiranja koji se koristio u jeziku Logo još kasnih 1960-ih. Python uključuje ovaj alat kao standardni modul. Koncept je sljedeći: postoji kornjača koju možemo kretati kroz dvodimenzionalni prostor s jednostavnim naredbama poput "odi naprijed 50 piksela" ili "skreni lijevo za 45 stupnjeva". Kornjača se najčešće prikazuje kao strelica, a vrlo je lako s njom početi eksperimentirati i interaktivno.

Kornjača živi u modulu `turtle`, a prozor u kojem je vizualizacija se može pokrenuti s naredbom `turtle.showturtle()`. Osnovne naredbe za kretanje kornjače su `turtle.forward(distance)`, gdje je `distance` udaljenost za koju će se kornjača pomaknuti u smjeru u kojem je orijentirana, te `turtle.left(angle)` i `turtle.right(angle)`, gdje je `angle` broj stupnjeva za koji će kornjača promijeniti orijentaciju u lijevo ili desno. Kada program pišemo u datoteku, dobro dođe i naredba `turtle.done()` koja pokreće kornjaču kao aplikaciju koja čeka korisnički unos. Ovo je korisno i već ako samo želimo spriječiti da se prozor zatvori čim se program završi, kao što smo to ranije radili naredbom `input("Pritisni <enter> za kraj")`.

Također, možemo modificirati i razne postavke kornjače kao što su brzina crtanja, debljina i boja linije i oblik kornjače. U ovom smislu najvažniji su nam brzina kornjače kako bi lakše mogli vidjeti što se zbiva i debljina linije, kako bi lakše vidjeli što je kornjača nacrtala. Brzinu kornjače možemo postaviti s funkcijom `turtle.speed(n)` gdje je n broj od jedan do deset, a jedan je najsporije kretanje. Debljinu linije možemo postaviti s funkcijom `turtle.width(n)` gdje je n broj piksela.

Imajući to na umu, probajte implementirati program u kornjači koji crta kvadrat. Pokušajte napisati ovaj program prije no što nastavite čitati skriptu!

Najjednostavnije rješenje ovog problema je kako slijedi:

Ovo rješenje radi što treba, ali je strukturalno loš program. Prvi problem je što se dvije posve iste naredbe, odnosno naredbe koje se sastoje od poziva na iste funkcije s istim parametrima, se u paru ponavljaju četiri puta. Kada krenemo na ovaj način ponavljati naredbe, to je signal da možemo iskoristiti petlju. Također, ulazne vrijednosti za izvršenje programa se ponavljaju u samim pozivima za funkcije, što ih čini težim za uočiti i mijenjati, a tako je i lakše napraviti grešku u kôdu. Na primjer, kada bismo željeli promijeniti dužinu stranice, morali bismo to učiniti na četiri različita mjesta u programu, a riječ je o banalno jednostavnom primjeru. Pogledajmo rješenje koje te vrijednosti izdvaja ranije kako bi njima bilo lakše baratati te koristi petlju za izbjegavanje ponavljanja kôda.

Na ovaj način jasno su nam odvojeni podaci i proces samog crtanja, a proces crtanja ne samo da izbjegava ponavljanje kôda već i omogućuje laku promjenu broja koraka kornjače. To ne samo da nam olakšava promjene ovog programa, već nam i otvara nove mogućnosti.

Ponavljajte petljom i odvojite podatke od logike. Izbjegavajte ponavljanje istih naredbi dupliciranjem. Tome služi petlja. Također, odvajajte podatke od logike jer ih je tako lakše kasnije saznati i mijenjati. Navedeno olakšava održavanje i promjene te umanjuje mogućnost pogrešaka u većim programima.


U postavkama sada možemo namjestiti crtanje bilo kojeg pravilnog poligona. Pogledajmo primjere za trokut i heksagon.

```python
# Kornjača i trokut
n_steps = 3  # broj koraka koji će kornjača napraviti
turn_angle = 120  # stupanj pod kojim se skreće
for _ in range(n_steps):
    turtle.forward(100)  # dužina stranice
    turtle.left(turn_angle)
{#fig:turtle_triangle width="50%"}

# Kornjača i heksagon
n_steps = 6  # broj koraka koji će kornjača napraviti
turn_angle = 60  # stupanj pod kojim se skreće
for _ in range(n_steps):
    turtle.forward(100)  # dužina stranice
    turtle.left(turn_angle)
{#fig:turtle_heksagon width="50%"}
```

Dapače, ukoliko razmislimo i prisjetimo se malo rudimentarne trigonometrije (ili pronađemo formule online), stupanj skretanja možemo automatski izračunati iz broja stranica, čime više ni tu vrijednost nije potrebno namještati. Dorađeni program, koji se u potpunosti bazira na poligonima i napustio je koncept kvadrata, vidimo niže.

Program je sada postavljen da crta pravilne poligone bilo kojeg broja stranica. Ima međutim još jedan problem: unosi su postavljeni tako da čim je veći broj stranica, tim je veći i poligon, ukoliko sami ne promijenimo dužinu stranice. Navedeno je vidljivo i u ovome tekstu u razlici u veličini između prikazanog trokuta i heksagona, a kako raste broj stranica, tako raste i veličina. Na slici vidimo poligon koji je pobjegao s ekrana.


Što ukoliko želimo da nam svi poligoni imaju istu veličinu bez ručnog podešavanja dužine stranice? Obzirom da su nam ulazne vrijednosti u kôdu izdvojene, navedeno možemo promijeniti trigonometrijskim izračunima radije no promjenama u toku programa. Možemo, na primjer, postaviti da je radijus, a ne dužina stranice, osnovna ulazna vrijednost. Dužinu stranice možemo zatim izračunati. Pogledajmo kako.

```
import math

# Izračun dužine stranice iz radijusa
radius = 100  # radijus poligona
n_steps = 6  # broj stranica
side_length = 2 * radius * math.sin(math.pi / n_steps)  # dužina stranice
turn_angle = 360 / n_steps  # kut za skretanje
for _ in range(n_steps):
    turtle.forward(side_length)  # crtanje strane
    turtle.left(turn_angle)
```
Tako smo izračunali dužinu stranice na temelju radijusa, i svi poligoni sada imaju istu veličinu bez potrebe za ručnim podešavanjem.
