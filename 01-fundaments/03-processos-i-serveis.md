# 03 — Processos i serveis de Windows

## Objectiu

Documentar una primera observació pràctica dels processos i serveis de Windows 11 Pro, entenent la diferència entre processos, serveis, estat actual i tipus d'inici.

## 1. Procés vs servei

Un **procés** és una instància d'un programa que s'està executant en un moment concret. Per exemple, quan s'obre Brave, Windows crea un o més processos per executar el navegador i les seves tasques.

Un **servei** és un tipus especial de programa que Windows pot executar en segon pla per oferir una funció del sistema o d'una aplicació. Normalment no té una finestra pròpia ni requereix interacció directa de l'usuari.

La diferència es pot resumir així:

- Una **aplicació** és el programa que l'usuari instal·la o obre, com un navegador o un editor de text.
- Un **procés** és l'execució activa d'una aplicació o d'una part del sistema.
- Un **servei** és un programa dissenyat per funcionar en segon pla i proporcionar una funció contínua o sota demanda.

Els serveis poden funcionar sense interacció directa de l'usuari perquè Windows els administra mitjançant el Service Control Manager. Això permet que funcions com les actualitzacions o la resolució de noms de domini estiguin disponibles encara que no hi hagi cap aplicació oberta a la pantalla.

Exemple conceptual: una aplicació de música oberta pot executar un procés visible per reproduir una cançó; en canvi, un servei de Windows pot comprovar actualitzacions en segon pla sense obrir cap finestra.

## 2. Observació de serveis

Durant la pràctica es va utilitzar:

```text
services.msc
```

No es va modificar, aturar, iniciar ni deshabilitar cap servei.

Es van observar aquests serveis:

### Windows Update

- Estat: En execució
- Tipus d'inici: Automàtic

Windows Update gestiona la detecció, la descàrrega i la instal·lació d'actualitzacions de Windows i d'altres components compatibles. Mantenir el sistema actualitzat és una mesura important de seguretat.

### DNS Client

- Estat: En execució
- Tipus d'inici: Automàtic

DNS Client ajuda Windows a resoldre noms de domini, com ara `example.com`, en les adreces que necessita per comunicar-se a la xarxa. També pot mantenir informació temporal per fer aquestes consultes de manera més eficient.

## 3. Observació de Microsoft Defender

Es va intentar localitzar el servei **Microsoft Defender Antivirus Service**, però no es va trobar amb aquest nom a la llista de serveis del sistema.

Això **no** permet concloure que Microsoft Defender no estigui funcionant. Al laboratori 02 es va identificar **Antimalware Service Executable** com un component relacionat amb Microsoft Defender, fet que mostra que una funcionalitat es pot presentar amb noms diferents segons el lloc o l'eina des d'on s'observa.

La lliçó d'anàlisi és:

> No trobar un element amb el nom esperat no significa que la funcionalitat no existeixi.

En una investigació real, caldria verificar-ho amb altres fonts o eines abans de treure conclusions: documentació del sistema, el Gestor de tasques, l'aplicació de Seguretat de Windows, registres o eines d'inventari autoritzades.

## 4. Estat vs tipus d'inici

L'**estat del servei** indica què està fent ara mateix, per exemple si està en execució o aturat.

El **tipus d'inici** indica com està configurat perquè Windows el gestioni durant l'arrencada o quan sigui necessari. No descriu necessàriament el seu estat en aquell instant.

Exemples conceptuals:

- **En execució + Automàtic**: el servei s'ha iniciat i està funcionant; Windows està configurat per iniciar-lo automàticament.
- **Aturat + Manual**: el servei no s'està executant ara, però pot iniciar-se quan Windows o una aplicació el necessitin.
- **Aturat + Deshabilitat**: el servei està aturat i Windows no el pot iniciar fins que es modifiqui la seva configuració.

Aquests són exemples conceptuals. Durant aquesta pràctica no s'ha modificat cap configuració de servei.

## 5. Relació amb ciberseguretat

Els processos i els serveis són importants en ciberseguretat perquè ajuden a entendre què s'està executant en un sistema. La identificació de processos i de serveis contribueix a establir el comportament normal o *baseline* de l'equip.

Quan apareix una possible anomalia, com un procés desconegut, un servei inesperat o un canvi de consum, cal recollir context abans de decidir si és rellevant. Els serveis també poden estar relacionats amb la persistència, ja que alguns programes es poden configurar per iniciar-se de manera automàtica. Aquesta observació forma part de la investigació d'incidents, però no és una prova per si sola de comportament maliciós.

Un procés desconegut o amb consum elevat **no** és automàticament maliciós. Cal analitzar-lo abans de treure conclusions: identificar-lo, entendre la seva funció, comprovar la seva activitat i contrastar-la amb el comportament normal del sistema.

## 6. Lliçó d'analista

```text
Element observat
→ Què és?
→ Quina funció té?
→ És esperat?
→ Què està fent?
→ El seu comportament és coherent?
→ Necessitem investigar més?
```

## 7. Conclusions

Aquesta pràctica ha servit per:

- Entendre la diferència entre processos i serveis.
- Observar serveis reals de Windows.
- Entendre l'estat actual i el tipus d'inici.
- Començar a pensar en termes de *baseline* i comportament normal.
- Evitar conclusions precipitades quan una dada no coincideix amb el que esperàvem.

## Seguretat

Aquest document no inclou IP, adreces MAC, contrasenyes, claus, identificadors personals ni altres dades sensibles.
