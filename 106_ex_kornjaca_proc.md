## Programiranje s kornjačom

\"Kornjača\" je alat za učenje programiranja koji se koristio u jeziku
Logo još kasnih 1960-ih. Python uključuje ovaj alat kao standardni
modul. Koncept je sljedeći: postoji kornjača koju možemo kretati kroz
dvodimenzionalni prostor s jednostavnim naredbama poput \"odi naprijed
50 piksela\" ili \"skreni lijevo za 45 stupnjeva\". Kornjača se najčešće
prikazuje kao strelica, a vrlo je lako s njom početi eksperimentirati i
interaktivno.

![Interaktivan rad s kornjačom](turtle_idle){#fig:turtle_idle
width="\\textwidth"}

Kornjača živi u modulu `turtle`{.python}, a prozor u kojem je
vizualizacija se može pokrenuti s naredbom
`turtle.showturtle()`{.python}. Osnovne naredbe za kretanje kornjače su
`turtle.forward(distance)`{.python}, gdje je `distance`{.python}
udaljenost za koju će se kornjača pomaknuti u smjeru u kojem je
orijentirana, te `turtle.left(angle)`{.python} i
`turtle.right(angle)`{.python}, gdje je `angle`{.python} broj stupnjeva
za koji će kornjača promijeniti orijentaciju u lijevo ili desno. Kada
program pišemo u datoteku, dobro dođe i naredba `turtle.done()`{.python}
koja pokreće kornjaču kao aplikaciju koja čeka korisnički unos. Ovo je
korisno i već ako samo želimo spriječiti da se prozor zatvori čim se
program završi, kao što smo to ranije radili naredbom
`input("Pritisni <enter> za kraj")`{.python}.

Također, možemo modificirati i razne postavke kornjače kao što su brzina
crtanja, debljina i boja linije i oblik kornjače. U ovom smislu
najvažniji su nam brzina kornjače kako bi lakše mogli vidjeti što se
zbiva i debljina linije, kako bi lakše vidjeli što je kornjača nacrtala.
Brzinu kornjače možemo postaviti s funkcijom `turtle.speed(n)`{.python}
gdje je je n broj od jedan do deset, a jedan je najsporije kretanje.
Debljinu linije možemo postaviti s funkcijom `turtle.width(n)`{.python}
gdje je n broj piksela.

Imajući to na umu probajte implementirati program u kornjači koji crta
kvadrat. Pokušajte napisati ovaj program prije no što nastavite čitati
skriptu!

Najjednostavnije rješenje ovog problema je kako slijedi:

