#### Account

```
  fragment AccountInfo on Account {
    id
    accountProfile {
      username
      name
      email
      avatarUrl
      telegram
      websiteUrl
      twitter
      id
    }
  }
```

```
  fragment AccountAuthInfo on Account {
    id
    auth {
      authenticator
      google
      password
      recovery
    }
  }
```

```
  query Me {
    me {
      ...AccountInfo
    }
  }
```

```
  query AccountAuth {
    me {
      ...AccountAuthInfo
    }
  }
```

```
  query AccountDetails($id: ID!) {
    account(id: $id) {
      authUser
      id
      firstSeen
      investor
      investorSince
      manager
      managerSince
    }
  }
```

```
  query LastAccountSharesAction($account: ID!, $vault: String!, $from: BigInt!) {
    account(id: $account) {
      id
      investments(where: { fund: $vault }) {
        id
        stateHistory(orderBy: timestamp, orderDirection: desc, where: { timestamp_gt: $from }, first: 1000) {
          id
          timestamp
          changes {
            id
            __typename
          }
        }
      }
    }
  }
```

#### Asset

```
  fragment Asset on Asset {
    id
    name
    symbol
    decimals
    type
  }
```

```
  fragment AssetWithPrice on Asset {
    ...Asset
    price {
      id
      price
      timestamp
    }
  }
```

```
  fragment FundDetails on Fund {
    id
    accessor {
      id
      sharesActionTimelock
      denominationAsset {
        ...AssetWithPrice
      }
    }
    inception
    investmentCount
    name
    manager {
      id
      manager
    }
    release {
      id
    }
    shares {
      id
      totalSupply
    }
  }
```

```
  query FundDetails($id: ID!) {
    fund(id: $id) {
      ...FundDetails
    }
  }
```

```
  query FundDetailsFromComptroller($comptroller: String!) {
    funds(where: { accessor: $comptroller }, first: 1) {
      ...FundDetails
    }
  }
```

```
  query FundInvestmentsCount($id: ID!) {
    fund(id: $id) {
      id
      investmentCount
    }
  }
```

```
  query FundInvestments($id: ID!) {
    fund(id: $id) {
      id
      investments(first: 1000) {
        id
        since
        investor {
          id
        }
        shares
      }
    }
  }
```

```
  query FundAuthorizedUsers($id: ID!) {
    fund(id: $id) {
      id
      accessor {
        id
        authUsers(first: 1000) {
          id
        }
      }
    }
  }
```
