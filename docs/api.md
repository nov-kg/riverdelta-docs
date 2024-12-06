
# Documentation de l'API

Bienvenue dans l'API Produits ! Cette API permet de gérer toutes les requêtes backend.

## Base URL
Les URLs de base de chaque environnement sont documenté dans [DevOps](devops.md).
```
https://<aws-api-gateway-url>/<stage>
```

## Produits
### Lister les produits
Récupère la liste de tous les produits disponibles.

`GET /products`  

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

`GET /products/{productId}`  

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

### Créer un produit
Ajoute un nouveau produit à la base de données.

`POST /products`  


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

### Mettre à jour un produit

`PUT /products/{productId}`

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

`DELETE/products/{productId}`  

**Paramètres d'URL**:

  - `productId` (string): ID du produit.

**Réponse**:

- **Code 200**: Produit supprimé.
- **Code 404**: Produit non trouvé.

---
## Lots
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
