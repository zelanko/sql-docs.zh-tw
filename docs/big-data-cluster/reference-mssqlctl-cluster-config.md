---
title: mssqlctl 叢集組態參考
titleSuffix: SQL Server big data clusters
description: Mssqlctl 叢集命令的參考文件。
author: rothja
ms.author: jroth
manager: craigg
ms.date: 05/22/2019
ms.topic: reference
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 984a3c50ac691df3759edc161baabc533bd9456f
ms.sourcegitcommit: be09f0f3708f2e8eb9f6f44e632162709b4daff6
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/21/2019
ms.locfileid: "65993338"
---
# <a name="mssqlctl-cluster-config"></a>mssqlctl cluster config

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

下列文章提供的參考**叢集組態**中的命令**mssqlctl**工具。 如需其他詳細資訊**mssqlctl**命令，請參閱[mssqlctl 參考](reference-mssqlctl.md)。

## <a name="commands"></a>命令
|     |     |
| --- | --- |
[mssqlctl 叢集 config show](#mssqlctl-cluster-config-show) | 取得 SQL Server 巨量資料叢集的目前組態。
[mssqlctl 叢集組態 init](#mssqlctl-cluster-config-init) | 初始化可以搭配叢集的叢集組態設定檔建立。
[mssqlctl 叢集組態清單](#mssqlctl-cluster-config-list) | 列出可用的設定檔選項。
[mssqlctl 叢集組態區段](reference-mssqlctl-cluster-config-section.md) | 使用 叢集組態檔的個別區段的命令。
## <a name="mssqlctl-cluster-config-show"></a>mssqlctl 叢集 config show
取得 SQL Server 巨量資料叢集的目前組態檔，並將它輸出到目標檔案或很將它列印至主控台。
```bash
mssqlctl cluster config show [--target -t] 
                             [--force -f]
```
### <a name="examples"></a>範例
顯示在主控台中的叢集組態
```bash
mssqlctl cluster config show
```
### <a name="optional-parameters"></a>選擇性參數
#### `--target -t`
若要將結果儲存在輸出檔。 預設值： 導向至 stdout。
#### `--force -f`
強制覆寫目標檔案。
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
初始化可以搭配叢集的叢集組態設定檔建立。 可以從 3 個選項的引數中指定組態設定檔的特定來源。
```bash
mssqlctl cluster config init [--target -t] 
                             [--src -s]  
                             [--force -f]
```
### <a name="examples"></a>範例
引導式叢集組態 init 體驗-您將收到提示所需的值。
```bash
mssqlctl cluster config init
```
叢集使用的引數的組態初始化，則會建立 aks-開發 / 測試中的組態設定檔。 / custom.json。
```bash
mssqlctl cluster config init --src aks-dev-test.json --target custom.json
```
### <a name="optional-parameters"></a>選擇性參數
#### `--target -t`
您要用來放置，組態設定檔預設為使用自訂 config.json cwd 檔案路徑。
#### `--src -s`
組態設定檔的來源: ['aks-dev-test.json'，' kubeadm-dev-test.json'，' minikube-dev-test.json']
#### `--force -f`
強制覆寫目標檔案。
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
mssqlctl cluster config list [--config-file -c] 
                             
```
### <a name="examples"></a>範例
顯示所有可用的組態設定檔名稱。
```bash
mssqlctl cluster config list
```
顯示特定的組態設定檔的 json。
```bash
mssqlctl cluster config list --config-file aks-dev-test.json
```
### <a name="optional-parameters"></a>選擇性參數
#### `--config-file -c`
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