---
title: azdata bdc debug 參考
titleSuffix: SQL Server big data clusters
description: Azdata bdc 偵錯工具命令的參考文章。
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 07/24/2019
ms.topic: reference
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 38c327287273ae6596326d88d9e0d67c8e014d47
ms.sourcegitcommit: 1f222ef903e6aa0bd1b14d3df031eb04ce775154
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/23/2019
ms.locfileid: "68426228"
---
# <a name="azdata-bdc-debug"></a>azdata bdc debug

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

下列文章提供**azdata**工具中**bdc debug**命令的參考。 如需其他**azdata**命令的詳細資訊, 請參閱[azdata 參考](reference-azdata.md)。

## <a name="commands"></a>命令
|     |     |
| --- | --- |
[azdata bdc debug 複製-記錄檔](#azdata-bdc-debug-copy-logs) | 複製記錄檔。
[azdata bdc debug dump](#azdata-bdc-debug-dump) | 觸發程式記錄傾印。
## <a name="azdata-bdc-debug-copy-logs"></a>azdata bdc debug 複製-記錄檔
在您的系統上需要複製 Big Data Cluster-kube config 的 debug 記錄檔。
```bash
azdata bdc debug copy-logs --namespace -n 
                           [--container -c]  
                           [--target-folder -d]  
                           [--pod -p]  
                           [--timeout -t]
```
### <a name="required-parameters"></a>必要參數
#### `--namespace -n`
Big data cluster name, 用於 kubernetes 命名空間。
### <a name="optional-parameters"></a>選擇性參數
#### `--container -c`
複製具有類似名稱 (選擇性) 之容器的記錄, 並依預設複製所有容器的記錄檔。 不能指定多次。 如果多次指定, 則會使用最後一個
#### `--target-folder -d`
要將記錄複製到其中的目的檔案夾路徑。 (選擇性) 根據預設, 會在本機資料夾中建立結果。  不能指定多次。 如果多次指定, 則會使用最後一個
#### `--pod -p`
複製具有類似名稱的 pod 記錄檔。 (選擇性) 根據預設, 會複製所有 pod 的記錄檔。 不能指定多次。 如果多次指定, 則會使用最後一個
#### `--timeout -t`
等候命令完成的秒數。 預設值為 0, 表示無限制
### <a name="global-arguments"></a>全域引數
#### `--debug`
增加記錄詳細資訊, 以顯示所有的調試記錄。
#### `--help -h`
顯示此說明訊息並結束。
#### `--output -o`
輸出格式。  允許的值: json、jsonc、table、tsv。  預設值: json。
#### `--query -q`
JMESPath 查詢字串。 如[http://jmespath.org/](http://jmespath.org/])需詳細資訊和範例, 請參閱。
#### `--verbose`
增加記錄詳細資訊。 使用--debug 取得完整的 debug 記錄檔。
## <a name="azdata-bdc-debug-dump"></a>azdata bdc debug dump
觸發記錄傾印, 並從容器 kube 設定將它複製到您的系統上。
```bash
azdata bdc debug dump --namespace -n 
                      --container -c  
                      [--target-folder -d]
```
### <a name="required-parameters"></a>必要參數
#### `--namespace -n`
Big data cluster name, 用於 kubernetes 命名空間。
#### `--container -c`
複製具有類似名稱 (選擇性) 之容器的記錄, 並依預設複製所有容器的記錄檔。 不能指定多次。 如果多次指定, 則會使用最後一個
### <a name="optional-parameters"></a>選擇性參數
#### `--target-folder -d`
要將記錄複製到其中的目的檔案夾路徑。 (選擇性) 根據預設, 會在本機資料夾中建立結果。  不能指定多次。 如果多次指定, 則會使用最後一個`./output/dump`
### <a name="global-arguments"></a>全域引數
#### `--debug`
增加記錄詳細資訊, 以顯示所有的調試記錄。
#### `--help -h`
顯示此說明訊息並結束。
#### `--output -o`
輸出格式。  允許的值: json、jsonc、table、tsv。  預設值: json。
#### `--query -q`
JMESPath 查詢字串。 如[http://jmespath.org/](http://jmespath.org/])需詳細資訊和範例, 請參閱。
#### `--verbose`
增加記錄詳細資訊。 使用--debug 取得完整的 debug 記錄檔。

## <a name="next-steps"></a>後續步驟

如需其他**azdata**命令的詳細資訊, 請參閱[azdata 參考](reference-azdata.md)。 如需有關如何安裝**azdata**工具的詳細資訊, 請參閱[install azdata to manage SQL Server 2019 big data](deploy-install-azdata.md)叢集。
