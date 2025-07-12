Případová studie: Dynamický přepočet jednotkové ceny v Shopify

Souhrn

Implementace na míru vytvořeného řešení pro Shopify, které dynamicky vypočítává a zobrazuje jednotkovou cenu produktu (cenu za kus). Funkce se v reálném čase aktualizuje při změně produktové varianty, čímž poskytuje zákazníkům transparentní informaci o ceně pro snazší porovnání.

Problém

Klient potřeboval u produktů prodávaných v baleních o různých velikostech (např. 25 ks, 21 ks, 19 ks) zobrazovat přepočtenou cenu za jeden kus. Standardní zobrazení v Shopify ukazovalo pouze celkovou cenu za balení. Cílem bylo zajistit, aby se jednotková cena okamžitě a spolehlivě aktualizovala vždy, když si zákazník zvolí jinou variantu (velikost balení).

Řešení

Vzhledem ke specifické architektuře použitého motivu bylo finální řešení navrženo jako soběstačný modul přímo v šabloně product.liquid. Tento přístup zaručuje stabilitu a nezávislost na problematických externích skriptech.

Řešení se skládá ze tří hlavních částí vložených na jedno místo:



Datová vrstva: Pomocí jazyka Liquid je na serveru vytvořen JavaScriptový objekt window.variantMetafields. Tento objekt obsahuje data z vlastního metapole (custom.pocet_kusu_v_baleni) a mapuje je na konkrétní ID variant, čímž je zpřístupní pro další zpracování v prohlížeči.

HTML a CSS: Do stránky je vložen jednoduchý HTML prvek (<div class="unit-price"></div>) sloužící jako cíl pro zobrazení vypočtené ceny. Veškerý vzhled tohoto prvku, včetně jeho správného umístění na nový řádek, je definován v bloku <style>, který je součástí modulu.

Logika: Izolovaný JavaScriptový skript naslouchá na standardní událost change na produktovém formuláři. Po výběru varianty spustí funkci updateUnitPrice. Tato funkce získá potřebná data, provede výpočet (cena varianty / počet kusů), výsledek naformátuje jako českou měnu a dynamicky ho vloží do cílového HTML prvku. Skript také zajišťuje správné zobrazení pro výchozí variantu při prvním načtení stránky.

