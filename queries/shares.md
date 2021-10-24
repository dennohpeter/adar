```
  fragment SharesBoughtEvent on SharesBoughtEvent {
    id
    investmentAmount
    asset {
      ...Asset
    }
    transaction {
      id
    }
  }
```

```
  fragment SharesRedeemedEvent on SharesRedeemedEvent {
    id
    fund {
      accessor {
        denominationAsset {
          ...Asset
        }
      }
    }
    payoutAssetAmounts {
      ...AssetAmount
    }
    transaction {
      id
    }
  }
```

```
  fragment SharesChange on SharesChangeInterface {
    shares
    timestamp
    fundState {
      id
      portfolio {
        id
        holdings {
          id
          asset {
            id
          }
          price {
            price
          }
        }
      }
      currencyPrices {
        ...CurrencyPrice
      }
    }
    ...SharesBoughtEvent
    ...SharesRedeemedEvent
  }
```

```
  fragment SharesChangeWithInvestor on SharesChangeInterface {
    ...SharesChange
    investor {
      id
    }
  }
```
```
  fragment InvestmentSharesChange on InvestmentSharesChangeInterface {
    shares
    timestamp
    fundState {
      id
      portfolio {
        id
        holdings {
          id
          asset {
            id
          }
          price {
            price
          }
        }
      }
      currencyPrices {
        ...CurrencyPrice
      }
    }
    ...SharesBoughtEvent
    ...SharesRedeemedEvent
  }
```

```
  fragment InvestmentSharesChangeWithInvestor on InvestmentSharesChangeInterface {
    ...InvestmentSharesChange
    investor {
      id
    }
  }
```
```
  fragment SharesChangeWithFund on SharesChangeInterface {
    ...SharesChange
    fund {
      id
      name
      accessor {
        id
        denominationAsset {
          ...Asset
        }
      }
    }
  }
```
```
  fragment InvestmentSharesChangeWithFund on InvestmentSharesChangeInterface {
    ...InvestmentSharesChange
    fund {
      id
      name
      accessor {
        id
        denominationAsset {
          ...Asset
        }
      }
    }
  }
```
```
  query FundSharesChanges($id: ID!) {
    fund(id: $id) {
      id
      sharesChanges(first: 1000) {
        ...SharesChangeWithInvestor
      }
    }
  }
```
```
  query FundInvestmentSharesChanges($id: ID!) {
    fund(id: $id) {
      id
      investmentSharesChanges(first: 1000) {
        ...InvestmentSharesChangeWithInvestor
      }
    }
  }
```

```
  query ManagerFundsSharesChanges($id: ID!) {
    account(id: $id) {
      id
      managements(first: 1000) {
        id
        name
        accessor {
          id
          denominationAsset {
            ...Asset
          }
        }
        sharesChanges(first: 1000) {
          ...SharesChangeWithInvestor
        }
      }
    }
  }
```

```
  query ManagerFundsInvestmentSharesChanges($id: ID!) {
    account(id: $id) {
      id
      managements(first: 1000) {
        id
        name
        accessor {
          id
          denominationAsset {
            ...Asset
          }
        }
        investmentSharesChanges(first: 1000) {
          ...InvestmentSharesChangeWithInvestor
        }
      }
    }
  }
```

```
  query InvestorFundsSharesChanges($id: ID!) {
    account(id: $id) {
      id
      sharesChanges(first: 1000) {
        ...SharesChangeWithFund
      }
    }
  }
```
```
  query InvestorFundsInvestmentSharesChanges($id: ID!) {
    account(id: $id) {
      id
      investmentSharesChanges(first: 1000) {
        ...InvestmentSharesChangeWithFund
      }
    }
  }
```