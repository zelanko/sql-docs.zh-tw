---
title: mssqlctl 叢集組態參考
titleSuffix: SQL Server big data clusters
description: Mssqlctl 叢集命令的參考文件。
author: rothja
ms.author: jroth
manager: craigg
ms.date: 04/23/2019
ms.topic: reference
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 3a4693c5ffb68ad555d97d02f983fadf4e6bbd9a
ms.sourcegitcommit: bd5f23f2f6b9074c317c88fc51567412f08142bb
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/24/2019
ms.locfileid: "63473301"
---
# <a name="mssqlctl-cluster-config"></a>mssqlctl cluster config

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

下列文章提供的參考**叢集組態**中的命令**mssqlctl**工具。 如需其他詳細資訊**mssqlctl**命令，請參閱[mssqlctl 參考](reference-mssqlctl.md)。

## <a name="commands"></a>命令
|     |     |
| --- | --- |
[mssqlctl cluster config get](#mssqlctl-cluster-config-get) | 取得叢集設定-kube 組態需要您的系統上。
[mssqlctl 叢集組態 init](#mssqlctl-cluster-config-init) | 初始化叢集組態。
[mssqlctl 叢集組態清單](#mssqlctl-cluster-config-list) | 列出可用的設定檔選項。
[mssqlctl 叢集組態區段](reference-mssqlctl-cluster-config-section.md) | 使用組態檔的個別區段的命令。
## <a name="mssqlctl-cluster-config-get"></a>取得 mssqlctl 叢集組態
取得 SQL Server 巨量資料叢集的目前組態檔。
```bash
mssqlctl cluster config get --name -n 
                            [--output-file -f]
```
### <a name="required-parameters"></a>必要參數
#### `--name -n`
Kubernetes 命名空間所使用的叢集名稱。
### <a name="optional-parameters"></a>選擇性參數
#### `--output-file -f`
若要將結果儲存在輸出檔。 預設值： 導向至 stdout。
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
## <a name="mssqlctl-cluster-config-init"></a>mssqlctl 叢集組態 init
初始化使用者指定的預設型別為基礎的叢集組態檔。
```bash
mssqlctl cluster config init [--target -t] 
                             [--src -s]
```
### <a name="optional-parameters"></a>選擇性參數
#### `--target -t`
您要用來放置，設定檔預設為使用自訂 config.json cwd 檔案路徑。
#### `--src -s`
組態來源: ['aks-dev-test.json'，' kubeadm-dev-test.json'，' minikube-dev-test.json']
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
## <a name="mssqlctl-cluster-config-list"></a>mssqlctl 叢集組態清單
列出可用的設定檔選擇用於叢集組態 init
```bash
mssqlctl cluster config list [--config-file -f] 
                             
```
### <a name="optional-parameters"></a>選擇性參數
#### `--config-file -f`
預設組態檔中: ['aks-dev-test.json'，' kubeadm-dev-test.json'，' minikube-dev-test.json']
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