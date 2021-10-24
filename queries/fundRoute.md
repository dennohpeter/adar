```
  query FundFees($comptrollerProxy: ID!) {
    comptrollerProxy(id: $comptrollerProxy) {
      id
      release {
        id
      }
      feeSettings {
        ...Fee
      }
    }
  }
```
```
  fragment Fee on FeeSettingInterface {
    id
    fee {
      id
      identifier
      feeManager {
        release {
          id
        }
      }
    }
    ...ManagementFeeSetting
    ...PerformanceFeeSetting
    ...EntranceRateBurnFeeSetting
    ...EntranceRateDirectFeeSetting
  }

```
  fragment ManagementFeeSetting on ManagementFeeSetting {
    scaledPerSecondRate
  }
```
```
  fragment PerformanceFeeSetting on PerformanceFeeSetting {
    rate
    period
  }
```
```
  fragment EntranceRateBurnFeeSetting on EntranceRateBurnFeeSetting {
    rate
  }
```
```
  fragment EntranceRateDirectFeeSetting on EntranceRateDirectFeeSetting {
    rate
  }
```
```
  query FundPolicies($comptrollerProxy: ID!) {
    comptrollerProxy(id: $comptrollerProxy) {
      id
      policySettings {
        id
        policy {
          id
        }
        ...AdapterBlacklistSetting
        ...AdapterWhitelistSetting
        ...AssetBlacklistSetting
        ...AssetWhitelistSetting
        ...InvestorWhitelistSetting
        ...MaxConcentrationSetting
        ...MinMaxInvestmentSetting
        ...BuySharesCallerWhitelistSetting
        ...GuaranteedRedemptionSetting
      }
    }
  }

```
```
  fragment AdapterBlacklistSetting on AdapterBlacklistSetting {
    listed
    enabled
  }
```
```
  fragment AdapterWhitelistSetting on AdapterWhitelistSetting {
    listed
    enabled
  }
```
```
  fragment AssetBlacklistSetting on AssetBlacklistSetting {
    listed
    enabled
  }
```
```
  fragment AssetWhitelistSetting on AssetWhitelistSetting {
    listed
    enabled
  }
```
```
  fragment InvestorWhitelistSetting on InvestorWhitelistSetting {
    enabled
    listedInvestors: listed(first: 1000) {
      id
    }
  }
```
```
  fragment MaxConcentrationSetting on MaxConcentrationSetting {
    enabled
    maxConcentration
  }
```
```
  fragment MinMaxInvestmentSetting on MinMaxInvestmentSetting {
    enabled
    minInvestmentAmount
    maxInvestmentAmount
  }
```
```
  fragment BuySharesCallerWhitelistSetting on BuySharesCallerWhitelistSetting {
    enabled
    listed
  }
```
```
  fragment GuaranteedRedemptionSetting on GuaranteedRedemptionSetting {
    enabled
    startTimestamp
    duration
  }
```
#### OffchainFundDetails

```
  query OffchainFundDetails($address: String!) {
    fund(where: { address: $address }) {
      id
      description
      email
      managerDescription
      postalAddress
      strategies(orderBy: { name: asc }) {
        id
        name
      }
      telegram
      twitter
      website
    }
  }
```
```
  mutation OffchainUpsertFund(
    $address: String!
    $description: String
    $email: String
    $managerDescription: String
    $postalAddress: String
    $strategies: [String!]
    $telegram: String
    $twitter: String
    $website: String
  ) {
    upsertFund(
      address: $address
      description: $description
      email: $email
      managerDescription: $managerDescription
      postalAddress: $postalAddress
      strategies: $strategies
      telegram: $telegram
      twitter: $twitter
      website: $website
    ) {
      id
    }
  }
```