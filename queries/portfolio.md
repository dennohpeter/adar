```
fragment Portfolio on PortfolioState {
    id
    holdings {
      ...Holding
    }
  }
```
```
  fragment Holding on HoldingState {
    id
    amount
    asset {
      ...AssetWithPrice
    }
  }
```
```
  query FundHoldings($id: ID!) {
    fund(id: $id) {
      id
      portfolio {
        ...Portfolio
      }
    }
  }
```