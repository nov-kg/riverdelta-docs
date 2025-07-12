```json
{
    "productLotId": "67103367-4da4-49c9-b1bf-d8be11c07f51",
    "productId": "67103367-4da4-49c9-b1bf-d8be11c07f51", // ref to catalog
    "type": "raw", // "raw" OR "finished"
    "name": "Ananas",
    "supplierId": "67103367-4da4-49c9-b1bf-d8be11c07f51", // ref to accounts table
    "lotNumber": "3728373",
    "expirationDate": "2024-12-31", // ISO8601 date
    "unit": "pièce",
    "transactionLines": [{
        "transactionId": "67103367-4da4-49c9-b1bf-d8be11c07f51", // ref to transaction
        "type": "in", // in, out, production-usage, production-creation
        "from": "Location",
        "to": "Location",
        "quantity": 4
    }],
    "productionLines": [{
        "location": "Location",
        "quantity": 5
    }],
    "inventory": [{
        "stockQuantity": 20,
        "location": "Goma POS",
    }],
    "properties": {}
}
```