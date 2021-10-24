```
fragment AssetAmount on AssetAmount {
    asset {
      ...Asset
    }
    amount
    price {
      price
    }
  }
```

```
  fragment CurrencyPrice on CurrencyPrice {
    id
    price
    currency {
      id
    }
  }
```
