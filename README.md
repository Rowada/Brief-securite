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

## Partie Front de l'application

### Présentation des recommendations :

**1. SOP (Same Origin Policy)**

> <samp>La SOP est une sécurité par defaut du navigateur, il bloque les interaction et entre origin(Domaine) différent. </samp>

**2. CORS (Cross-Origin Resource Sharing)**

> <samp>Les CORS est une méthode qui permet le partage de ressource avec d'autre origin en contournant la SOP. Un accord des deux partie doit avoir lieux pour valider le partage.</samp>

**3. CSP (Content Security Policy)**

> <samp>Protection mis en place contre les attaques XSS, permet d'ecrit une liste appellé liste blanche ou sera regrouper les ressource que l'on veux partager et avec qui on veux les partager.</samp>

**4. SRI (Subresource Integrity)**

> <samp>Vérifie l'intégrité des ressources (ex: venant d'un CDN), empêche l'injection ou la modification du contenu.</samp>
