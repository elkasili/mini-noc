# 📘 Guide d'installation — Mini-NOC

> Prérequis : un PC Windows avec **Docker Desktop** (voir étape 1).

## Étape 1 — Installer Docker Desktop (sur le PC Windows)

1. Télécharger : https://www.docker.com/products/docker-desktop/
2. Installer en cochant **WSL 2** quand proposé, puis redémarrer le PC.
3. Lancer Docker Desktop et attendre que l'icône baleine soit verte.

## Étape 2 — Démarrer Zabbix

1. Copier `docker-compose.yml` dans un dossier, ex. `C:\mini-noc\`.
2. Ouvrir un terminal dans ce dossier :
   ```
   docker compose up -d
   ```
3. Attendre ~2 minutes (création de la base), puis ouvrir :
   **http://localhost:8080**
4. Connexion : `Admin` / `zabbix` (pense à changer le mot de passe après !)

## Étape 3 — Superviser le PC Windows

1. Télécharger **Zabbix Agent 2** pour Windows : https://www.zabbix.com/download_agents
2. Pendant l'installation, renseigner :
   - *Zabbix server IP/DNS* : `127.0.0.1`
   - Cocher **"Enable active checks"**
3. Dans Zabbix web : *Collecte de données > Hôtes > Créer un hôte*
   - Nom : `PC-Ilyas`, groupe : `Windows`, interface : Agent `127.0.0.1:10050`
   - Modèle : **"Windows by Zabbix agent active"**
4. Vérifier que l'hôte passe au vert (disponibilité ZBX).

## Étape 4 — Superviser la box et Internet

Créer un hôte `Box-Internet` (groupe `Network`, interface sans agent) avec ces
éléments supervisés (type **"Vérification simple"**) :

| Élément | Clé | Seuil d'alerte |
|---|---|---|
| Box : page admin (port 80) | `net.tcp.service[tcp,192.168.1.1,80]` | = 0 pendant 3 min → alerte |
| Ping Internet | `icmpping[8.8.8.8]` | = 0 pendant 3 min → alerte |
| DNS Google (port 53) | `net.tcp.service[tcp,8.8.8.8,53]` | = 0 → alerte |

> La box bloque le ping (ICMP) par défaut : on teste sa page d'administration (port 80)
> à la place. De même, `net.dns` n'existe pas en "vérification simple" (réservé à
> l'agent) : on teste le port DNS 53 directement.
> Si ta box n'est pas en `192.168.1.1`, adapte (souvent `192.168.1.1` chez IAM / Orange / INWI).

## Étape 5 — Alertes Telegram 🔔

1. Sur Telegram, parler à **@BotFather** : `/newbot` → récupérer le **token**.
2. Envoyer un message à ton bot, puis récupérer ton **chat ID** via :
   `https://api.telegram.org/bot<TON_TOKEN>/getUpdates`
3. Dans Zabbix : *Alertes > Types de médias > Telegram* → coller le token, tester.
4. *Alertes > Actions > Trigger actions* → activer **"Report problems to Zabbix administrators"**
   et ajouter ton utilisateur Telegram comme destinataire.
5. Test : coupe le Wi-Fi 5 minutes → tu reçois l'alerte. 🎉

## Étape 6 — Dashboard NOC

*Surveillance > Tableaux de bord > Créer* : ajoute des widgets
**"Disponibilité des hôtes"**, **"Problèmes"**, **"Graphique"** (CPU, ping).
Fais des captures d'écran propres : elles serviront pour GitHub et le portfolio.

## Étape 7 — Publication

1. Créer un dépôt GitHub `mini-noc` avec tout le contenu de ce dossier
   + les captures d'écran du dashboard et d'une alerte Telegram reçue.
2. Ajouter le projet au portfolio (section Projets) avec le lien GitHub.
