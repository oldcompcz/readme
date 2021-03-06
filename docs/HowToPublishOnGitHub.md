# Jak publikovat GIT repozitář na GitHubu

Účelem tohoto jednoduchého návodu je ukázat, jak publikovat a pracovat s 
repozitářem na github.com.

## Proč publikovat projekt?

Cílem zveřejnění projektu na github.com je zejména:

* Vybudovat si komunitu uživatelů a poskytovat dokumentaci, informace o 
releasech a fixech.
* Spolupráce s dalšími vývojáři, kteří mohou do projektu přispívat.

GitHub umožňuje zdarma vytváření neomezeného množství veřejných repozitářů. 
Je rovněž možné vytvářet privátní repozitáře, které vidí jen vlastník a případně
omezená komunita vývojářů. Privátní repozitáře s komunitou max. do 3 vývojářů 
jsou na GitHubu zdarma.  

Alternativy ke GitHubu jsou bitbucket.org nebo gitlab.com.

## Založení účtu na github.com

Pokud ještě nemáte založený účet, tak navštivte stránku github.com a založte si
ho. Ujistěte se, že ve svém profilu máte uvedený stejný mail, který jste si
nastavili při instalaci gitu na svůj počítač. Tento mail je součástí commit 
messages a github podle něj identifikuje uživatele, který commit provedl. Pokud
nenajde účet s příslušným mailem, tak nedokáže u commitů zobrazit správného
uživatele.

## Založení repozitáře na github.com a práce s ním

### Vypublikování repozitáře

Nyní máme účet na github.com a předpokládejme, že na svém počítači máme projekt
TestProject, který chceme zveřejnit na GitHubu.  

* Na stránce GitHubu vpravo nahoře klikneme na ikonu `+` a zvolíme 
`New repository`
* Zvolíme název "TestProject" a popis. Repozitář zvolíme veřejný a potvrdíme.
* Repozitář je založený a GitHub nám napovídá jak můžeme pokračovat.

Přepneme se do projektu na počítači. Pokud pracujete ve Windows, tak klikněte do
adresáře pravým tlačítkem myši a zvolte `Git Bash Here`. Otevře se vám příkazová 
řádka bashe. Nastavíme cestu ke vzdálenému repozitáři a pushneme projekt na 
server. (myuser v adrese nahraďte svým přihlašovacím jménem)

```
git remote add origin https://github.com/myuser/TestProject.git
git push -u origin master
```

Nyní máme lokální projekt vypublikovaný a propojený se vzdáleným repozitářem na 
GitHubu.

### Klonování repozitáře

Pokud si sedneme k jinému počítači, kde projekt nemáme a chtěli bychom si ho 
stáhnout (naklonovat), tak to provedeme následujícím příkazem

```
git clone https://github.com/myuser/TestProject.git 
```

### Lokálni versus vzdálený repozitář

Další práce na projektu je podobná jako když jsme měli pouze lokální repozitář
na počítači. V projektu provádíme změny, změněné soubory přidáváme do stage a 
commitujeme tak jak jsme zvyklí `git add .`, `git commit -m "Commit message"`.  

Pokud chceme naše lokální commity poslat na server, tak nejprve stáhneme 
případné změny ze vzdáleného serveru k sobě.

```
git pull
```

Pokud nějaké vzdálené změny byly, tak se provede merge. Následně můžeme naše 
změny poslat na server.

```
git push
```   

## Read me

V žádném projektu by neměl chybět read me soubor, kde byste měli napsat základní
informace o projektu. Minimálně by měl read me obsahovat jak projekt stáhnout, 
sestavit a spustit, případně také popis použití.  

