---
title: azdata bdc debug 參考
titleSuffix: SQL Server big data clusters
description: azdata bdc debug 命令的參考文章。
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: seanw
ms.date: 09/22/2020
ms.topic: reference
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: fe9f79373bd26ab4b010c63487ffa38de44dae3b
ms.sourcegitcommit: d56f1eca807c55cf606a6316f3872585f014fec1
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/22/2020
ms.locfileid: "90914575"
---
# <a name="azdata-bdc-debug"></a>azdata bdc debug

適用於 `azdata`

下列文章提供 **azdata** 工具中 **sql** 命令的參考。 如需其他 **azdata** 命令的詳細資訊，請參閱 [azdata 參考](reference-azdata.md)

## <a name="commands"></a>命令

|命令|說明|
| --- | --- |
[azdata bdc debug copy-logs](#azdata-bdc-debug-copy-logs) | 複製記錄。
[azdata bdc debug dump](#azdata-bdc-debug-dump) | 觸發記憶體傾印。
## <a name="azdata-bdc-debug-copy-logs"></a>azdata bdc debug copy-logs
從巨量資料叢集中複製偵錯記錄 - 系統需要 Kubernetes 設定。
```bash
azdata bdc debug copy-logs --namespace -ns 
                           [--container -c]  
                           
[--target-folder -d]  
                           
[--pod -p]  
                           
[--timeout -t]  
                           
[--skip-compress -sc]  
                           
[--exclude-dumps -ed]
```
### <a name="required-parameters"></a>必要參數
#### `--namespace -ns`
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
#### `--skip-compress -sc`
是否要略過壓縮結果資料夾。 預設值為 False，表示會壓縮結果資料夾。
#### `--exclude-dumps -ed`
是否要從結果資料夾排除傾印。 預設值為 False，表示要包含傾印。
### <a name="global-arguments"></a>全域引數
#### `--debug`
增加記錄詳細資訊，以顯示所有偵錯記錄。
#### `--help -h`
顯示此說明訊息並結束。
#### `--output -o`
輸出格式。  允許的值：json、jsonc、table、tsv。  預設值：json。
#### `--query -q`
JMESPath 查詢字串。 如需詳細資訊和範例，請參閱 [http://jmespath.org/](http://jmespath.org)。
#### `--verbose`
增加記錄詳細資訊。 使用 --debug 來取得完整偵錯記錄。
## <a name="azdata-bdc-debug-dump"></a>azdata bdc debug dump
觸發記憶體傾印並將其容器中複製出來 - 系統需要 Kubernetes 設定。
```bash
azdata bdc debug dump --namespace -ns 
                      [--container -c]  
                      
[--target-folder -d]
```
### <a name="required-parameters"></a>必要參數
#### `--namespace -ns`
巨量資料叢集名稱，用於 kubernetes 命名空間。
### <a name="optional-parameters"></a>選擇性參數
#### `--container -c`
要觸發傾印執行中處理序 `controller` 的目標容器
#### `--target-folder -d`
要複製傾印的目標資料夾。`./output/dump`
### <a name="global-arguments"></a>全域引數
#### `--debug`
增加記錄詳細資訊，以顯示所有偵錯記錄。
#### `--help -h`
顯示此說明訊息並結束。
#### `--output -o`
輸出格式。  允許的值：json、jsonc、table、tsv。  預設值：json。
#### `--query -q`
JMESPath 查詢字串。 如需詳細資訊和範例，請參閱 [http://jmespath.org/](http://jmespath.org)。
#### `--verbose`
增加記錄詳細資訊。 使用 --debug 來取得完整偵錯記錄。

## <a name="next-steps"></a>後續步驟

如需其他 **azdata** 命令的詳細資訊，請參閱 [azdata 參考](reference-azdata.md)。 

如需如何安裝 **azdata** 工具的詳細資訊，請參閱[安裝 azdata](..\install\deploy-install-azdata.md)。

