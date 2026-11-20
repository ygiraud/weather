# Météo animée

Une page web toute simple qui affiche une animation plein écran correspondant à la météo actuelle : soleil, lune et étoiles, nuages, bruine, pluie, neige, brouillard ou orage avec éclairs.

Tout tient dans un seul fichier, [`index.html`](index.html) : HTML, CSS et JavaScript, sans dépendance, sans build et sans clé API.

## Fonctionnement

1. **Lieu** : la ville passée en paramètre `?ville=` (ou saisie dans le champ en haut à droite) si elle est fournie, sinon la géolocalisation du navigateur, et Paris si celle-ci est refusée.
2. **Météo** : la météo actuelle vient de l'API gratuite [Open-Meteo](https://open-meteo.com). Le nom de ville est converti en coordonnées par son [service de géocodage](https://open-meteo.com/en/docs/geocoding-api).
3. **Animation** : le code météo WMO choisit la scène, dessinée sur un `<canvas>`. Le fond change selon qu'il fait jour ou nuit, et la vitesse du vent incline la pluie et la neige.

Les données se rafraîchissent toutes les 15 minutes.

| Codes WMO | Scène |
|---|---|
| 0 | Ciel dégagé (soleil, ou lune et étoiles la nuit) |
| 1–2 | Partiellement nuageux |
| 3 | Couvert |
| 45, 48 | Brouillard |
| 51–57 | Bruine |
| 61–67, 80–82 | Pluie |
| 71–77, 85–86 | Neige |
| 95–99 | Orage |

## Utilisation

Ouvrir `index.html` dans un navigateur suffit. Pour que les paramètres d'URL fonctionnent partout, il vaut mieux le servir en local :

```bash
python3 -m http.server 8765
```

puis ouvrir <http://localhost:8765>.

### Paramètres d'URL

| Paramètre | Exemple | Effet |
|---|---|---|
| `ville` | `?ville=Lyon` | Affiche la météo de cette ville |
| `meteo` | `?meteo=storm` | Force une scène, pour tester : `clear`, `partly`, `cloudy`, `fog`, `drizzle`, `rain`, `snow`, `storm` |
| `nuit` | `?meteo=clear&nuit=1` | Avec `meteo`, force la version de nuit |

## Hébergement

C'est un site statique : il peut être publié tel quel sur GitHub Pages, Netlify ou n'importe quel serveur web. La géolocalisation du navigateur exige HTTPS (ou `localhost`).
