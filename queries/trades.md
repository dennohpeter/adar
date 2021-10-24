```
  fragment Trade on Trade {
    id
    method
    timestamp
    adapter {
      id
      identifier
    }
    ...AddTrackedAssetsTrade
    ...ApproveAssetsTrade
    ...LendTrade
    ...LendAndStakeTrade
    ...ClaimRewardsAndReinvestTrade
    ...ClaimRewardsAndSwapTrade
    ...MultiLendTrade
    ...MultiRedeemTrade
    ...MultiTokenSwapTrade
    ...RedeemTrade
    ...TokenSwapTrade
    ...UnstakeAndRedeemTrade
  }
```

````
fragment AddTrackedAssetsTrade on AddTrackedAssetsTrade {
  incomingAssetAmounts {
    ...AssetAmount
  }
  fundState {
    id
    currencyPrices {
      ...CurrencyPrice
    }
  }
}
```

```
fragment ApproveAssetsTrade on ApproveAssetsTrade {
  fundState {
    id
    currencyPrices {
      ...CurrencyPrice
    }
  }
}
```
fragment LendTrade on LendTrade {
  price
  incomingAssetAmount {
    ...AssetAmount
  }
  outgoingAssetAmount {
    ...AssetAmount
  }
  fundState {
    id
    currencyPrices {
      ...CurrencyPrice
    }
  }
}
```
```
fragment LendAndStakeTrade on LendAndStakeTrade {
  incomingAssetAmount {
    ...AssetAmount
  }
  outgoingAssetAmounts {
    ...AssetAmount
  }
  fundState {
    id
    currencyPrices {
      ...CurrencyPrice
    }
  }
}
```
```
fragment ClaimRewardsAndReinvestTrade on ClaimRewardsAndReinvestTrade {
  incomingAssetAmount {
    ...AssetAmount
  }
  fundState {
    id
    currencyPrices {
      ...CurrencyPrice
    }
  }
}
```
```
fragment ClaimRewardsAndSwapTrade on ClaimRewardsAndSwapTrade {
incomingAssetAmount {
    ...AssetAmount
  }
  fundState {
    id
    currencyPrices {
      ...CurrencyPrice
    }
  }
}
```
```
fragment MultiLendTrade on MultiLendTrade {
  incomingAssetAmounts {
    ...AssetAmount
  }
  outgoingAssetAmounts {
    ...AssetAmount
  }
  fundState {
    id
    currencyPrices {
      ...CurrencyPrice
    }
  }
}
```
```
fragment MultiRedeemTrade on MultiRedeemTrade {
  incomingAssetAmounts {
    ...AssetAmount
  }
  outgoingAssetAmounts {
    ...AssetAmount
  }
  fundState {
    id
    currencyPrices {
      ...CurrencyPrice
    }
  }
}
```
```
fragment MultiTokenSwapTrade on MultiTokenSwapTrade {
  incomingAssetAmounts {
    ...AssetAmount
  }
  outgoingAssetAmounts {
    ...AssetAmount
  }
  fundState {
    id
    currencyPrices {
      ...CurrencyPrice
    }
  }
}
```
```
fragment RedeemTrade on RedeemTrade {
  price
  incomingAssetAmount {
    ...AssetAmount
  }
  outgoingAssetAmount {
    ...AssetAmount
  }
  fundState {
    id
    currencyPrices {
      ...CurrencyPrice
    }
  }
}
```
```
fragment TokenSwapTrade on TokenSwapTrade {
  price
  incomingAssetAmount {
    ...AssetAmount
  }
  outgoingAssetAmount {
    ...AssetAmount
  }
  fundState {
    id
    currencyPrices {
      ...CurrencyPrice
    }
  }
}
```
```
fragment UnstakeAndRedeemTrade on UnstakeAndRedeemTrade {
  incomingAssetAmounts {
    ...AssetAmount
  }
  outgoingAssetAmount {
    ...AssetAmount
  }
  fundState {
    id
    currencyPrices {
      ...CurrencyPrice
    }
  }
}
```
```
query FundTrades($id: ID!) {
  fund(id: $id) {
    id
    trades(first: 1000) {
      ...Trade
    }
  }
}
```
```
query ManagerFundsTrades($id: ID!) {
  account(id: $id) {
    id
    managements(first: 1000) {
      id
      name
      trades {
        ...Trade
      }
    }
  }
}
```
```
query InvestorFundsTrades($id: ID!) {
  account(id: $id) {
    id
    investments(first: 1000) {
      id
      fund {
        id
        name
        trades {
          ...Trade
        }
      }
    }
  }
}
```
```
query NetworkTrades {
  trades(orderBy: timestamp, orderDirection: desc, first: 100) {
    ...Trade
    fund {
      id
      name
    }
  }
}
```
````
