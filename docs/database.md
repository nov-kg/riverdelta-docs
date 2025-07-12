# Base de donnée
La base de donnée est organisée également selon les service présentés dans [[architecture.md]]

## Products Service
### Product Catalog Collection
Le catalogue produit fournit tous les _product_ qui peuvent être utilisé par les autres services.

Partition Key: `productId`
```json
{
    "productId": "67103367-4da4-49c9-b1bf-d8be11c07f51",
    "name": "Ananas",
    "description": "Matière première, Ananas",
    "type": "raw" // raw or finished
}
```

## Inventory Service
### Product Lot Collection
Un _product lot_ représente un lot différent d'un produit (produit fini ou matière première). C'est à ce niveau que les stocks sont gérés.

Primary Key: productLotId,
Sort Key: productId
```json
{
    "productLotId": "67103367-4da4-49c9-b1bf-d8be11c07f51",
    "productId": "67103367-4da4-49c9-b1bf-d8be11c07f51", // ref to catalog
    "type": "raw", // "raw" OR "end-product"
    "name": "Ananas",
    "lotNumber": "3728373",
    "unit": "pièce",
    "inventory": [{
        "stockQuantity": 20,
        "location": "Goma POS",
    }]
}
```
### Transactions
Une trans
```json
{
    "transactionId": "67103367-4da4-49c9-b1bf-d8be11c07f51",
    "from_location": "Kinshasa",
    "to_location": "Goma POS",
    "type": "transport", // sale, purchase
    "transactionDate": 2024-12-31,
    "productLots": [{
        "productId": "67103367-4da4-49c9-b1bf-d8be11c07f51",
        "quantity": 25
    }],
    "properties": {}
}
```

## Production Collection
**Partition Key**: location
**Sort Key**: productionDate
```json
{
    "productionId": "67103367-4da4-49c9-b1bf-d8be11c07f51",
    "location": "Kimpese",
    "inputs": [{
        "productLotId": "67103367-4da4-49c9-b1bf-d8be11c07f51", // ref to ProductLot
        "quantity": 20
    }],
    "outputs": [{
        "productLotId": "67103367-4da4-49c9-b1bf-d8be11c07f51", // ref to ProductLot
        "quantity": 20
    }],
    "productionDate": 2024-31-12,
    "properties": {}
}
```

## Accounts
```json
{
    "accountID": "67103367-4da4-49c9-b1bf-d8be11c07f51",
    "AccountType": "Supplier", // Supplier ou Customer 
    "Name": "Acme Corp.",
    "ContactInfo": {
    "Email": "contact@acmecorp.com",
    "Phone": "+123456789",
    "Address": "123 Acme St, Springfield",
    "AssociatedProducts": ["P123", "P124", "P125"],
    "AccountDetails": {},
    "Properties": {}
}
```

## Other Entities
### Properties
Properties gives metadata information about the entity, it covers most entities in the database.
```json
"properties": {
    "CreatedBy": "67103367-4da4-49c9-b1bf-d8be11c07f51", // ref to user
    "CreatedAt": "2022-12-27 08:26:49.219717",
    "UpdatedBy": "67103367-4da4-49c9-b1bf-d8be11c07f51", // ref to user
    "UpdatedAt": "2022-12-27 08:26:49.219717"
}
```