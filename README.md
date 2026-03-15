# Station_meteo

Diagram Mermaid 
```mermaid
 A[Demarrage systeme] --> B[Initialisation SD RTC GPS Capteurs LED Interface]
    B --> C{Bouton rouge appuye 5 s ?}
    C -- Oui --> D[Mode Configuration]
    C -- Non --> E[Mode Standard]

    E -- Bouton vert 5 s --> F[Mode Economique]
    F -- Bouton vert 5 s --> E

    E -- Bouton rouge 5 s --> G[Mode Maintenance]
    F -- Bouton rouge 5 s --> G
    G -- Bouton rouge 5 s --> H[Retour mode precedent]

    D -- Inactivite depassee --> E
```
