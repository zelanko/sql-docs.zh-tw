---
title: mssqlctl 叢集偵錯參考
titleSuffix: SQL Server big data clusters
description: Mssqlctl 叢集命令的參考文件。
author: rothja
ms.author: jroth
manager: craigg
ms.date: 02/28/2019
ms.topic: reference
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: b12b0421cf32a36cfd6d681bc90ad9ca7c3f9209
ms.sourcegitcommit: 2de5446fbc57787f18a907dd5deb02a7831ec07d
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/02/2019
ms.locfileid: "58860549"
---
# <a name="mssqlctl-cluster-debug"></a>mssqlctl cluster debug

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

下列文章提供的參考**叢集偵錯**中的命令**mssqlctl**工具。 如需其他詳細資訊**mssqlctl**命令，請參閱[mssqlctl 參考](reference-mssqlctl.md)。

## <a id="commands"></a> 命令

|||
|---|---|
| [copy-logs](#copy-logs) | 複製記錄檔。 |
| [dump](#dump) | 觸發程序記錄傾印。 |

## <a id="copy-logs"></a> 叢集偵錯複製記錄檔

複製記錄檔。

```
mssqlctl cluster debug copy-logs
   --namespace
   [--container]
   [--pod]
   [--target-folder]
   [--timeout]
```

### <a name="parameters"></a>參數

| 參數 | 描述 |
|---|---|
| **--namespace -n** | Kubernetes 命名空間所使用的叢集名稱。 必要。 |
| **--container -c** | 複製記錄檔名稱類似的容器，選擇性，預設會複製的所有容器的記錄檔。 不能指定多次。 如果指定了多次，最後一個會使用。 |
| **--pod -p** | 將複製的 pod 名稱類似的記錄檔。 （選擇性） 根據預設所有 pod 的複製記錄檔。 不能指定多次。 如果指定了多次，最後一個會使用。 |
| **--target-folder -d** | 複製記錄檔的目標資料夾路徑。 選擇性，預設會建立結果中的本機資料夾。  不能指定多次。 如果指定了多次，最後一個會使用。 |
| **--timeout -t** | 等候命令完成的秒數。 預設值為 0 表示無限制。 |

## <a id="dump"></a> 叢集偵錯傾印

觸發程序記錄傾印。

```
mssqlctl cluster debug dump
   [--container]
   [--namespace]
   --target-folder
```

### <a name="parameters"></a>參數

| 參數 | 描述 |
|---|---|
| **--container -c** | 複製記錄檔名稱類似的容器，選擇性，預設會複製的所有容器的記錄檔。 不能指定多次。 如果指定了多次，最後一個會使用。  允許的值： mssql 控制站。 |
| **--namespace -n** | Kubernetes 命名空間所使用的叢集名稱。 必要。 |
| **--target-folder -d** | 複製記錄檔的目標資料夾路徑。 選擇性，預設會建立結果中的本機資料夾。  不能指定多次。 如果指定了多次，最後一個會使用。  預設值： `./output/dump`。 必要。 |

## <a name="next-steps"></a>後續步驟

如需其他詳細資訊**mssqlctl**命令，請參閱[mssqlctl 參考](reference-mssqlctl.md)。 如需有關如何安裝**mssqlctl**工具，請參閱[安裝來管理 SQL Server 2019 巨量資料叢集 mssqlctl](deploy-install-mssqlctl.md)。