# Base de donnée

## Products
### Product Catalog Item
Partition Key: `productId`
```json
{
    "productId": "67103367-4da4-49c9-b1bf-d8be11c07f51",
    "name": "Ananas",
    "description": "Matière première, Ananas",
    "category": "Fruit",
    "properties": {}
}
```
### Product Lot
Primary Key: productLotId,
Sort Key: productId
```json
{
    "productLotId": "67103367-4da4-49c9-b1bf-d8be11c07f51",
    "productId": "67103367-4da4-49c9-b1bf-d8be11c07f51", // ref to catalog
    "type": "Raw material", // or finished product
    "name": "Ananas",
    "supplierId": "67103367-4da4-49c9-b1bf-d8be11c07f51", // ref to accounts table
    "lotNumber": "3728373",
    "unit": "pièce",
    "transactionLines": [{
        "transactionId": "67103367-4da4-49c9-b1bf-d8be11c07f51", // ref to transaction
        "type": "in", // in, out
        "from": "Location",
        "to": "Location",
        "quantity": 4
    }],
    "inventory": [{
        "stockQuantity": 20,
        "location": "Goma POS",
    }],
    "properties": {}
}
```

## Transactions
```json
{
    "transactionId": "67103367-4da4-49c9-b1bf-d8be11c07f51",
    "from": "Kinshasa",
    "to": "Goma POS",
    "Type": "Transport", // Sale, Purchase
    "TransactionDate": 2024-12-31,
    "Properties": {}
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
"Properties": {
    "CreatedBy": "67103367-4da4-49c9-b1bf-d8be11c07f51", // ref to user
    "CreatedAt": "2022-12-27 08:26:49.219717",
    "UpdatedBy": "67103367-4da4-49c9-b1bf-d8be11c07f51", // ref to user
    "UpdatedAt": "2022-12-27 08:26:49.219717"
}
```