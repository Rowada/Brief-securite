# Brief, Sécurisation d'une application :

## Introduction

## Sommaire

- Stratégies générales de sécurisations
- Sécurité partie front de l'application
- Sécurité partie back de l'application
- Sécurité d'API
- Stratégie de sauvegarde

## Stratégie générales

**1. Défense en profondeur**

> <samp>La défense en profondeur, est une stratègie de sécurité qui consiste à utiliser de multiples mesures de sécurité pour progéter l'intégrité du système.</samp>

**2. Moindre privilège**

> <samp>Le principe de moindre privilège, consiste à limiter les droits et de donner les permissions qu'aux personne autoriser.
> _Exemple_ (Un utilisateur lambda ne pourra pas avoir accès aux données administrateur.)</samp>

**3. Réduction de la surface d'attaque**

> <samp>Réduire la surface d'attaque, est une stratègie qui consiste à reduire aux maximum les zones ou de possible attaques pourraient avoir lieux.</samp>

## Les principales menaces

**1. Compromission des ressources**

> <samp>Est une attaque qui touche à l'intégrité du contenu d'un site ou d'une application. L'attaquant remplace le vrai contenu par celui de sont choix. La technique du point d'eau (_watering hole_) utilise ce principe, cette attaque est difficile à détecté et peut infecté les services sans aucune souspicion. </samp>

**2. Vol de données**

> <samp>Attaque qui occationne la perte de donnée (Informations personnelles, Authentifiants). Elle est réalisé le plus souvent pour l'usurpation d'identité ou l'escroquerie.</samp>

**3. Déni de service**

> <samp>Attaque qui pour but le ralentissement des sites attaqués voir les rendre indisponibles.</samp>

**4. XSS (_Cross-Site Scripting_)**

> <samp>Cette attaque conciste à injecter des scripts malveillants dans le contenu d'un site web. Elle permet la diffusion de malware, la réécriture du contenu d'un site et la récupération de données sensible (Ex: Identifiant, Mot de passe, Information bancaire).Les attaques XSS ne vise pas directement les applications mais plutôt les utilisateurs de celle-ci. </samp>

**5. CSRF (_Cross-Site Request Forgery_)**

> <samp>Attaque qui à pour but d'usurper l'identité d'un utilisateur à fort privilège (Ex: Administrateur) à l'aide de requête http et oblige le navigateur web de l'utilisateur à effectuer des opérations indésirables, sur des sites ou lútilisateur est authentifier.</samp>

**6. SSRF (_Server-Side Request Forgery_)**

> <samp>Est l'équilvalent, côté serveur, du CSRF. L'attaquant peut avoir accès à des services internes et à des données qui ne sont pas censés être exposés (Ex: Base de données HTTP, données de configuration du serveur).</samp>

**7. SQLI (_Injection SQL_)**

> <samp>Cette attaque consiste à modifier les requêtes SQL lors des appels à la base de données, le plus souvent par le biais des formulaires. L'attaquant peut ainsi avoir accès à la base de données, modifier sont contenu et par conséquent nuire à la sécurité du système </samp>

## Partie Front de l'application

### Présentation des recommendations :

**1. SOP (_Same Origin Policy_)**

> <samp>La SOP est une sécurité par defaut du navigateur, il bloque les interaction et entre origin(Domaine) différent. </samp>

**2. CORS (_Cross-Origin Resource Sharing_)**

> <samp>Les CORS est une méthode qui permet le partage de ressource avec d'autre origin en contournant la SOP. Un accord des deux partie doit avoir lieux pour valider le partage.</samp>

**3. CSP (_Content Security Policy_)**

> <samp>Protection mis en place contre les attaques XSS, permet d'ecrit une liste appellé liste blanche ou sera regrouper les ressource que l'on veux partager et avec qui on veux les partager.</samp>

**4. SRI (_Subresource Integrity_)**

> <samp>Vérifie l'intégrité des ressources (ex: venant d'un CDN), empêche l'injection ou la modification du contenu.</samp>
