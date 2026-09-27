# 🗺️ Roadmap — Mini-NOC

## Phase 1 — Socle technique ✅ Terminé
- [x] `docker-compose.yml` : PostgreSQL 15 + Zabbix Server 7.0 + Zabbix Web
- [x] Documentation : README FR/EN, architecture, guide d'installation
- [x] Vitrine GitHub prête (ce dépôt)

## Phase 2 — Déploiement ✅ Terminé
- [x] Docker Desktop installé (WSL 2) — virtualisation activée via `wsl --update`
- [x] `docker compose up -d` — PostgreSQL, Zabbix Server, Zabbix Web actifs
- [x] Accès `http://localhost:8080` (Admin / zabbix)

## Phase 3 — Supervision ✅ Terminé
- [x] Zabbix Agent 2 installé sur Windows (mode actif, sans PSK)
- [x] Hôte `PC-Ilyas` créé (template *Windows by Zabbix agent active*) — ZBX vert
- [x] Hôte `Box-Internet` : page admin box (port 80), ping `8.8.8.8`, DNS port 53
- [x] Diagnostic : box en mode furtif (ICMP bloqué), trafic via VPN (saut 10.2.0.1)

## Phase 4 — Alertes Telegram ✅ Terminé
- [x] Bot créé via @BotFather, token + chat ID récupérés
- [x] Media type Telegram configuré et testé
- [x] Action *Report problems to Zabbix administrators* activée
- [x] Test de bout en bout concluant (déclencheur test → alerte reçue)

## Phase 5 — Dashboard NOC ✅ Terminé
- [x] Dashboard *Mini-NOC* créé (disponibilité, problèmes, graphiques)
- [x] Captures d'écran : dashboard + alerte Telegram

## Phase 6 — Publication ⬜ En cours
- [ ] Créer le dépôt GitHub `mini-noc` et pousser les fichiers + captures
- [ ] Ajouter le projet au portfolio avec le lien GitHub
- [ ] (Bonus) Ajouter le projet au CV / LinkedIn
