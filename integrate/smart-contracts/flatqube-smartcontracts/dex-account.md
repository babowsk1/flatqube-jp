---
description: Dexアカウントとは、Dexプール内を管理するためのロジックを規定しているものです。
---

# Dexアカウント

Dexプール内で行われるユーザートランザクション(トークンの引き出し/預け入れ、流動性の追加/削除、ペアの追加/交換)を管理するスマートコントラクトです。

次のクラスやインターフェースを継承しています：_DexContractBase, IDexAccount, IAcceptTokensTransferCallback, IUpgradableByRequest, IResetGas_

## ゲッター

### getRoot

特定のDexルートのルートアドレスを取得します。

```solidity
function getRoot() override external view responsible returns (address)
```

**リターン値:**

| タイプ     | 説明                                    |
| ------- | ------------------------------------- |
| address | Address of the account's root address |

### getOwner

アカウントの所有者を取得します。

```solidity
function getOwner() override external view responsible returns (address) 
```

**リターン値:**

| タイプ     | 説明            |
| ------- | ------------- |
| address | アカウント所有者のアドレス |

### getVersion

アカウントの現在のバージョンを取得します。

```solidity
function getVersion() override external view responsible returns (uint32)
```

**リターン値**

| タイプ    | 説明       |
| ------ | -------- |
| uint32 | 現在のバージョン |

### getVault

アカウントのヴォールトを取得します。

```solidity
function getVault() override external view responsible returns (address)
```

**リターン値:**

| タイプ     | 説明         |
| ------- | ---------- |
| address | ヴォールトのアドレス |

### getWalletData

token\_rootを使用して、指定されたトークンがウォレット一覧に存在するかどうかを調べ、存在する場合はウォレットのアドレスと残高をリターンし、存在しない場合はアドレスと残高にそれぞれ0をリターンします。

```solidity
function getWalletData(address token_root) override external view responsible returns (address wallet, uint128 balance)
```

**パラメータ:**

| 名称          | タイプ     | 説明          |
| ----------- | ------- | ----------- |
| token\_root | address | トークンルートアドレス |

| 名称      | タイプ     | 説明               |
| ------- | ------- | ---------------- |
| wallet  | address | 指定トークンのウォレットアドレス |
| balance | uint128 | ウォレット内のトークン残高    |

### getWallets

```solidity
function getWallets() external view returns (mapping(address => address))
```

このアカウントの全トークンウォレット一覧を取得します。

**リターン値:**

| タイプ     | 説明                       |
| ------- | ------------------------ |
| address | 特定のアカウントのトークンウォレットアドレス一覧 |

### getBalances

```solidity
function getBalances() external view returns (mapping(address => uint128))
```

このアカウントの全トークン残高一覧を取得します

**リターン値:**

| タイプ     | 説明                                |
| ------- | --------------------------------- |
| uint128 | 特定のアカウントの様々なトークンウォレットの全てのトークン残高一覧 |
