# 02 — Explorant Windows per dins

## Objectiu

Documentar una primera observació pràctica del sistema Windows 11 Pro utilitzant el Gestor de tasques, com a exercici inicial d'anàlisi de sistemes per a ciberseguretat.

## Sistema

- Sistema operatiu: Windows 11 Pro
- CPU: AMD Ryzen 5 5500U with Radeon Graphics, 2.10 GHz
- RAM física: 16 GB

## Observació de recursos

### CPU

- Utilització observada: 29%
- Velocitat observada: 1,81 GHz
- Processos observats: 314

Aquestes dades són una fotografia del sistema en un moment concret. La utilització, la velocitat i el nombre de processos poden variar constantment segons l'activitat del sistema, els serveis i les aplicacions obertes.

### Memòria

- Memòria en ús: 14,1 GB
- Memòria mostrada disponible per Windows: 17,7 GB
- Velocitat: 3200 MHz
- Memòria disponible observada: 4,9 GB

La memòria disponible i l'ús poden variar segons els processos i serveis actius. Windows també gestiona memòria reservada o compartida amb el maquinari, de manera que diferents pantalles del sistema poden mostrar xifres amb contextos diferents.

### Disc

- Utilització observada: 4%
- Lectura observada: 11 MB/s
- Escriptura observada: 280 KB/s
- Capacitat mostrada: 477 GB

### Xarxa

- Es va observar trànsit variable.
- En un moment de la pràctica es van observar aproximadament 120 Kbps de recepció.

El trànsit de xarxa varia segons l'activitat del sistema i les aplicacions: navegació web, sincronització de fitxers, actualitzacions, serveis en segon pla o connexions VPN poden generar activitat.

## Processos observats

Durant l'observació es van identificar, entre els processos amb més activitat o consum:

- ChatGPT
- iCloud
- Git for Windows
- Brave
- Administrador de tasques
- Antimalware Service Executable
- Microsoft Rewards
- NordVPN

Trobar un procés entre els que més recursos consumeixen **no** significa que sigui maliciós. El consum s'ha d'interpretar tenint en compte què és el procés, quina tasca està fent i si el comportament és coherent amb l'ús normal del sistema.

Antimalware Service Executable correspon al component antimalware de Microsoft Defender. La seva presència és esperable en un sistema Windows protegit; pot consumir més recursos, per exemple, durant una anàlisi o una actualització de signatures.

## Concepte: baseline

Una *baseline* o línia base és una referència del comportament habitual d'un sistema. Pot incloure l'ús normal de CPU, memòria, disc i xarxa, els processos habituals i els serveis que s'executen regularment.

Abans de poder detectar comportaments anòmals, hem d'entendre quin comportament és normal en aquell sistema. Aquesta comparació evita confondre una activitat legítima amb un possible problema de seguretat.

Flux conceptual:

```text
Procés → Què és? → És esperat? → Què està fent? → El consum és coherent? → Hi ha algun comportament anòmal?
```

## Conclusions

Aquesta pràctica ha servit per començar a observar un sistema informàtic real, identificar recursos i processos i entendre la importància d'establir una línia base abans d'investigar possibles anomalies.

## Seguretat i privacitat

Aquest document no inclou adreces IP, adreces MAC, noms d'usuari, contrasenyes, claus, identificadors personals ni cap altra dada sensible. Cap dels processos observats es presenta com a maliciós simplement pel seu nom o pel seu consum de recursos.
