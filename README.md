# Brief : Stratégie de Sécurisation d'une Application

## Tables des matières

- [Introduction](#introduction)
- [Stratégies générales](#stratégies-générales)
- [Les principales menaces](#les-principales-menaces)
- [Présentation des recommendations :](#présentation-des-recommendations-)
  - [HTTPS / TLS / HSTS](#https--tls--hsts)
  - [Sanitisation](#sanitisation)
  - [Cookie / Session / Token](#cookie--session--token)
  - [Les API (_Application programming Interface_)](#les-api-application-programming-interface)
- [Journalisation](#journalisation)
- [Authenfication vs Autorisation](#authenfication-vs-autorisation)
  - [RGPD (_Règlement Général sur la Protection des Données_)](#rgpd-règlement-général-sur-la-protection-des-données)
  - [Audit](#audit)
  - [Bug Bounty](#bug-bounty)
  - [Hachage / Salage / Sécurisation Mot de passe](#hachage--salage--sécurisation-mot-de-passe)
  - [Stratégie de sauvegarde](#stratégie-de-sauvegarde)
  - [Ressources](#ressources)

## Introduction

This documentation has been realized in order to present a security strategy for a web application. You will find my choices in terms of security and a presentation of the main security protocols of a web application.

## Stratégies générales

**1. Défense en profondeur**

> La défense en profondeur est une stratègie de sécurité qui consiste à utiliser de multiples mesures de sécurité pour protéger l'intégrité du système.

**2. Moindre privilège**

> Le principe de moindre privilège consiste à limiter les droits et à ne donner les permissions qu'aux personnes autorisées.
> _Exemple_ :(Un utilisateur lambda ne pourra pas avoir accès aux données administrateur.)

**3. Réduction de la surface d'attaque**

> Réduire la surface d'attaque est une stratègie qui consiste à reduire aux maximum les zones où de possibles attaques pourraient avoir lieu.

## Les principales menaces

**1. Compromission des ressources**

> Est une attaque qui touche à l'intégrité du contenu d'un site ou d'une application. L'attaquant remplace le vrai contenu par celui de son choix. La technique du point d'eau (_watering hole_) utilise ce principe. Cette attaque est difficile à détecter et peut infecter les services sans aucune suspicion.

**2. Vol de données**

> Attaque qui occationne la perte de données (Informations personnelles, Authentifiants). Elle est réalisée le plus souvent pour l'usurpation d'identité ou l'escroquerie.

**3. Déni de service (_DDOS_)**

> Attaque qui a pour but le ralentissement des sites attaqués voir les rendre indisponible.

**4. XSS (_Cross-Site Scripting_)**

> Cette attaque conciste à injecter des scripts malveillants dans le contenu d'un site web. Elle permet la diffusion de malware, la réécriture du contenu d'un site et la récupération de données sensibles (Ex: Identifiant, Mot de passe, Information bancaire). Les attaques XSS ne viseent pas directement les applications mais plutôt les utilisateurs de celles-ci.

**5. CSRF (_Cross-Site Request Forgery_)**

> Attaque qui à pour but d'usurper l'identité d'un utilisateur à fort privilège (Ex: Administrateur) à l'aide de requête http et oblige le navigateur web de l'utilisateur à effectuer des opérations indésirables sur des sites ou l'utilisateur est authentifier.

**6. SSRF (_Server-Side Request Forgery_)**

> Est l'équilvalent côté serveur du CSRF. L'attaquant peut avoir accès à des services internes et à des données qui ne sont pas censé être exposées (Ex: Base de données HTTP, données de configuration du serveur).

**7. SQLI (_Injection SQL_)**

> Cette attaque consiste à modifier les requêtes SQL lors des appels à la base de données, le plus souvent par le biais des formulaires. L'attaquant peut ainsi avoir accès à la base de données, modifier son contenu et par conséquent nuire à la sécurité du système.

**8. Clickjacking**

> le clickjacking est une attaque qui incite un utilisateur à cliquer sur un élément d'un site web qui au préalable a été modifié. Les utilisateurs touchés par cette attaque peuvent être amené à télécharger des virus ou à être dirigé vers des sites malveillants. Dans certain cas cette attaque peut même entrainer un vol de données sensibles.

## Présentation des recommendations :

**1. SOP (_Same Origin Policy_)**

> Le SOP est une sécurité par defaut du navigateur, il bloque les interactions entre origin (Domaine) différent.

**2. CORS (_Cross-Origin Resource Sharing_)**

> Le CORS est une méthode qui permet le partage de ressource avec d'autre origin en contournant le SOP. Un accord des deux parties doit avoir lieu pour valider le partage.

_Dans le cadre du projet nous utiliserons le CORS pour le partage de ressources avec les partenaires._

**3. CSP (_Content Security Policy_)**

> Protection mis en place contre les attaques XSS, elle permet d'écrire une liste appellée liste blanche où seront regroupées les ressources que l'on veut partager et avec qui les partager.

**4. SRI (_Subresource Integrity_)**

> Vérifie l'intégrité des ressources (ex: venant d'un CDN), empêche l'injection ou la modification du contenu.

_Dans le cadre du projet nous nous servirons du SRI pour contrôler l'intégrité des ressources externes en cas d'utilisation de librairie._

### HTTPS / TLS / HSTS

**1. HTTPS (_Hyper Text Protocole Secure_)**

> HTTPS est une extension sécurisée du protocole HTTP. Le "S" signifie d'ailleur _Secured_ (sécurisé). Il garantit la confidentialité et l'intégrité des données envoyées par l'utilisateur et reçues par le serveur.
> Le "S" s'obtient grâce à un certificat SSL/TLS acquis auprès d'une Autorité de Certification.

**2. TLS (_Transport Layer Security_)**

> TLS est un protocole de sécurité qui facilite la confidentialité et la sécurité des données. Il permet de chiffrer les données lors des échanges entre les applications web et les serveurs.

**3. HSTS (_HTTP Strict Transport Security_)**

> HSTS est une politique de sécurité Web conçue pour protéger les sites web HTTPS contre les attaques. Il indique aux navigateurs Web de n'utiliser que les connexions HTTPS et bloque l'utilisation du protocole HTTP.

### Sanitisation

_"Ne jamais faire confiance aux entrées de l'utilisateur"_

> La sanitisation consiste à supprimer tout caractère dangereux des entrées utilisateurs et vérifie si les données ont le format et le type attendu.
> Il est recommandé pour une sécurité un maximal des entrées utilisateurs, d'effectuer la sanitisation à la fois côté client et côté serveur.
> Ce traitement des formulaires prévient d'éventuel attaque de type SQL ou XSS.

### Cookie / Session / Token

**1. Cookie**

> Les cookies sont des petits fichiers stockés par un serveur dans l'appareil d'un utilisateur et associés à un domaine web.
> Les cookies ont plusieurs utilisations, ils peuvent permettre de mémoriser les identifiants, les préférences d'un utilisateur.
> Il existe un type de cookie appellé _Cookie tier_ qui est déposé par des sites différents de ceux visités par les utilisateurs, via le navigateur. Il va collecter des données sur les utilisateurs, ces données vont être analysées et utilisées à des fins publicitaires.

Il est recommandé de ne pas stocker des données sensibles dans les cookies.

**2. Session**

> Une session web est le temps passé par un utilisateur à naviguer sur un site web, du moment où il s'authentifie jusqu'au moment où il quitte le site.
> Une session web peut stocker des informations sur les utilisateurs lors de leurs navigations. Il peut s'agir par exemple des pages que l'utilisateur à consultées, les données saisies dans un formulaire ou même un panier d'articles.
> Le plus souvent une session a une limite de temps qui varie selon les sites, il est d'ailleurs recommandé de limiter cette durée sur les sessions pouvant contenir des données sensibles.

_Dans le cadre du projet, nous recommandons de limiter la durée des sessions après une période d'inactivité, 15 minutes nous semble être la durée appropriée._

**3. Token**

> Un token peut être vu comme un genre de signature numérique, il est généralement encodé et utilisé pour authentifier et autoriser un utilisateur à accèder à des ressources.
> Un token est généré sous la forme d'un OTP (_One-Time Password_), ce qui veux dire qu'il ne peut être utilisé qu'une seule fois.
> L'authentification avec un token permet aux utilisateurs de vérifier leur identité. Ils reçoivent en contre partie un token unique qui leur donne accès à certaines ressources suivant leurs autorisations et cela pendant un lapse de temps défini.

> **JSON Web Token (_JWT_)** est utilisé pour fournir en toute sécurité des informations sous la forme d'un objet JSON. Les token JWT sont souvent utilisés pour sécuriser les API (EX: API RESTful), gérer l'authenfication et les autorisations des utilisateurs.

### Les API (_Application programming Interface_)

Les API permettent à deux applications de communiquer entre elles et d'échanger des données. Par exemple, dans le cas d'une application météo l'utilisateur va rentrer un code postal et l'API va lui retourner la température ou le temps à venir.
Lors de ces échanges plusieurs failles de sécurité peuvent survenir mais avec l'utilisation des protocoles cités plus haut (HTTPS, Token d'authentification ect..), les API pourront être sécurisées.

Pour empêcher d'éventuelles attaques DDOS il est recommandé de mettre en place des quotas pour limiter le nombre de requêtes autorisées par les utilisateurs.

**Les API Stateless**

> Une API Stateless est une API qui ne stocke pas de données sur les utilisateurs.
> Chaque requête devra contenir toutes les informations nécessaires pour que le serveur puisse l'exécuter et y répondre.
> Le protoque stateless traite chaque action comme si elle se produit pour la première fois.

**Les API Stateful**

> À inverse les API stateful conserve les informations des sessions précèdentes et les stockes sur un serveur. Par conséquence chaque nouvelle requête est traitée comme la précèdente.

## Journalisation

> La journalisation consiste à tenir un journal contenant des messages fournissant des informations sur les éventuels incidents de sécurité. Elle permet d'analyser le comportement de l'application web et du réseau.
> Il est recommandé que l'analyse du journal se fasse de manière automatique pour permettre une détection plus rapide en cas d'incident.

## Authenfication vs Autorisation

**1. L'authentification**

> L'authentification consiste à vérifier l'identité des utilisateurs. Si le système détermine que vous êtes la personne appropriée, il vous donne les autorisations qui vous ont été attibuées.
> En général, le système d'authentification est constitué d'un nom d'utilisateur et d'un mot de passe.

**2. L'autorisation**

> L'autorisation est utilisée pour déterminer les droits accordées à un utilisateur.
> L'autorisation intervient après l'authentification, une fois que l'identité de l'utilisateur a été vérifiée.
> Pour mieux gérer les droits d'accès dans une application web, mettre en place un RBAC (_Contrôle d'accès basé sur les rôles_) peut être la solution.
> Ce système permet de mieux gérer les permissions des utilisateurs en leurs assignant un rôle, chaque rôle à un niveau d'autorisation différent ce qui empêche les utilisateurs d'effectuer des actions lorqu'ils n'ont pas les permissions pour le faire.

_Dans le cadre du projet, divers rôles ont déjà été définis._

- Jeune :
  - accès à une interface dédiée
  - possibiliter de demander un rendez-vous
- Utilisateur :
  - proposition d'ajout/modification de contenus rédactionnels
- Modérateur :
  - validation des ajouts/modifications de contenus rédactionnels
- Administrateur :
  - accès complet (panel admin)

### RGPD (_Règlement Général sur la Protection des Données_)

> Le RGPD est une loi européenne qui encadre le traitememt des données personnonelles sur le territoire de l'Union européenne.

### Audit

> Un audit est une analyse complète d'un site web.
> Cette analyse couvre plusieurs aspects tel que le référencement(SEO) et l'expérience utilisateur.
> La réalisation d'un audit peut contribuer à corriger les éventuels problèmes et à améliorer le site.

### Bug Bounty

> le bug bounty fait réfèrence à une récompense attribuée pour la recherche et le signalement de faille de sécurité dans un site web. De nombreuses entreprises offrent ce genre de prime car cette méthode est plus souvent moins coûteuse qu'un audit.

### Hachage / Salage / Sécurisation Mot de passe

**1. Hachage**

> Grâce à une fonction de hachage, il est possible de chiffrer les données à l'aide d'un algorithme mathématique.
> Mais le hachage n'est pas à 100% sécurisé car si le chiffrement a été réalisé avec un algorithme public et que la clé a été trouvée, on peut effectuer l'opération inverse et ainsi récupérer les données d'origine. Pour sécuriser davantage un hachage il est préférable de le combiner avec le salage.

**2. Salage**

> Une opération de salage consiste à rajouter une donnée choisie ou aléatoire après un hachage. Après cette opération, il est conseillé de procéder à un autre hachage pour rendre le tout indéchiffrable.

_Dans le cadre du projet, nous vous conseillons d'utiliser la fonction de hachage SHA-256 ainsi qu'un sel aléatoire pour sécuriser les mots de passe des modérateurs et des administrateurs._

**Politique de sécurisation des mots de passe :**

- Ne jamais stocké les mots de passe en clair
- Mettre en place un délai d'expiration des mots de passe pour les administrateurs (Validité de 6 mois)
- Imposer une longueur minimale des mots de passe
- Possibiliter d'utiliser l'authentification multifacteur pour les utilisateurs
- Ne pas utiliser le SMS comme moyen de réception d'un facteur d'authentification
- Limiter dans le temps le nombre de tentatives d'authentification
- Limiter le durée de validation d'une session authentifiée
- Générer aléatoirement le mot de passe au moment de l'inscription d'un utilisateur
- Réaliser l'authentification au travers d'un canal sécurisé pour les modérateurs et les administrateurs

### Stratégie de sauvegarde

Afin d'éviter la perte de données en cas d'attaque ou en raison d'une erreur interne, il est préférable d'effectuer régulierèment des sauvegardes.

Nous vous conseillons la mise en place d'une sauvegarde régulière (Une chaque soir dans l'idéal) et l'utilisation de la stratégie 3-2-1 conseillée par l'ANSSI (Agence National de la Sécurité des Systèmes d'Information).

La première étape de cette méthode consiste à effectuer 3 copies de sauvegarde stockées sur différents périphéries. Cela minimise la perte de données dans le cas d'une défaillance informatique.

La deuxième étape consiste à copier les données vers deux supports différents (exemple un disque dur externe).

La troisième et dernière étape consiste à répliquer les données et à les stocker sur un serveur distant, vous pouvez ainsi toujours en avoir une copie même en cas de vol ou de catastrophe naturelle.

Cette stratégie permettra de s'assurer qu'il y a toujours une sauvegarde viable quelle que soit la situation et que les données des utilisateurs de l'application sont en sécurité.

## Ressources

- [Sécurisation d'API](https://www.redhat.com/fr/topics/security/api-security)
- [RGPD](https://www.cnil.fr/fr/rgpd-de-quoi-parle-t-on)
- [Recommandations ANSSI](https://www.ssi.gouv.fr/uploads/2013/05/anssi-guide-recommandations_mise_en_oeuvre_site_web_maitriser_standards_securite_cote_navigateur-v2.0.pdf)
- [Journalisation](https://www.cnil.fr/fr/la-cnil-publie-une-recommandation-relative-aux-mesures-de-journalisation)
- [Méthode de sauvegarde 3-2-1](https://www.savbox.fr/sauvegarde-3-2-1/)
