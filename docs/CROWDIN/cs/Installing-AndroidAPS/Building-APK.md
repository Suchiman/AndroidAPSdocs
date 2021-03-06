# Sestavení APK

## Vyrobte si místo stažení

**AndroidAPS není k dispozici ke stažení kvůli regulaci zdravotnických zařízení. Je legální vytvořit aplikaci pro své vlastní použití, ale nesmíte dát kopii ostatním! See [FAQ page](../Getting-Started/FAQ.md) for details.**

## ## Důležité poznámky

* Please use **[Android Studio Version 3.5.1](https://developer.android.com/studio/)** or newer to build the apk.
* [Windows 10 32-bit systems](../Installing-AndroidAPS/troubleshooting_androidstudio#unable-to-start-daemon-process) are not supported by Android Studio 3.5.1.

**Configuration on demand** is not supported by the current version of the Android Gradle plugin!

Jestliže vytváření apk selže s chybou "on demand configuration", proveďte následující změnu:

* Otevřete okno Preferences klepnutím na File > Settings (na platformě Mac, Android Studio > Preferences).
* V levé části pak na Build, Execution, Deployment > Compiler.
* Zrušte označení možnosti Configure on demand.
* Klepněte na tlačítko použít nebo OK.

* * *

### Tento článek je rozdělený do dvou částí.

* V části Přehled najdete vysvětlení, které kroky jsou obecně nutné, abyste sestavili soubor APK.
* V části Průvodce krok za krokem najdete snímky obrazovky z konkrétní instalace. Jelikož se Android Studio (vývojové prostředí, které použijeme k sestavení APK) v čase mění velmi rychle, nebudou snímky úplně shodné s vaší instalací, ale určitě vám poskytnou dobrý záchytný bod. Android studio běží na Windows, Linuxu a Mac OS X, a proto mohou být na různých platformách malé rozdíly. Jestliže najdete něco zásadního, co je špatně nebo vám něco chybí, prosím informujte o tom facebookovou skupinu „AndroidAPS users“ nebo použijte Gitter chat [Android APS](https://gitter.im/MilosKozak/AndroidAPS) nebo [AndroidAPSwiki](https://gitter.im/AndroidAPSwiki/Lobby), abychom se na to mohli podívat.

## Přehled

Následují obecné kroky k sestavení souboru APK:

* [Nainstalujte git](../Installing-AndroidAPS/git-install.rst)
* Nainstalujte a nastavte Android Studio.
* Použijte git, abyste si naklonovali zdrojové kódy z centrálního úložiště na Githubu, kam vývojáři umístili nejnovější zdrojové kódy aplikace.
* Otevřete naklonovaný projekt v Android Studiu jako aktivní projekt.
* Sestavete podepsané APK.
* Přeneste podepsané APK do svého telefonu.

## Průvodce krok za krokem

Následuje detailní popis kroků nutných k sestavení souboru APK.

## Nainstalujte git (pokud ho ještě nemáte)

Follow the manual on the [git installation page](../Installing-AndroidAPS/git-install.rst).

## Instalace Android Studio

Následující snímky obrazovky byly převzaty z aplikace Android Studio verze 3.1.3. Vaše obrazovka by mohla vypadat trochu jinak, v závislosti na verzi aplikace Android Studio, kterou používáte. Měli byste však být schopni najít cestu. Pomoc komunity je poskytována například ve [facebookové skupině AndroidAPS](https://www.facebook.com/groups/1900195340201874/) a [na dalších místech](../Where-To-Go-For-Help/Connect-with-other-users.md).

Nainstalujte [Android Studio](https://developer.android.com/studio/install.html) a proveďte úvodní nastavení.

Zvolte "Do not import settings", protože jste tento software zatím nevyužívali.

![Snímek 1](../images/Installation_Screenshot_01.png)

Klikněte na „Next“.

![Snímek 2](../images/Installation_Screenshot_02.png)

Vyberte "Standard" instalaci a klikněte na „Next“.

![Snímek 3](../images/Installation_Screenshot_03.png)

Vyberte si motiv uživatelského rozhraní, který se vám líbí. (V tomto návodu používáme "Intellij". Poté klikněte na tlačítko „Next“. Jedná se pouze o barevný motiv. Můžete si vybrat jakýkoli jiný (např. „Darcula“ pro tmavý režim). Tato volba nemá žádný vliv na sestavení APK.

![Snímek 4](../images/Installation_Screenshot_04.png)

Klikněte na „Next“ v dialogovém okně „Verify Settings“.

![Snímek 5](../images/Installation_Screenshot_05.png)

Emulátor Androidu (pro simulaci telefonu na vašem PC nebo Macu) se pro sestavení APK nepoužívá. Můžete kliknout na „Finish“, abyste dokončili instalaci a odložili četbu dokumentace na později.

![Snímek 6](../images/Installation_Screenshot_06.png)

Android Studio stahuje velké množství softwarových komponent, které používá. Můžete kliknout na tlačítko „Show Details“ pro zobrazení detailů, které ale vůbec nejsou důležité.

![Snímek 7](../images/Installation_Screenshot_07.png)

![Snímek 8](../images/Installation_Screenshot_08.png)

Jakmile jsou stahování dokončena, klikněte na tlačítko „Finish“.

![Snímek 9](../images/Installation_Screenshot_09.png)

* Hurá, hurá, nyní jste dokončili instalaci Android Studia a můžete začít s klonováním zdrojových souborů. Možná je teď vhodná doba na krátkou přestávku?

## Nastavení cesty k nástroji git v předvolbách

### Windows

* Zadejte do Studia umístění souboru git.exe: File - Settings
  
  ![Android Studio - otevřete nastavení](../images/Update_GitSettings1.png)

* „Validity (years)“ můžete ponechat na výchozí hodnotě 25.

* Zvolte správnou cestu: .../Git<font color="#FF0000"><b>/bin</b></font>

* Ujistěte se, že je vybrána metoda aktualizace „Merge“.
  
  ![Android Studio - cesta GIT](../images/Update_GitSettings2a.png)

### Mac

* Pokud instalujete git přes homebrew, není třeba měnit žádné předvolby. Pokud by bylo třeba: Najdete je zde: Android Studio - Preferences.

## Stáhněte si kód a další komponenty

* Použijte klonování gitu v Android Studiu, jak je vidět na snímku níže. Zvolte „Check out project from Version Control“ s „Git“ jako konkrétní verzí správce zdrojových kódů.

![Snímek 10](../images/Installation_Screenshot_10.png)

![Version_Control_Git](../images/Version_Control_Git.png)

Zadejte URL adresu do hlavního úložiště AndroidAPS („https://github.com/MilosKozak/AndroidAPS“) a klepněte na „Clone“.

![Snímek 13](../images/Installation_Screenshot_13.png)

Android Studio začne s klonováním. Neklikejte na „Background“, což by věci nyní pouze zkomplikovalo.

![Snímek 14](../images/Installation_Screenshot_14.png)

Dokončete načtení projektu od správce zdrojových kódů kliknutím na „Yes“, což projekt otevře.

![Snímek 15](../images/Installation_Screenshot_15.png)

Použijte standardní „default gradle wrapper“ a klikněte na „OK“.

![Snímek 16](../images/Installation_Screenshot_16.png)

Přečtěte si okno „Tip of Day“ a kliknutím na „Close“ je zavřete.

![Snímek 17](../images/Installation_Screenshot_17.png)

* Super, máte vlastní kopii zdrojového kódu a jste připraveni na vytvoření Apk.
* Nyní se blížíme k první chybové zprávě. Naštěstí nám Android Studio nabídne její řešení.

Klikněte na „Install missing platform(s) and sync project“, protože Android Studio potřebuje doinstalovat chybějící platformu.

![Snímek 18](../images/Installation_Screenshot_18.png)

Přijměte licenční ujednání zvolením „Accept“ a klikněte na „Next“.

![Snímek 19](../images/Installation_Screenshot_19.png)

Jak již bylo řečeno v dialogovém okně, počkejte, než se stahování dokončí.

![Snímek 20](../images/Installation_Screenshot_20.png)

Nyní je dokončené. Klikněte prosím na tlačítko „Finish“.

![Snímek 21](../images/Installation_Screenshot_21.png)

Aaaach, další chyba. Ale Android Studio navrhuje podobné řešení. Klikněte na „Install Build Tools and sync project“, protože Android Studio potřebuje stáhnout chybějící pomůcky.

![Snímek 22](../images/Installation_Screenshot_22.png)

Jak již bylo řečeno v dialogovém okně, počkejte, než se stahování dokončí.

![Snímek 23](../images/Installation_Screenshot_23.png)

Nyní je dokončené. Klikněte prosím na tlačítko „Finish“.

![Snímek 24](../images/Installation_Screenshot_24.png)

A další chyba k řešení, protože Android Studio potřebuje zase stáhnout chybějící platformu. Klikněte na „Install missing platform(s) and sync project“.

![Snímek 25](../images/Installation_Screenshot_25.png)

Jak již bylo řečeno v dialogovém okně, počkejte, než se stahování dokončí.

![Snímek 26](../images/Installation_Screenshot_26.png)

Nyní je dokončené. Klikněte prosím na tlačítko „Finish“.

![Snímek 27](../images/Installation_Screenshot_27.png)

Klikněte na „Install Build Tools and sync project“, protože Android Studio potřebuje stáhnout chybějící pomůcky.

![Snímek 28](../images/Installation_Screenshot_28.png)

Jak již bylo řečeno v dialogovém okně, počkejte, než se stahování dokončí.

![Snímek 29](../images/Installation_Screenshot_29.png)

Nyní je dokončené. Klikněte prosím na tlačítko „Finish“.

![Snímek 30](../images/Installation_Screenshot_30.png)

Ano, chybové zprávy jsou pryč a první gradle sestavení běží. Možná je čas dát si trochu vody?

![Snímek 31](../images/Installation_Screenshot_31.png)

Android Studio doporučuje aktualizaci systému gradle. **Nikdy neaktualizujte gradle!** Mohlo by to vše zkomplikovat!

Klikněte prosím na „Znovu nepřipomínat pro tento projekt“.

![Snímek 32](../images/AS_NoGradleUpdate.png)

Sestavení zase běží.

![Snímek 33](../images/Installation_Screenshot_33.png)

Ano, první sestavení bylo úspěšné, ale ještě nejsme hotoví.

![Snímek 34](../images/Installation_Screenshot_34.png)

## Vytvořte podepsaný soubor APK

V nabídce vyberte „Build“ a pak „Generate Signed Bundle / APK…“. (Nabídka Android Studio se v září 2018 změnila. Ve starších verzích vyberte nabídku „Build“ a poté „Generate Signed APK“.

Podepsání znamená, že podepíšete vygenerovanou aplikaci, ale digitálním způsobem, jakoby nějakým digitálním otiskem prstu uvnitř samotné aplikace. To je nezbytné, protože Android má pravidlo, že z bezpečnostních důvodů přijme pouze podepsaný kód. Pokud se o toto téma zajímáte, můžete si k tomu víc přečíst [zde](https://developer.android.com/studio/publish/app-signing.html#generate-key), ale Bezpečnost je hluboké a komplexní téma a teď ho nepotřebujete.

![Snímek 39a](../images/Installation_Screenshot_39a.PNG)

V následujícím dialogovém okně vyberte „APK“ místo „Android App Bundle“ a klepněte na tlačítko „Next“.

![Snímek 39b](../images/Installation_Screenshot_39b.PNG)

Zvolte „app“ a klepněte na tlačítko „Next“.

![Snímek 40](../images/Installation_Screenshot_40.png)

Klepněte na „Create new...“ a vytvořte úložiště svých klíčů. Úložiště klíčů v tomto případě není nic jiného než soubor, ve kterém jsou uložené podepisovací informace. Je zašifrované a údaje jsou zabezpečené hesly. Doporučujeme, abyste si ho uložili do své domovské složky a zapamatovali si hesla. Kdybyste však tyto informace ztratili, nebyl by to tak velký problém, protože potom byste prostě museli vytvořit nové úložiště klíčů. Ale lepší je tyto údaje pečlivě uložit.

![Snímek 41](../images/Installation_Screenshot_41.png)

* Vyplňte údaje pro další dialogové okno. 
  * Key store path: je cesta k vašemu úložišti klíčů. **Do not save in same folder as projekt. You must use a different directory!**
  * Políčka s hesly níže jsou pro úložiště klíčů a jsou zdvojená, aby se zabránilo překlepům.
  * Alias je název pro klíč, který potřebujete. Můžete ponechat výchozí, anebo si vybrat jakýkoli jiný název.
  * Políčka s hesly pod tím jsou pro samotný klíč. Jako vždy jsou zdvojená, aby se zabránilo překlepům.
  * You can let the validity at the default of 25 years.
  * You only have to fill out first name and last name but feel free to complete the rest of information. Then click "OK".

![Screenshot 42](../images/Installation_Screenshot_42.png)

Fill in the information of the last dialog in this dialog and click "Next".

![Screenshot 43](../images/Installation_Screenshot_43.png)

Select "full" (or "fullRelease") as flavour for the generated app. Select V1 "Jar Signature" (V2 is optional) and click "Finish". Následující údaje mohou být důležité pro pozdější použití.

* Možnost „Release“ by měla být výchozí volbou pro „Build Type“, možnost „Debug“ je pouze pro vývojáře.
* Vyberte typ sestavení, jaký budete chtít. 
  * full / fullRelease (i.e. recommendations automatically enacted in closed looping)
  * openloop (tj. doporučení pro uživatele s otevřenou smyčkou)
  * pumpcontrol (tj. vzdálené ovládání pumpy bez smyčky)
  * nsclient (tj. zobrazují se data jiného uživatele se smyčkou a lze vkládat záznamy ošetření)

![Snímek 44](../images/Installation_Screenshot_44.png)

V podokně „Event Log“ vidíme, že podepsaný soubor APK byl úspěšně vygenerován.

![Snímek 45](../images/Installation_Screenshot_45.png)

Klikněte na odkaz „locate“ v podokně „Event Log“.

![Snímek 46](../images/Installation_Screenshot_46.png)

## Přeneste soubor APK do telefonu

Objeví se okno správce souborů. Na vašem počítači může vypadat trochu jinak, protože já používám systém Linux. Pokud používáte sytém Windows, otevře se Průzkumník souborů, na platformě Mac OS X to bude Finder. V něm byste měli vidět složku s vygenerovaným souborem APK. Toto bohužel není správné umístění, protože „wear-release.apk“ není podepsaný soubor „app“ APK, který hledáme.

![Snímek 47](../images/Installation_Screenshot_47.png)

Přejděte prosím do složky AndroidAPS/app/full/release a tam vyhledejte soubor „app-full-release.apk“. Přeneste tento soubor do telefonu s Androidem. You can do it on your preferred way, i.e.

* Bluetooth
* cloud upload (Google Drive or other cloud services)
* connect computer and phone by cable 
* by mail (Note that some mail apps do not allow apk attachments, in this case use other transfer method.)

In this example Gmail is used as it is fairly simple. To install the self-signed app you need to allow Android on your smartphone to do this installation even if this file is received via Gmail which is normally forbidden. Pokud použijete jinou metodu, zvolte vhodný postup.

![Snímek 48](../images/Installation_Screenshot_48.png)

V nastavení telefonu je nabídka (instalovat neznámé aplikace), kde lze povolit instalaci APK souborů, které jsem si poslal přes Gmail.

Vyberte možnost „Povolit z tohoto zdroje“. Po instalaci můžete tuto volbu zase zakázat.

![Instalace z neznámých zdrojů](../images/Installation_Screenshot_49-50.png)

Posledním krokem je klepnout na soubor APK, který jsem přijal přes Gmail, a nainstalovat aplikaci. Pokud se APK nechce nainstalovat a máte v telefonu již starší verzi AndroidAPS, pravděpodobně byla podepsaná jiným klíčem – v tom případě musíte starou verzi nejdřív odinstalovat, avšak nezapomeňte předtím exportovat svá nastavení!

Ano, máte to a můžete začít s úvodní konfigurací AndroidAPS (CGM, inzulínová pumpa) atd.

## Identify receiver if using xDrip

[See xDrip page](../Configuration/xdrip#identify-receiver)

## Poradce při potížích

See separate page [troubleshooting Android Studio](../Installing-AndroidAPS/troubleshooting_androidstudio.rst).