Read me soubror může být buď klasický textový `README.txt` nebo modernější, 
formátovaný ve značkovacím jazyce Mark Down `README.md`. Přehled značek 
Mark Down naleznete 
[zde](https://guides.github.com/features/mastering-markdown/).
Pokud máte rádi emotikony, tak si v Mark Down také 
[přijdete na své](https://github.com/ikatyang/emoji-cheat-sheet/blob/master/README.md).  

Mark Down je na GitHubu preferovaný a lze ho používat všude kde něco píšete. 
V issues, v komentářích ale třeba i v informacích o sobě ve svém profilu. 

## Vytváření release

V každém projektu jednou za čas dojdete do fáze, kdy si řeknete, že byl učiněn 
dostatečný pokrok a zároveň je nyní program stabilní a mohli byste tedy nyní
vydat nový release. Vydat na GitHubu release je jednoduché a používají se
pro tento účel takzvané tagy.  

Přepneme se do projektu na počítači. Pokud pracujete ve Windows, tak klikněte do
adresáře pravým tlačítkem myši a zvolte `Git Bash Here`. Otevře se vám příkazová 
řádka bashe. Následujícím příkazem si vylistujeme seznam už existujících tagů v
našem projektu. Nyní tam zřejmě žádné nebudou.

```
git tag
```

Vytvoříme tedy nový tag Release-1.0.0. První číslice je tzv. major číslo, které
se mění, když byla v projektu nějaká velmi zásadní změna. Druhé číslo verze je
tzv. minor číslo, které budeme měnit, když přibylo několik vlastností. Poslední
číslo je tzv. revize, nebo číslo buildu. Obvykle se mění když jsme jen 
zafixovali nějaké chyby.

```
git tag "Release-1.0.0"
```

Zkontrolujeme nyní zda se nám tag v projektu vytvořil `git tag` a můžeme ho 
vypublikovat na GitHub.

```
git push origin "Release-1.0.0"
```

Když se přepnete v prohlížeči do svého projektu na GitHubu, tak v horní liště 
projektu uvidíte `1 release`. Klikněte na něj a uvidíte svůj tag. Vpravo nahoře
je tlačítko `Draft a new release`. Když na něj kliknete, tak můžete vytvořit 
popis release. Vyberte tag, který reprezentuje release a vyplňte release title.
Následně můžete napsat libovolné informace o release. Je možné používat Mark 
Down formátovací značky. Zároveň můžete k release přiložit zkompilované binárky. 
Ty nebudou součástí repozitáře, ale GitHub je bude nabízet uživatelům ke stažení 
v sekci releases. Nakonec vše potvrďte tlačítkem `Publish release`. 

## Issues

Issues jsou nejdůležitějším komunikačním kanálem mezi správcem projektu a 
uživatelem a zároveň mezi vývojáři, pokud jich do projektu přispívá více.
Když někdo ve vašem projektu založí issue, tak to není třeba chápat nijak
špatně. Právě naopak, je to známka toho, že je váš projekt aktivní a že je
kolem něj komunita. Issues je možné a vhodné onálepkovat. Například:

* bug
* enhancement
* question
* good first issue
* help wanted

Pokud chcete přilákat do svého projektu nové vývojáře, tak můžete připravit
několik lehčích úkolů a onálepkovat je jako `good first issue`. Nebo pokud
řešíte problém, se kterým si nevíte rady, tak můžete založit issue s nálepkou
`help wanted`. Pokud vy, nebo někdo jiný začne na některém issue pracovat,
tak je vhodné issue přiřadit přislušnému uživateli, aby pro ostatní bylo patrné,
že na tomto issue už někdo pracuje.  

Takže se rozhodně nebojte ve svém projektu, nebo v těch cizích používat issues. 
Například pokud v tomto návodu objevíte chybu, tak neváhejte založit issue.

## Pull requesty

Pokud jste správcem projektu, tak máte právo na zápis změn v projektu. Právo
zápisu můžete a nemusíte povolit dalším konkrétním vývojářům. Pokud nějaký
vývojář nemá právo zapisovat do projektu, tak má stále možnost poslat vám 
commit formou pull requestu. Vy si můžete pull request prohlédnout, akceptovat
ho a zařadit do projektu. Nebo můžete autora pull requestu požádat o nějakou
doúpravu. Případně můžete pull request s odůvodněním definitivně zamítnout.  

Pokud byste například chtěli tento návod opravit, doplnit, nebo rozšířit, tak
můžete vytvořit pull request.

## Jak dál

GitHub je úžasná platforma, která nabízí spoustu dalších nástrojů pro spolupráci
na projektech. Na další nástroje snadno narazíte sami - rozhraní GitHubu je 
hodně intuitivní.  

Pokud jste fandové starých počítačů a programujete pro ně, tak se nezapomeňte
nechat přidat ke [skupině OldCompCz na Githubu](https://github.com/oldcompcz).
Cílem je propojení vývojářů a uživatelů software na GitHubu tak, aby o sobě 
věděli a mohli si pomáhat. Jako žádost o přidání jednoduše vytvořte issue v 
projektu readme.

Můžete pokračovat návodem [Podepisujte své commity](HowSignCommits.md).