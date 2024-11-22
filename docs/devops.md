# DevOps

## Environnement

| Environnement | Description | API | App |
| --- | --- | --- | --- |
| `dev` | Environnement uniquement à but de développement, non stable | https://c0zxxa808l.execute-api.eu-west-3.amazonaws.com/dev | https://dev.d2m9fd2puxvkv3.amplifyapp.com/ |
| `test` | Spécification prête à la validation par l'équipe d'Elembo | | |
| `prod` | Environnement de production | | |

## Déploiements
Le frontend se déploie automatiquement dans l'environnement relatif à la branche du même nom. Exemple: un merge sur le branche `dev` déploiera le frontend automatiquement sur le déploiement dev dans Amplify.

Le backend est pour le moment développé directement via la console web AWS et déployée lors du développement. Un CI/CD est nécessaire pour passer en test.