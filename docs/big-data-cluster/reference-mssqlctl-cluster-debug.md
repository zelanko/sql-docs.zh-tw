---
title: mssqlctl 叢集偵錯參考
titleSuffix: SQL Server big data clusters
description: Mssqlctl 叢集偵錯 命令的參考文件。
author: rothja
ms.author: jroth
manager: jroth
ms.date: 05/22/2019
ms.topic: reference
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 4eafc3838d153a2616e34e98aed041374c04292d
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "66779396"
---
# <a name="mssqlctl-cluster-debug"></a>mssqlctl cluster debug

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

下列文章提供的參考**叢集偵錯**中的命令**mssqlctl**工具。 如需其他詳細資訊**mssqlctl**命令，請參閱[mssqlctl 參考](reference-mssqlctl.md)。

## <a name="commands"></a>命令
|     |     |
| --- | --- |
[mssqlctl cluster debug copy-logs](#mssqlctl-cluster-debug-copy-logs) | 複製記錄檔。
[mssqlctl 叢集偵錯傾印](#mssqlctl-cluster-debug-dump) | 觸發程序記錄傾印。
## <a name="mssqlctl-cluster-debug-copy-logs"></a>mssqlctl cluster debug copy-logs
從叢集複製偵錯記錄檔-kube 設定需要您的系統上。
```bash
mssqlctl cluster debug copy-logs --namespace -n 
                                 [--container -c]  
                                 [--target-folder -d]  
                                 [--pod -p]  
                                 [--timeout -t]
```
### <a name="required-parameters"></a>必要參數
#### `--namespace -n`
Kubernetes 命名空間所使用的叢集名稱。
### <a name="optional-parameters"></a>選擇性參數
#### `--container -c`
複製記錄檔名稱類似的容器，選擇性，預設會複製的所有容器的記錄檔。 不能指定多次。 如果指定了多次，最後一個會使用
#### `--target-folder -d`
複製記錄檔的目標資料夾路徑。 選擇性，預設會建立結果中的本機資料夾。  不能指定多次。 如果指定了多次，最後一個會使用
#### `--pod -p`
將複製的 pod 名稱類似的記錄檔。 （選擇性） 根據預設所有 pod 的複製記錄檔。 不能指定多次。 如果指定了多次，最後一個會使用
#### `--timeout -t`
等候命令完成的秒數。 預設值是 0 表示無限制
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
## <a name="mssqlctl-cluster-debug-dump"></a>mssqlctl 叢集偵錯傾印
觸發記錄傾印，並將它複製出來中，從容器-kube 設定需要您的系統上。
```bash
mssqlctl cluster debug dump --namespace -n 
                            --container -c  
                            [--target-folder -d]
```
### <a name="required-parameters"></a>必要參數
#### `--namespace -n`
Kubernetes 命名空間所使用的叢集名稱。
#### `--container -c`
複製記錄檔名稱類似的容器，選擇性，預設會複製的所有容器的記錄檔。 不能指定多次。 如果指定了多次，最後一個會使用
### <a name="optional-parameters"></a>選擇性參數
#### `--target-folder -d`
複製記錄檔的目標資料夾路徑。 選擇性，預設會建立結果中的本機資料夾。  不能指定多次。 如果指定了多次，最後一個會使用 `./output/dump`
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

如需其他詳細資訊**mssqlctl**命令，請參閱[mssqlctl 參考](reference-mssqlctl.md)。 如需有關如何安裝**mssqlctl**工具，請參閱[安裝來管理 SQL Server 2019 巨量資料叢集 mssqlctl](deploy-install-mssqlctl.md)。