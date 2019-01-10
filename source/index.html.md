---
title: Swello Pixel API Reference

language_tabs: # must be one of https://git.io/vQNgJ
  - shell

toc_footers:
  - <a href='https://swello.com/fr/contact'>Obtenir une clé d'API</a>

includes:
  - errors
  - export
  - internal

search: true
---

# Introduction

Intégrez Swello Pixel à votre application!

```html
<iframe src="http://localhost:8567/testi.html?userKey=uezgyfuiyrekuh"></iframe>
```

Pour intégrer Pixel vous aurez besoin d'intégrer une iframe dans votre code.
Pour identifier l'utilisateur vous pourrez aurez besoin d'ajouter une clé `userKey` à la source de l'iframe.
Ces clés utilisateur sont à générer en utilisant l'API présentée dans ce document.

<aside class="notice">
L'API consomme et produit uniquement du <code>JSON</code>.
</aside>

# Authentification

> Exemple de requête authentifiée:

```shell
curl "https://api.pixel.swello.com"
  -H "Authorization: YOUR_API_KEY"
```

Toutes vos requêtes doivent être authentifiés avec votre clé d'API.
Pour obtenir votre clé [contactez-nous](https://swello.com/fr/contact).

Pour authentifier vos requêtes, utilisez l'en-tête `Authorization` avec votre clé d'API.

`Authorization: YOUR_API_KEY`

<aside class="notice">
N'oubliez pas de remplacer <code>YOUR_API_KEY</code> par votre clé d'API.
</aside>

# Clé utilisateur

## Créer une clé utilisateur

```shell
curl "https://api.pixel.swello.com/userKey"
  -H "Authorization: YOUR_API_KEY"
  -H "Content-Type: application/json"
  -d '{"userId":"123","plan":"free"}'
```

> Exemple de réponse

```json
{
  "userKey": "2875616e2d924e57999e0fce8e7fdb59",
  "expiresAt": "2019-10-15T15:53:00+00:00",
  "userId": "123",
  "plan": "free"
}
```

Ce point d'entrée permet de créer une clé utilisateur pour un de vos utilisateurs. Cette clé est valable 30 jours et permet d'identifier un utilisateur de votre application sur Pixel. C'est vous qui définissez les droits qu'aura cet utilisateur sur Pixel.

### HTTP Request

`POST https://api.pixel.swello.com/userKey`

### Paramètres de la requête

Paramètre | Type | Description
--------- | ------- | -----------
userId | String | un identifiant utilisateur unique de votre application (64 caractères max.)
plan | String | le plan auquel a accès cet utilisateur (`free`,`premium`)
admin | Boolean | cet utilisateur peut créér des templates publics

Le `userId` est un identifiant qui permet de faire le lien entre les utilisateurs enregistrés dans votre application et notre base d'utilisateurs.

Pour un utilisateur de votre application, lorsque vous renouvellerez sa clé il faudra redonner le même `userId` ce qui nous permettra de retrouver ses templates.

Il nous permet également de mesurer l'utilisation de notre application et donc de vous prévenir si vous dépassez les limites propres à votre abonnement.  

## Supprimer une clé utilisateur

```shell
curl "https://api.pixel.swello.com/userKey/2875616e2d924e57999e0fce8e7fdb59"
  -X DELETE
  -H "Authorization: YOUR_API_KEY"
```

> Cette reqûete ne retourne pas de données mais un status code `204 No Content`

Ce point d'entrée permet de supprimer une clé utilisateur

### HTTP Request

`DELETE https://api.pixel.swello.com/userKey/<userKey>`

### URL Parameters

Paramètre | Description
--------- | -----------
userKey | la clé utilisateur à supprimer
