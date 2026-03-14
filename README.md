# Station_meteo
'''mermaid
flowchart TD

START([DEBUT]) --> MODESTD[Mode standard]
MODESTD --> LEDSTD[LED verte continue]

%% ===============================
%% ACQUISITION STANDARD
%% ===============================

LEDSTD --> ACQ[Capturer les donnees toutes les 10 minutes]

ACQ --> ERRDATA{Erreur acces donnees ?}

ERRDATA -- Oui --> LEDERR1[LED rouge + vert 2x plus long]
LEDERR1 --> TECH1[Appel technicien]
TECH1 --> END1((Fin))

ERRDATA -- Non --> TIMEOUT{Transmission > 30 sec ?}

TIMEOUT -- Oui --> DESTROY[Destruction des donnees]
DESTROY --> DISPLAYNA[Afficher NA sur interface]

TIMEOUT -- Non --> TRAITER[Traiter les donnees]

TRAITER --> GPSERR{Erreur GPS ou horloge ?}

GPSERR -- Oui --> LEDERR2[GPS : LED rouge + jaune / Horloge : rouge + bleu]
LEDERR2 --> TECH2[Appel technicien]
TECH2 --> END2((Fin))

GPSERR -- Non --> DATEPOS

%% ===============================
%% DATE + POSITION
%% ===============================

DATEPOS[Indiquer date et heure]
DATEPOS --> POSITION[Indiquer position]

POSITION --> SDTEST{Carte SD pleine ?}

SDTEST -- Oui --> LEDSD[LED rouge + blanc]
LEDSD --> DISPLAYDATA[Afficher donnees interface]

SDTEST -- Non --> SDERR{Erreur carte SD ?}

SDERR -- Oui --> LEDSDERR[LED rouge + blanc long]
LEDSDERR --> TECH3[Appel technicien]
TECH3 --> END3((Fin))

SDERR -- Non --> SAVE

SAVE[ Sauvegarder donnees sur carte SD ]
SAVE --> DISPLAYDATA2[Afficher donnees interface]

DISPLAYDATA2 --> BUTTON{Appuyer sur bouton ?}

%% ===============================
%% CHANGEMENT DE MODE
%% ===============================

BUTTON -- Non --> MODESTD

BUTTON -- Oui --> BUTTONTEST{Appuyer pendant 5 sec ?}

BUTTONTEST -- Bouton vert --> MODEECO[Mode economique]

BUTTONTEST -- Bouton rouge --> MODEMAINT[Mode maintenance]

MODEMAINT --> LEDORANGE[LED orange continue]
LEDORANGE --> ACQ

%% ===============================
%% MODE ECONOMIQUE
%% ===============================

MODEECO --> LEDBLUE[LED bleu continue]

LEDBLUE --> ECOSETTINGS

ECOSETTINGS[Desactiver capteurs au choix]
ECOSETTINGS --> ECOINTERVAL[Intervalle mesure configurable]
ECOINTERVAL --> ECOGPS[GPS mesure 1 fois sur 2]

ECOGPS --> ECOACQ[Capturer les donnees]

ECOACQ --> ERRDATA
