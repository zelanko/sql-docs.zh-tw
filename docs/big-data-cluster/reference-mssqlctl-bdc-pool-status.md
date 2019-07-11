---
title: mssqlctl bdc 集區狀態的參考
titleSuffix: SQL Server big data clusters
description: Mssqlctl bdc 集區狀態命令的參考文件。
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
manager: jroth
ms.date: 06/26/2019
ms.topic: reference
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 818773708087927b5c2f3ccea44ba52cd77e7a71
ms.sourcegitcommit: e0c55d919ff9cec233a7a14e72ba16799f4505b2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/10/2019
ms.locfileid: "67728566"
---
# <a name="mssqlctl-bdc-pool-status"></a>mssqlctl bdc 集區狀態

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

下列文章提供的參考**bdc 集區狀態**中的命令**mssqlctl**工具。 如需其他詳細資訊**mssqlctl**命令，請參閱[mssqlctl 參考](reference-mssqlctl.md)。

## <a name="commands"></a>命令
|     |     |
| --- | --- |
[mssqlctl bdc 集區狀態顯示](#mssqlctl-bdc-pool-status-show) | 集區狀態。
## <a name="mssqlctl-bdc-pool-status-show"></a>mssqlctl bdc 集區狀態顯示
集區狀態。
```bash
mssqlctl bdc pool status show --kind -k 
                              [--name -n]
```
### <a name="examples"></a>範例
取得儲存體集區的狀態。
```bash
mssqlctl bdc pool status show --kind storage --name default
```
取得資料集區的狀態。
```bash
mssqlctl bdc pool status show --kind data --name default
```
取得計算集區的狀態。
```bash
mssqlctl bdc pool status show --kind compute --name default
```
取得主要集區的狀態。
```bash
mssqlctl bdc pool status show --kind master --name default
```
取得 spark 集區的狀態。
```bash
mssqlctl bdc pool status show --kind spark --name default
```
### <a name="required-parameters"></a>必要參數
#### `--kind -k`
BDC 集區類型。
### <a name="optional-parameters"></a>選擇性參數
#### `--name -n`
BDC 集區名稱。
`default`
### <a name="global-arguments"></a>全域引數
#### `--debug`
增加記錄詳細程度以顯示所有偵錯記錄檔。
#### `--help -h`
顯示此說明訊息並結束。
#### `--output -o`
輸出格式。  允許的值： json、 jsonc、 table、 tsv。  預設值： json。
#### `--query -q`
JMESPath 查詢字串。 請參閱[ http://jmespath.org/ ](http://jmespath.org/])如需詳細資訊和範例。
#### `--verbose`
增加記錄詳細程度。 使用--debug 取得完整的偵錯記錄。

## <a name="next-steps"></a>後續步驟

如需有關如何安裝**mssqlctl**工具，請參閱[安裝來管理 SQL Server 2019 巨量資料叢集 mssqlctl](deploy-install-mssqlctl.md)。