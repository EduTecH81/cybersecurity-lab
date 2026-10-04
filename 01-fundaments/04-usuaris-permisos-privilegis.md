# 04 — Usuaris, permisos i privilegis a Windows

## Objectiu

Documentar una pràctica bàsica sobre identitat, permisos, privilegis i UAC a Windows 11 Pro.

## 1. Conceptes bàsics

- **Usuari**: identitat associada a un compte que permet iniciar sessió i executar processos.
- **Permís**: autorització per fer una acció sobre un recurs, com llegir o modificar un fitxer.
- **Privilegi**: capacitat per fer una operació del sistema, com gestionar determinats components de Windows. No és el mateix que un permís sobre un fitxer.
- **Usuari estàndard**: compte pensat per a les tasques habituals, amb capacitats limitades per modificar el sistema.
- **Administrador**: compte membre del grup Administradors, que pot executar tasques administratives mitjançant elevació quan calgui.

El **principi de mínim privilegi** consisteix a utilitzar només els permisos i privilegis necessaris per a cada tasca. Tenir més privilegis dels necessaris augmenta la superfície de risc: un error o un procés compromès pot afectar més recursos i provocar canvis de més abast.

## 2. Compte utilitzat

Durant la pràctica es va comprovar el compte actual:

- Tipus de compte: Administrador

Es documenta només el tipus de compte, sense noms d'usuari, correus electrònics ni identificadors personals.

## 3. Comanda whoami

Es va obrir una consola normal de `cmd` i es va executar:

```cmd
whoami
```

La sortida seguia aquest patró genèric:

```text
nom-pc\usuari
```

La comanda mostra la identitat sota la qual s'està executant el procés actual. El patró anterior és il·lustratiu i no conté el nom real de l'ordinador ni de l'usuari. Conèixer la identitat no indica, per si sol, si el procés està elevat.

## 4. Grups de seguretat

A la consola normal es va executar:

```cmd
whoami /groups
```

Es va observar que l'usuari pertanyia al grup Administradors, però aquest apareixia en un estat tipus **Deny only / Solo para denegar**.

Amb UAC (Control de comptes d'usuari), els processos habituals d'un compte administrador poden executar-se amb un **token limitat**. El token és la informació de seguretat que Windows utilitza per comprovar la identitat, els grups i els privilegis d'un procés.

En aquest token limitat, el grup Administradors marcat com a *Deny only* no es pot utilitzar per concedir accés mitjançant permisos assignats al grup. Sí que es té en compte per aplicar denegacions explícites. Això no elimina la pertinença al grup: limita com s'utilitza en les comprovacions d'accés del procés no elevat.

## 5. UAC i elevació de privilegis

Després es va obrir `cmd` amb **Executar com a administrador** i es va tornar a executar:

```cmd
whoami /groups
```

En aquest cas, el grup Administradors ja apareixia habilitat.

**Ser membre del grup Administradors** és una característica del compte. **Executar un procés amb privilegis elevats** significa que aquell procés utilitza un token amb capacitats administratives disponibles. L'elevació afecta el procés elevat i els processos que hereten el seu token; no converteix automàticament totes les aplicacions obertes en processos elevats.

Esquema conceptual del comportament observat:

```text
Compte administrador
→ sessió normal
→ token limitat per UAC
→ privilegis reduïts

Compte administrador
→ executar com a administrador
→ UAC
→ token elevat
→ privilegis administratius actius
```

Aquí, «privilegis administratius actius» expressa que el procés té capacitats administratives efectives. No implica que tots els privilegis individuals del token estiguin habilitats permanentment.

## 6. Relació amb ciberseguretat

Aquest comportament és important perquè:

- Limita l'impacte dels processos executats normalment amb un token limitat.
- Redueix l'exposició a canvis no autoritzats que requereixen elevació.
- Ajuda a aplicar el principi de mínim privilegi, elevant només les tasques que ho necessiten.
- Diferencia la identitat del compte del nivell de privilegi efectiu d'un procés.

**«Usuari administrador» no significa que tots els processos s'executin sempre amb privilegis administratius.** Cal observar el context d'execució i el token utilitzat per entendre què pot fer realment cada procés.

UAC ajuda a controlar l'elevació, però no substitueix la prudència: cal revisar quin programa demana privilegis i per què abans d'autoritzar-lo.

## 7. Conclusions

La pràctica ha servit per entendre:

- La identitat d'usuari que mostra `whoami`.
- La diferència entre permisos i privilegis.
- El paper d'UAC en l'elevació.
- El token limitat d'un procés no elevat.
- El token elevat d'un procés executat com a administrador.
- El principi de mínim privilegi i la importància d'elevar només quan és necessari.

## Seguretat i privacitat

El document utilitza exemples genèrics i no inclou noms reals d'usuari o de dispositius, correus electrònics, IP, MAC, contrasenyes, claus ni identificadors personals.
