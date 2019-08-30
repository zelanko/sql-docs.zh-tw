---
title: azdata bdc 應用程式狀態參考
titleSuffix: SQL Server big data clusters
description: Azdata bdc 應用程式狀態命令的參考文章。
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 08/28/2019
ms.topic: reference
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 7ebf442b3bf87960d081bfe4b0867cdd082ec22a
ms.sourcegitcommit: 5e45cc444cfa0345901ca00ab2262c71ba3fd7c6
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2019
ms.locfileid: "70158093"
---
# <a name="azdata-bdc-app-status"></a>azdata bdc 應用程式狀態

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]  

本文是**azdata**的參考文章。 

## <a name="commands"></a>命令
|     |     |
| --- | --- |
[azdata bdc 應用程式狀態顯示](#azdata-bdc-app-status-show) | App service 狀態。
## <a name="azdata-bdc-app-status-show"></a>azdata bdc 應用程式狀態顯示
App service 狀態。
```bash
azdata bdc app status show [--resource -r] 
                           [--all -a]
```
### <a name="examples"></a>範例
取得應用程式服務的狀態。
```bash
azdata bdc app status show
```
取得具有所有實例之 app service 的狀態。
```bash
azdata bdc app status show --all
```
取得 app service 中 appproxy 資源的狀態。
```bash
azdata bdc app status show --resource appproxy
```
### <a name="optional-parameters"></a>選擇性參數
#### `--resource -r`
在此服務中取得此資源。
#### `--all -a`
顯示服務內每個資源的所有實例。
### <a name="global-arguments"></a>全域引數
#### `--debug`
增加記錄詳細資訊，以顯示所有偵錯記錄。
#### `--help -h`
顯示此說明訊息並結束。
#### `--output -o`
輸出格式。  允許的值：json、jsonc、table、tsv。  預設值：json。
#### `--query -q`
JMESPath 查詢字串。 如需詳細資訊和範例，請參閱 [http://jmespath.org/](http://jmespath.org/])。
#### `--verbose`
增加記錄詳細資訊。 使用 --debug 來取得完整偵錯記錄。

## <a name="next-steps"></a>後續步驟

- 如需其他 **azdata** 命令的詳細資訊，請參閱 [azdata 參考](reference-azdata.md)。 

- 如需如何安裝 **azdata** 工具的詳細資訊，請參閱[安裝 azdata 來管理 SQL Server 2019 巨量資料叢集](deploy-install-azdata.md)。
