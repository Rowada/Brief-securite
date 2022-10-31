# Brief, Sécurisation d'une application :

## Introduction

## Sommaire

- Stratégies générales de sécurisation
- Sécurité partie front de l'application
- Sécurité partie back de l'application
- Sécurité d'API
- Stratégie de sauvegarde

## Stratégies générales

**1. Défense en profondeur**

> <samp>La défense en profondeur est une stratègie de sécurité qui consiste à utiliser de multiples mesures de sécurité pour progéter l'intégrité du système.</samp>

**2. Moindre privilège**

> <samp>Le principe de moindre privilège consiste à limiter les droits et à ne donner les permissions qu'aux personnes autorisées.
> _Exemple_ :(Un utilisateur lambda ne pourra pas avoir accès aux données administrateur.)</samp>

**3. Réduction de la surface d'attaque**

> <samp>Réduire la surface d'attaque est une stratègie qui consiste à reduire aux maximum les zones où de possibles attaques pourraient avoir lieu.</samp>

## Les principales menaces

**1. Compromission des ressources**

> <samp>Est une attaque qui touche à l'intégrité du contenu d'un site ou d'une application. L'attaquant remplace le vrai contenu par celui de son choix. La technique du point d'eau (_watering hole_) utilise ce principe. Cette attaque est difficile à détecter et peut infecter les services sans aucune suspicion. </samp>

**2. Vol de données**

> <samp>Attaque qui occationne la perte de données (Informations personnelles, Authentifiants). Elle est réalisée le plus souvent pour l'usurpation d'identité ou l'escroquerie.</samp>

**3. Déni de service** (_DDOS_)

> <samp>Attaque qui a pour but le ralentissement des sites attaqués voir les rendre indisponible.</samp>

**4. XSS (_Cross-Site Scripting_)**

> <samp>Cette attaque conciste à injecter des scripts malveillants dans le contenu d'un site web. Elle permet la diffusion de malware, la réécriture du contenu d'un site et la récupération de données sensibles (Ex: Identifiant, Mot de passe, Information bancaire). Les attaques XSS ne viseent pas directement les applications mais plutôt les utilisateurs de celles-ci. </samp>

**5. CSRF (_Cross-Site Request Forgery_)**

> <samp>Attaque qui à pour but d'usurper l'identité d'un utilisateur à fort privilège (Ex: Administrateur) à l'aide de requête http et oblige le navigateur web de l'utilisateur à effectuer des opérations indésirables sur des sites ou l'utilisateur est authentifier.</samp>

**6. SSRF (_Server-Side Request Forgery_)**

> <samp>Est l'équilvalent côté serveur du CSRF. L'attaquant peut avoir accès à des services internes et à des données qui ne sont pas censé être exposées (Ex: Base de données HTTP, données de configuration du serveur).</samp>

**7. SQLI (_Injection SQL_)**

> <samp>Cette attaque consiste à modifier les requêtes SQL lors des appels à la base de données, le plus souvent par le biais des formulaires. L'attaquant peut ainsi avoir accès à la base de données, modifier son contenu et par conséquent nuire à la sécurité du système </samp>

## Partie Front de l'application

### Présentation des recommendations :

**1. SOP (_Same Origin Policy_)**

> <samp>Le SOP est une sécurité par defaut du navigateur, il bloque les interactions entre origin (Domaine) différent. </samp>

**2. CORS (_Cross-Origin Resource Sharing_)**

> <samp>Le CORS est une méthode qui permet le partage de ressource avec d'autre origin en contournant le SOP. Un accord des deux parties doit avoir lieu pour valider le partage.</samp>

**3. CSP (_Content Security Policy_)**

> <samp>Protection mis en place contre les attaques XSS, elle permet d'écrire une liste appellée liste blanche où seront regroupées les ressources que l'on veut partager et avec qui les partager.</samp>

**4. SRI (_Subresource Integrity_)**

> <samp>Vérifie l'intégrité des ressources (ex: venant d'un CDN), empêche l'injection ou la modification du contenu.</samp>

### HTTPS / TLS / HSTS

**1. HTTPS (_Hyper Text Protocole Secure_)**

> <samp>HTTPS est une extension sécurisée du protocole HTTP. Le "S" signifie d'ailleur _Secured_ (sécurisé). Il garantit la confidentialité et l'intégrité des données envoyées par l'utilisateur et reçues par le serveur.
> Le "S" s'obtient grâce à un certificat SSL/TLS acquis auprès d'une Autorité de Certification.</samp>

**2. TLS (_Transport Layer Security_)**

> <samp>TLS est un protocole de sécurité qui facilite la confidentialité et la sécurité des données. Il permet de chiffrer les données lors des échanges entre les applications web et les serveurs. </samp>

**3. HSTS (_HTTP Strict Transport Security_)**

> <samp>HSTS est une politique de sécurité Web conçue pour protéger les sites web HTTPS contre les attaques. Il indique aux navigateurs Web de n'utiliser que les connexions HTTPS et bloque l'utilisation du protocole HTTP.</samp>

### Sanitization

_"Ne jamais faire confiance aux entrées de l'utilisateur"_

> <samp>la sanitization consiste à supprimer tout caractère dangereux des entrées utilisateurs et vérifie si les données ont le format et le type attendu.
> Ce traitement des formulaires prévient d'éventuel attaque de type SQL ou XSS. </samp>

### Cookie / Session / Token

**1. Cookie**

> <samp>Les cookies sont des petits fichiers stockés par un serveur dans l'appareil d'un utilisateur et associés à un domaine web.
> Les cookies ont plusieurs utilisations, ils peuvent permettre de mémoriser les identifiants, les préférences d'un utilisateur.
> Il existe un type de cookie appellé _Cookie tier_ qui est déposé par des sites différents de ceux visités par les utilisateurs, via le navigateur. Il va collecter des données sur les utilisateurs, ces données vont être analysées et utilisées à des fins publicitaires.
> Il est recommandé de ne pas stocker des données sensibles dans les cookies.</samp>

**2. Session**

> <samp>Une session web est le temps passé par un utilisateur à naviguer sur un site web, du moment où il s'authentifie jusqu'au moment où il quitte le site.
> Une session web peut stocker des informations sur les utilisateurs lors de leurs navigations. Il peut s'agir par exemple des pages que l'utilisateur à consultées, les données saisies dans un formulaire ou même un panier d'articles.
> Le plus souvent une session a une limite de temps qui varie selon les sites, il est d'ailleurs recommandé de limiter cette durée sur les sessions pouvant contenir des données sensibles.</samp>

**3. Token**

> <samp>L'authentification par jeton (_token_) est un protocole qui permet de vérifier l'identité d'un utilisateur, d'une API ou d'un autre serveur.
> </samp>