![Rezultat programa Kornjača i kvadrat
1](turtle_square){#fig:turtle_square width="50%"}

Ovo rješenje radi što treba, ali je strukturalno loš program. Prvi
problem je što se dvije posve iste naredbe, odnosno naredbe koje se
sastoje od poziva na iste funkcije s istim parametrima, se u paru
ponavljaju četiri puta. Kada krenemo na ovaj način ponavljati naredbe to
je signal da možemo iskoristiti petlju. Također, ulazne vrijednosti za
izvršenje programa se ponavljaju u samim pozivima za funkcije što ih
čini težim za uočiti i mijenjati, a tako je i lakše tako napraviti
grešku u kôdu. Na primjer, kada bismo željeli promijeniti dužinu
stranice, morali bismo to učiniti na četiri različita mjesta u programu,
a riječ je o banalno jednostavnom primjeru. Pogledajmo rješenje koje te
vrijednosti izdvaja ranije kako bi njima bilo lakše baratati te koristi
petlju za izbjegavanje ponavljanja kôda.

Na ovaj način jasno su nam odvojeni podaci i proces samog crtanja, a
proces crtanja ne samo da izbjegava ponavljanje kôda već i omogućuje
laku promjenu broja koraka kornjače. To ne samo da nam olakšava promjene
ovog programa, već nam i otvara nove mogućnosti.

::: important
Ponavljajte petljom i odvojite podatke od logike Izbjegavajte
ponavljanje istih naredbi dupliciranjem. Tome služi petlja. Također,
odvajajte podatke od logike jer ih je tako lakše kasnije saznati i
mijenjati. Navedeno olakšava održavanje i promjene te umanjuje mogućnost
pogrešaka u većim programima.
:::

U postavkama sada možemo namjestiti crtanje bilo kojeg pravilnog
poligona. Pogledajmo primjere za trokut i heksagon.

::: pythonp
Kornjača i trokut \# \... n_steps = 3 \# broj koraka koji će kornjača
napraviti turn_angle = 120 \# stupanj pod kojim se skreće \# \...
:::

![Rezultat programa Kornjača i
trokut](turtle_triangle){#fig:turtle_triangle width="50%"}

::: pythonp
Kornjača i heksagon \# \... n_steps = 6 \# broj koraka koji će kornjača
napraviti turn_angle = 60 \# stupanj pod kojim se skreće \# \...
:::

![Rezultat programa Kornjača i
heksagon](turtle_hex){#fig:turtle_heksagon width="50%"}

Dapače, ukoliko razmislimo i prisjetimo se malo rudimentarne
trigonometrije (ili pronađemo formule *online*), stupanj skretanja
možemo automatski izračunati iz broja stranica čime više ni tu
vrijednost nije potrebno namještati. Dorađeni program, koji se u
potpunosti bazira na poligonima i napustio je koncept kvadrata vidimo
niže.

Program je sada postavljen da crta pravilne poligone bilo kojeg broja
stranica. Ima međutim još jedan problem, unosi su postavljeni tako da
čim je veći broj stranica, tim je veći i poligon ukoliko sami ne
promijenimo dužinu stranice. Navedeno je vidljivo i u ovome tekstu u
razlici u veličini između prikazano trokuta i heksagona, a kako raste
broj stranica, tako raste i veličina. Na slici
[5](#fig:turtle_big_poly){reference-type="ref"
reference="fig:turtle_big_poly"} vidimo poligon koji je pobjegao s
ekrana.

![Interaktivan rad s kornjačom](turtle_big_poly){#fig:turtle_big_poly
width="75%"}

Što ukoliko želimo da nam svi poligoni imaju istu veličinu bez ručnog
podešavanja dužine stranice? Obzirom da su nam ulazne vrijednosti u kôdu
izdvojene, navedeno možemo promijeniti trigonometrijskim izračunima
radije no promjenama u toku programa. Možemo, na primjer, postaviti da
je radijus, a ne dužina stranice, osnovna ulazna vrijednost. Dužinu
stranice možemo zatim izračunati. Pogledajmo kako.

Dodali smo samo formulu za izračun dužine stranice iz radijusa. Na ovaj
način kad crtamo poligone istog radijusa, oni ne rastu s brojem
stranica. Dok ovaj kod prikazuje svrsishodnu upotrebu trigonometrije u
programiranju, za potrebe učenja programiranja nam je ovdje najvažnije
da smo dobrom strukturom, odnosno korištenjem petlje i jasnim odvajanjem
ulaznih podataka od samih naredbi, razvili općenit postupak crtanja
poligona, a krenuli smo od koncepta kvadrata. Sada kad smo razvili
postupak, crtanje poligona bi mogli definirati kao zasebnu funkciju čime
bi omogućili crtanje poligona kroz jednu naredbu. Obzirom da je ovo vrlo
važno za programiranje iole kompleksnijih programa, naučiti ćemo to
kasnije u ovom tekstu, ali pogledajmo prvo još koji primjer koji se
koristi znanjem koje smo već usvojili.

Također, vrijedi spomenuti da smo ovdje prikazali samo najosnovnije
mogućnosti kornjače pa ćemo se na to još vratiti, ali ako netko želi
eksperimentirati s kornjačom više neka se referira na [službenu
dokumentaciju](https://docs.python.org/3.8/library/turt le.html).
Čitanje dokumentacije i traženje odgovora *online* je i dobra vježba jer
se radi o nezaobilaznom koraku prilikom programiranja, a na čitanje
dokumentacije se treba naviknuti (i to pogotovo kada se radi o službenoj
dokumentaciji jer je često pisana tehničkim jezikom) pa je dobro početi
s vježbom.

Također, s kornjačom se mogu raditi kojekakve čudesne i uglavnom
beskorisne stvari. Programiranje radi umjetnosti. Ukoliko smo Python
instalirali prema uputama iz ove skripte i u komandnoj liniji pokrenemo
naredbu `python -m turtledemo`{.python} pokrenuti će nam se grafičko
sučelje koje prikazuje napredne primjere i mogućnosti kornjače. Ukoliko,
na primjer, iz padajućeg izbornika \"examples\" odaberemo primjer
\"bytedesign\" te kliknemo na \"start\", dobiti ćemo sliku
[6](#fig:turtle_examples){reference-type="ref"
reference="fig:turtle_examples"}.

![Napredni primjeri mogućnosti s
kornjačom](turtle_examples){#fig:turtle_examples width="\\textwidth"}

Ipak, ovi primjeri su uglavnom napredni i koriste mnoge koncepte koje
još nismo objasnili pa u njih nećemo sada dublje ulaziti. Ovdje su
spomenuti jer prikazuju mogućnost programiranja radi kreativnog procesa
radije no pragmatične vrijednosti programa.
