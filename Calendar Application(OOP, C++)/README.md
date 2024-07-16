# Aplikace "Kalendář", Autor: Byaliauski Yahor

## Zadání

Tato semestrální práce patří do kategorie interaktivních aplikací. Vaším cílem je vytvořit aplikaci, kterou bude uživatel interaktivně ovládat (např. pomocí příkazů na standardním vstupu). Případné parametry aplikace se nesnažte definovat přímo v kódu (a to ani pomocí konstant). Umístěte je do konfiguračních souborů (jednoho nebo více), které váš program bude načítat.

Vaším cílem je implementovat aplikaci pro správu kalendářů a událostí v nich.

Implementujte následující funcionality:

1. Kalendář musí zobrazovat alespoň denní, týdenní a měsíční přehled událostí.

2. U událostí chceme evidovat alespoň následující informace: název události, datum a čas, trvání, místo, účastníky, tagy a textovou poznámku. V rámci své implementace můžete přidat další zajímavé atributy (př. účast: povinná, přesunutelná, volitelná, …).

3. Události mohou být jednorázové nebo opakující se. Umožněte definovat frekvenci opakování alespoň na úrovni dní.

4. Kalendář musí umožnit vyhledávat události podle jednotlivých atributů a to včetně kombinací obsahující spojky "a zároveň" a "nebo" (př. události před 23.1.2022 a zároveń v Praze, …).

5. Umožněte exportování a importování událostí. Exportovat lze i výběr definovaný vyhledáváním.

6. Kalendář nesmí umožnit kolizi, v případě kolize musí umožnit najít nejbližší volný termín nebo přesunout událost (je-li to možné). Alternativně můžete povolit max. počet kolizí (př. 24 kolizí pro učebnu, podle počtu studentů, které v ní mohou být, …), nelze však kolize ignorovat.

Kde lze využít polymorfismus? (doporučené)

* zobrazení kalendáře: denní, týdenní, měsíční, …

* strategie řešení kolizí: nalezení nejbližšího možného termínu, přesun max. X jiných událostí na volné sloty, …

* formáty exportovaných událostí: proprietární, iCalendar, CSV, …

* uživatelské rozhraní: konzole, ncurses, SDL, OpenGL (různé varianty), …

* druhy událostí (předem si rozmyslete, zda ve vašem případě se jedná o polymorfismus) 

## Specifikace

Rozhraním aplikace je konzole. Uživatel muže zadavat různé příkazy pro řízení aplikace. Souhrn všech příkazů vola příkaz /help:

- /help - souhrn všech příkazů
- /get calendar year - zobrazit kalendář na tento rok
- /get calendar [month] - zobrazit kalendář na konkretní měsíc tento rok
- /set event - vytvořit událost

> Povinné parametry události: 
> - Název
> - Datum
> - Frekvence(Jednorazová, každoroční)

> Nepovinné parametry události:
> - Čas a trvání události
> - Místo trvání
> - Tagy události
> - Textová poznámka
> - Povinnost/Nepovinnost (defoltně událost je povinná)
> - Účastnící

- /get events - zobrazit všechny události
- /find event - najít a zobrazit události podle nějakých parametrů
> Zadavaní povinných parametrů může mít nasledující tvar: 
> - Name: Birthday
> - Frequency: (výbrat mezi 1-jednor., 2-každor.)
> - Datum: 23.06.2005
> - Time: 10:30
> - Place: Park | Club 
> - Tag: #party | #music
>
> Lze využit logickou spojku '|'(or). Uživatel může nechat nejaký atribut prázdným, jestli nechce vyhledávat podle toho atributu 
- /set id - nastavit nový atribut události
- /del id - zahodit událost
- /del event all - zahodit všechny události
- /time - zobrazit aktuální čas
- /date - zobrazit aktuální datum
- /clear - vymazat terminál
- /exit - ukončit aplikaci

Aplikace má své uložistě, kam uloží události. Rozhraní je barevně odlišeno. Barevný text je zde pro snazší čitelnost.

## Polymorfismus

Polymorfismus byl použit v hierarchii tříd "CAttribute", která má potomky "CDate", "CTime", "CParticipant", "CPlace", "CTag", "CText" a "CName", a v hierarchii tříd "CCalendar", potomkami které jsou třídy "CCalendarDay", "CCalendarMonth" a "CCalendarYear".

Potomci tříd-atributů mají s rodičem společný destruktor a metody setAttr, která umožňuje nastavit novou hodnotu atributu, inputAttr, která zobrazí interaktivní menu pro příslušný atribut, a metodu empty, která zkontroluje, zda je atribut prázdný.

Potomci třídy CCalendar mají společný destruktor a metodu printCalendar, která vytiskne kalendář odpovídajícího typu pro každou třídu. Navíc třída CCalendarYear pro výpis ročního kalendáře používá metodu printCalendar pro každý měsíc v roce. Vstupní parametry pro každý kalendář se liší.

## Ovladání

Pro kompilaci projektu musíte vyplnit příkaz "make all".
