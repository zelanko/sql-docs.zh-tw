---
title: mssqlctl bdc 組態參考
titleSuffix: SQL Server big data clusters
description: Mssqlctl bdc 命令的參考文件。
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 06/26/2019
ms.topic: reference
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: f6aee38bd11d226ba324153b76c750ba57eb9fb8
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/15/2019
ms.locfileid: "67958170"
---
# <a name="mssqlctl-bdc-config"></a>mssqlctl bdc 組態

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

下列文章提供的參考**bdc config**中的命令**mssqlctl**工具。 如需其他詳細資訊**mssqlctl**命令，請參閱[mssqlctl 參考](reference-mssqlctl.md)。

## <a name="commands"></a>命令
|     |     |
| --- | --- |
[mssqlctl bdc config show](#mssqlctl-bdc-config-show) | 取得巨量資料叢集的目前組態。
[mssqlctl bdc config init](#mssqlctl-bdc-config-init) | 初始化可以與叢集搭配使用的組態設定檔建立巨量資料叢集。
[mssqlctl bdc 組態清單](#mssqlctl-bdc-config-list) | 列出可用的組態設定檔選項。
[mssqlctl bdc 組態區段](reference-mssqlctl-bdc-config-section.md) | 使用巨量資料叢集組態設定檔的個別區段的命令。
## <a name="mssqlctl-bdc-config-show"></a>mssqlctl bdc config show
取得巨量資料叢集的目前組態設定檔，並將它輸出到目標目錄或很將它列印至主控台。
```bash
mssqlctl bdc config show [--target -t] 
                         [--force -f]
```
### <a name="examples"></a>範例
在主控台中顯示 BDC 組態
```bash
mssqlctl bdc config show
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
## <a name="mssqlctl-bdc-config-init"></a>mssqlctl bdc config init
初始化可以與叢集搭配使用的組態設定檔建立巨量資料叢集。 可以從 3 個選項的引數中指定組態設定檔的特定來源。
```bash
mssqlctl bdc config init [--target -t] 
                         [--source -s]  
                         [--force -f]
```
### <a name="examples"></a>範例
引導式的 BDC config init 體驗-您會收到提示所需的值。
```bash
mssqlctl bdc config init
```
BDC config init 引數時，會建立 aks-開發 / 測試中的組態設定檔。 或自訂。
```bash
mssqlctl bdc config init --source aks-dev-test --target custom
```
### <a name="optional-parameters"></a>選擇性參數
#### `--target -t`
您要用來放置，組態設定檔預設為使用自訂 config.json cwd 檔案路徑。
#### `--source -s`
組態設定檔的來源: ['aks-開發 / 測試 '、 'kubeadm-開發 / 測試 '、' minikube-開發 / 測試 ']
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
## <a name="mssqlctl-bdc-config-list"></a>mssqlctl bdc 組態清單
列出可用的組態設定檔選擇，以用於 `bdc config init`
```bash
mssqlctl bdc config list [--config-profile -c] 
                         
```
### <a name="examples"></a>範例
顯示所有可用的組態設定檔名稱。
```bash
mssqlctl bdc config list
```
顯示特定的組態設定檔的 json。
```bash
mssqlctl bdc config list --config-profile aks-dev-test
```
### <a name="optional-parameters"></a>選擇性參數
#### `--config-profile -c`
預設組態設定檔: ['aks-開發 / 測試 '、 'kubeadm-開發 / 測試 '、' minikube-開發 / 測試 ']
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