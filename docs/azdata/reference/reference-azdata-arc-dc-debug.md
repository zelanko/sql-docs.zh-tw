---
title: azdata arc dc debug reference
titleSuffix: SQL Server big data clusters
description: azdata arc dc debug 命令的參考文章。
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: seanw
ms.date: 09/22/2020
ms.topic: reference
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: bfb4c13f262609328bf73dca282f9d3445a8bf8c
ms.sourcegitcommit: 29a2be59c56f8a4b630af47760ef38d2bf56a3eb
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/22/2020
ms.locfileid: "92358796"
---
# <a name="azdata-arc-dc-debug"></a>azdata arc dc debug

適用於 [!INCLUDE [azure-data-cli-azdata](../../includes/azure-data-cli-azdata.md)]

下列文章提供 **azdata** 工具中 **sql** 命令的參考。 如需其他 **azdata** 命令的詳細資訊，請參閱 [azdata 參考](reference-azdata.md)

## <a name="commands"></a>命令

|命令|描述|
| --- | --- |
[azdata arc dc debug copy-logs](#azdata-arc-dc-debug-copy-logs) | 複製記錄。
[azdata arc dc debug dump](#azdata-arc-dc-debug-dump) | 觸發記憶體傾印。
## <a name="azdata-arc-dc-debug-copy-logs"></a>azdata arc dc debug copy-logs
從資料控制器複製偵錯記錄 - 系統需要 Kubernetes 設定。
```bash
azdata arc dc debug copy-logs --namespace -ns 
                              [--container -c]  
                              
[--target-folder -d]  
                              
[--pod]  
                              
[--resource-kind -rk]  
                              
[--resource-name -rn]  
                              
[--timeout -t]  
                              
[--skip-compress -sc]  
                              
[--exclude-dumps -ed]
```
### <a name="required-parameters"></a>必要參數
#### `--namespace -ns`
資料控制器的 Kubernetes 命名空間。
### <a name="optional-parameters"></a>選擇性參數
#### `--container -c`
複製具有類似名稱的容器記錄 (選擇性)，依預設複製所有容器的記錄檔。 無法多次指定。 如果多次指定，則會使用最後一個
#### `--target-folder -d`
要將記錄複製到其中的目標資料夾路徑。 (選擇性) 依預設，會在本機資料夾中建立結果。  無法多次指定。 如果多次指定，則會使用最後一個
#### `--pod`
複製具有類似名稱的 Pod 記錄。 (選擇性) 根據預設，會複製所有 Pod 的記錄檔。 無法多次指定。 如果多次指定，則會使用最後一個
#### `--resource-kind -rk`
複製特定資源種類的記錄。 無法多次指定。 如果多次指定，將會使用最後一個。 若已指定，則也應指定 --resource-name 以識別資源。
#### `--resource-name -rn`
複製指定名稱之資源的記錄。 無法多次指定。 如果多次指定，將會使用最後一個。 若已指定，則也應指定 --resource-kind 以識別資源。
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
## <a name="azdata-arc-dc-debug-dump"></a>azdata arc dc debug dump
觸發記憶體傾印並將其容器中複製出來 - 系統需要 Kubernetes 設定。
```bash
azdata arc dc debug dump --namespace -ns 
                         [--container -c]  
                         
[--target-folder -d]
```
### <a name="required-parameters"></a>必要參數
#### `--namespace -ns`
資料控制器的 Kubernetes 命名空間。
### <a name="optional-parameters"></a>選擇性參數
#### `--container -c`
要觸發以傾印執行中處理序的目標容器。
`controller`
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

