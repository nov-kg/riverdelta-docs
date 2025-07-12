
# Documentation de l'API

Cette API permet de gérer toutes les requêtes backend et est organisée en 4 sections :

- Produits : pour la gestion des matières premières et des produits finis
- Inventaire : permet de gérer les stocks, d'entrer et sortir des produits
- Production : permet de gérer les événements de productions

## Base URL
Les URLs de base de chaque environnement sont documenté dans [DevOps](devops.md).
```
https://<aws-api-gateway-url>/<stage>
```

## Produits
### Créer un produit
Ajoute un nouveau produit à la base de données.

`POST /product`  


**Corps de la requête**:
```json
{
  "Name": "Produit C",
  "Category": "Catégorie 3",
  "Description": "Description du produit C",
}
```

**Réponse**:

- **Code 201**: Produit créé avec succès.
- **Code 400**: Erreur dans les données envoyées.

---

### Lister les produits
Récupère la liste de tous les produits disponibles.

`GET /product/list`  

**Réponse**:
```json
  [
    {
    	"ProductId": "12345",
    	"Name": "Produit A",
    	"Category": "Catégorie 1",
     	"Description": "Description du produit A"
    },
    {
     	"ProductId": "67890",
      	"Name": "Produit B",
      	"Category": "Catégorie 2",
      	"Description": "Description du produit B"
	}
]
```

---
### Récupérer les détails d'un produit
Récupère les détails d’un produit spécifique.

`GET /product/{productId}`  

**Paramètre d'URL**:
- `productId` (string): ID du produit.

**Réponse**:
```json
{
    "ProductId": "12345",
    "Name": "Produit A",
    "Category": "Catégorie 1",
    "Description": "Description du produit A"
}
```

---


### Mettre à jour un produit

`PUT /products/{productId}/edit`

**Paramètres d'URL**:

  - `productId` (string): ID du produit.

**Corps de la requête**:
```json
{
  "Description": "Produit C - Mis à jour",
}
```

**Réponse**:

- **Code 200**: Produit mis à jour.
- **Code 404**: Produit non trouvé.

---

### Supprimer un produit
Supprime un produit spécifique.

`DELETE /products/{productId}`  

**Paramètres d'URL**:

  - `productId` (string): ID du produit.

**Réponse**:

- **Code 200**: Produit supprimé.
- **Code 404**: Produit non trouvé.

---
## Inventaire
### Créer un nouveau lot
Créer un nouveau lot. Cet API crée une transaction et ajoute un nouveau lot pour le produit désigné. La transaction est automatiquement liée dans le lot.

`POST /transactions/receive` 

**Corps de la requête**:
```json
{
	"To": "Lieu de réception",
	"TransactionDate": "2000-01-23T01:23:45.678+09:00",

}
```

**Réponse**:
```json
{
	"transactionId": "89f8dbea-b327-44a7-8a16-ac7632c1d7de",
	"productLotId": "1b974476-3b95-48b4-91ca-1878da48bcdc"
}
```
---
### Lister les lots d'un produit
Envoi la liste des lots d'un produit. Pour chaque lot, retourne également les inventaires et les transactions liées à ce lot.

`GET /transactions/{productId}`

**Paramètres d'URL**:

  - `productId` (string): ID du produit.

---
### Sortir un produit de stock
Permet de sortir un produit, matière première ou produit fini de stocks.

`POST /inventory/delivery`

## Production
### Créer une production

`POST /production`
 Permet de créer une production

### Lister les productions

`GET /production/list`

**Réponse**: liste de productions


---

## Codes d'erreur communs

- **400**: Requête mal formée.
- **404**: Ressource introuvable.
- **500**: Erreur interne du serveur.

---

## Exemples d'utilisation

### Lister les produits

```bash
curl -X GET https://<base-url>/<stage>/products
```

### Ajouter un produit

```bash
curl -X POST https://votre-api-url.com/dev/products \
-H "Content-Type: application/json" \
-d '{
  "Name": "Nouveau Produit",
  "Category": "Catégorie",
  "Description": "Description du produit"
}'
```
