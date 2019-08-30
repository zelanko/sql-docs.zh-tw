---
title: azdata bdc debug 參考
titleSuffix: SQL Server big data clusters
description: azdata bdc debug 命令的參考文章。
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 08/28/2019
ms.topic: reference
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 9e14528baf80d08841f6e9e17a0476dfa81fd48d
ms.sourcegitcommit: 5e45cc444cfa0345901ca00ab2262c71ba3fd7c6
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2019
ms.locfileid: "70153192"
---
# <a name="azdata-bdc-debug"></a>azdata bdc debug

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]  

本文是**azdata**的參考文章。 

## <a name="commands"></a>命令
|     |     |
| --- | --- |
[azdata bdc debug copy-logs](#azdata-bdc-debug-copy-logs) | 複製記錄。
[azdata bdc debug dump](#azdata-bdc-debug-dump) | 觸發程式記錄傾印。
## <a name="azdata-bdc-debug-copy-logs"></a>azdata bdc debug copy-logs
在您的系統上需要複製 Big Data Cluster-Kubernetes 設定的偵錯工具記錄檔。
```bash
azdata bdc debug copy-logs --namespace -n 
                           [--container -c]  
                           [--target-folder -d]  
                           [--pod -p]  
                           [--timeout -t]
```
### <a name="required-parameters"></a>必要參數
#### `--namespace -n`
巨量資料叢集名稱，用於 kubernetes 命名空間。
### <a name="optional-parameters"></a>選擇性參數
#### `--container -c`
複製具有類似名稱的容器記錄 (選擇性)，依預設複製所有容器的記錄檔。 無法多次指定。 如果多次指定，則會使用最後一個
#### `--target-folder -d`
要將記錄複製到其中的目標資料夾路徑。 (選擇性) 依預設，會在本機資料夾中建立結果。  無法多次指定。 如果多次指定，則會使用最後一個
#### `--pod -p`
複製具有類似名稱的 Pod 記錄。 (選擇性) 根據預設，會複製所有 Pod 的記錄檔。 無法多次指定。 如果多次指定，則會使用最後一個
#### `--timeout -t`
等待命令完成的秒數。 預設值為 0，表示無限制
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
## <a name="azdata-bdc-debug-dump"></a>azdata bdc debug dump
觸發記錄傾印, 並從容器 Kubernetes 設定將它複製到您的系統上。
```bash
azdata bdc debug dump --namespace -n 
                      --container -c  
                      [--target-folder -d]
```
### <a name="required-parameters"></a>必要參數
#### `--namespace -n`
巨量資料叢集名稱，用於 kubernetes 命名空間。
#### `--container -c`
複製具有類似名稱的容器記錄 (選擇性)，依預設複製所有容器的記錄檔。 無法多次指定。 如果多次指定，則會使用最後一個
### <a name="optional-parameters"></a>選擇性參數
#### `--target-folder -d`
要將記錄複製到其中的目標資料夾路徑。 (選擇性) 依預設，會在本機資料夾中建立結果。  無法多次指定。 如果多次指定，則會使用最後一個 `./output/dump`
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
