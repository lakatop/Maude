# Maude

Riesenie pozostava z 3 suborov ([atm.maude](atm.maude), [bank.maude](bank.maude) a [test.maude](test.maude)) ktore implementuju moduly ATM, BANK a TEST.

## ATM
Atm sa sklada z cisla (`AtmNumber`), zoznamu definovanych bank (`Banks`) a zostatku (`ATMBalance`).
Atm si uchovava stavy o pocte jednotlivych bankoviek (100, 200, 500, 1000, 2000 CZK) z ktorych je potom pocitany celkovy zostatok a takisto su pomocou nich definovane operacie, ktore moze uzivatel na Atm vykonavat:
<ul>
  <li>Skontrolovat stav uctu - checkAccountBalance</li>
  <li>Ziskat informacie o svojom ucte - getAccountInfo</li>
  <li>Vlozit peniaze - deposit</li>
  <li>Vybrat peniaze withdraw</li>
</ul>

Pre jednotlive bankovky su vytvorene samostatne sorty ktore si udrziavaju ich stav (`M100`, `M200`, `M500`, `M1000` a `M2000`). K ich poctom sa vieme dostat pomocou `getATMBalance<sort>` operacie. Doplnenie penazi do bankomatu je realizovane pomocou operacie `insertMoney`.

Pri ukazani zostatku na ucte alebo ziskani informacii o ucte je potrebne mat vlozenu kartu, automat a zadat spravny pin. To je reprezentovane vstupnymi argumentami operacii : `Card`, `CardPin`, `Atm`.
Pri operacii withdraw a deposit je to iste co vyssie ale zaroven je potrebne zadat sumu ktoru chceme vybrat/vlozit - `Money`. Vysledok je potom reprezentovany statusom - `Status`.

## BANK
Banka sa sklada z nazvu banky (`BankName`) a uctov zaregistrovanych v danej banke (`BankAccounts`). 
Modul BANK v sebe uchovava rozne banky (`Banks`). Do jedotlivych bank vieme pridat novych klientov (`addAccount`) a vyriadovat jednotlive transakcie `withdraw` a `deposit`. Zaroven ma na starosti validaciu karty pomocou pinu zadaneho uzivatelom - `validateCard`.

## TEST
Tento modul pozostava z testovacich scenarov pre rozne situacie. Najpr je vytvorene celkove prostredie - banky, ucty v jednotlivych bankach a ich karty, bankomat a rozne sumy. Potom nasleduje 6 rozlicnych scenarov:<br />
Korektny vyber penazi - `testWithdraw`<br />
Korektne vlozenie penazi na ucet - `testDeposit`<br />
Ziskanie zostatku na ucte - `testCheckAccountBalance`<br />
Ziskanie informacii o ucte - `testAccountInfo`<br />
Neplatny vyber z uctu pre nedostatok penazi - `testInvalidWithdraw`<br />
Neplatny vklad na ucet pre nespravny pin kod ktory nepresiel validaciou - `testInvalidDeposit`<br />

Na zaklade vysledku jednotlivych testov dostaneme odpovedajuce statusy ako vysledok.

## Splnenie zadania
V tejto kapitole len spomeniem ako cim su splnene jednotlive poziadavky ktore boli zadane:<br />
`state: number of available banknotes for each value (100, 200, 500, 1000, 2000)` - riesene pomocou uchovavania si jednotlivych sortov `M100`, `M200`, `M500`, `M1000` a `M2000`a definovania operacii na nich.<br />
`- card validation` - riesene v module `BANK` pomocou `validateCard` pri jednotlivych operaciach.<br />
`- checking account balance` - riesene pomocou operacie `testCheckAccountBalance`<br />
`- cash withdrawal` - riesene pomocou operacie `withdraw` definovanej v module `Atm` a jednotlivych withdraw operacii v module `Bank`<br />
`- cash deposit` - riesene pomocou operacie `deposit` definovanej v module `Atm` a jednotlivych deposit operacii v module `Bank`<br />
`- retrieving account information from the central database of a respective bank` - riesene pomocou operacie `testAccountInfo`<br />
`- reading user PIN from keyboard` - riesene pomocou vstupneho argumentu(`CardPin`) pri jednotlivych operaciach ktore to vyzaduju<br />
`document your solution` - this document
`prepare some test cases (scenarios, inputs)` - riesene v module [TEST](#test)
