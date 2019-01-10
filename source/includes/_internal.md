# Implémentation interne

En terme d'architecture je pense qu'on pourrait utiliser une stack
AWS Lambda + API Gateway + Mongo

## Facturation

Pour calculer le nombre d'utilisateur d'une entreprise, on peut se baser sur le nombre de clé utilisateur créée,
 c'est pourquoi il serait intéressant de ne pas les supprimer mais de les marquer comme étant supprimée.

## Collections Mongo

### apiKey

Champ | Type | Description
----- | ---- | -----------
_id | String | clé API générée avec un uuid v4 par exemple
businessId | String | identifiant pour savoir à qui appartieur cet clé d'API. Ex: `5euros`

### user

Champ | Type | Description
----- | ---- | -----------
_id | String | clé utilisateur générée avec un uuid v4 également
expiresAt | DateTime | date d'expiration 30 jours après le createdAt ou lors de l'appel à DELETE
createdAt | DateTime | date de création
user | Object | 
user.businessId | String | businessId
user.id | String | userId
plan | String | le plan de cet utilisateur ou ses droits

### templates

Champ | Type | Description
----- | ---- | -----------
_id | String | ObjectId généré automatiquement par Mongo
createdAt | DateTime | date de création (peut-être omis car ObjectId le contient)
user | Object | 
user.businessId | String | businessId
user.id | String | userId
... | ... | les autres données habituelles du templates (`height`, `width`, `private` ...)
