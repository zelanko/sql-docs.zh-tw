---
title: mssqlctl 應用程式參考
titleSuffix: SQL Server big data clusters
description: Mssqlctl 應用程式命令的參考文件。
author: rothja
ms.author: jroth
manager: jroth
ms.date: 05/22/2019
ms.topic: reference
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 75ada3528ab287cf49f717f99efa2405e4aad1db
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "66800953"
---
# <a name="mssqlctl-app"></a>mssqlctl app

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

下列文章提供的參考**應用程式**中的命令**mssqlctl**工具。 如需其他詳細資訊**mssqlctl**命令，請參閱[mssqlctl 參考](reference-mssqlctl.md)。

## <a name="commands"></a>命令
|     |     |
| --- | --- |
[mssqlctl 應用程式範本](reference-mssqlctl-app-template.md) | 範本。
[mssqlctl 應用程式初始化](#mssqlctl-app-init) | 新應用程式基本架構著手進行。
[mssqlctl 應用程式建立](#mssqlctl-app-create) | 建立應用程式。
[mssqlctl 應用程式更新](#mssqlctl-app-update) | 更新應用程式。
[mssqlctl 應用程式清單](#mssqlctl-app-list) | 列出應用程式。
[mssqlctl app delete](#mssqlctl-app-delete) | 刪除應用程式。
[mssqlctl 應用程式執行](#mssqlctl-app-run) | 執行應用程式。
[mssqlctl 應用程式描述](#mssqlctl-app-describe) | 說明應用程式。
## <a name="mssqlctl-app-init"></a>mssqlctl 應用程式初始化
可協助您著手進行新的應用程式基本架構和/或根據執行階段環境的規格檔案。
```bash
mssqlctl app init [--spec -s] 
                  [--name -n]  
                  [--version -v]  
                  [--template -t]  
                  [--destination -d]  
                  [--url -u]
```
### <a name="examples"></a>範例
建立新的應用程式的結構`spec.yaml`只。
```bash
mssqlctl app init --spec
```
建立新 R 應用程式的應用程式基本架構為基礎的結構`r`範本。
```bash
mssqlctl app init --name reduce --template r
```
建立新 Python 應用程式的應用程式基本架構為基礎的結構`python`範本。
```bash
mssqlctl app init --name reduce --template python
```
建立新 SSIS 應用程式的應用程式基本架構為基礎的結構`ssis`範本。
```bash
mssqlctl app init --name reduce --template ssis            
```
### <a name="optional-parameters"></a>選擇性參數
#### `--spec -s`
產生只是應用程式 spec.yaml。
#### `--name -n`
應用程式名稱
#### `--version -v`
應用程式版本。
#### `--template -t`
範本名稱。 如需完整清單，關閉執行支援的範本名稱 `mssqlctl app template list`
#### `--destination -d`
放置應用程式基本架構的位置。 預設： 目前的工作目錄。
#### `--url -u`
指定不同的範本存放庫位置。 預設值： https://github.com/Microsoft/SQLBDC-AppDeploy.git
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
## <a name="mssqlctl-app-create"></a>mssqlctl 應用程式建立
建立應用程式。
```bash
mssqlctl app create --spec -s 
                    
```
### <a name="examples"></a>範例
從包含有效的 spec.yaml 部署規格的目錄中建立新的應用程式。
```bash
mssqlctl app create --spec /path/to/dir/with/spec/yaml
```
### <a name="required-parameters"></a>必要參數
#### `--spec -s`
描述應用程式的 YAML 規格的檔案與目錄路徑。
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
## <a name="mssqlctl-app-update"></a>mssqlctl 應用程式更新
更新應用程式。
```bash
mssqlctl app update [--spec -s] 
                    [--yes -y]
```
### <a name="examples"></a>範例
更新現有的應用程式，從包含有效的 spec.yaml 部署規格的目錄。
```bash
mssqlctl app update --spec /path/to/dir/with/spec/yaml    
```
### <a name="optional-parameters"></a>選擇性參數
#### `--spec -s`
描述應用程式的 YAML 規格的檔案與目錄路徑。
#### `--yes -y`
不提示確認時從 CWD spec.yaml 檔案將應用程式更新。
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
## <a name="mssqlctl-app-list"></a>mssqlctl 應用程式清單
列出應用程式。，
```bash
mssqlctl app list [--name -n] 
                  [--version -v]
```
### <a name="examples"></a>範例
列出依名稱和版本的應用程式。
```bash
mssqlctl app list --name reduce  --version v1
```
依名稱列出所有的應用程式版本。
```bash
mssqlctl app list --name reduce
```
依名稱列出所有的應用程式版本。
```bash
mssqlctl app list
```
### <a name="optional-parameters"></a>選擇性參數
#### `--name -n`
應用程式名稱
#### `--version -v`
應用程式版本。
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
## <a name="mssqlctl-app-delete"></a>mssqlctl 應用程式刪除
刪除應用程式。
```bash
mssqlctl app delete --name -n 
                    --version -v
```
### <a name="examples"></a>範例
刪除應用程式的名稱和版本。
```bash
mssqlctl app delete --name reduce --version v1    
```
### <a name="required-parameters"></a>必要參數
#### `--name -n`
應用程式名稱
#### `--version -v`
應用程式版本。
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
## <a name="mssqlctl-app-run"></a>mssqlctl 應用程式執行
執行應用程式。
```bash
mssqlctl app run --name -n 
                 --version -v  
                 [--inputs]
```
### <a name="examples"></a>範例
執行應用程式不含輸入參數。
```bash
mssqlctl app run --name reduce --version v1
```
執行應用程式與 1 個輸入參數。
```bash
mssqlctl app run --name reduce --version v1 --inputs x=10
```
執行應用程式與多個輸入參數。
```bash
mssqlctl app run --name reduce --version v1 --inputs x=10,y5.6    
```
### <a name="required-parameters"></a>必要參數
#### `--name -n`
應用程式名稱
#### `--version -v`
應用程式版本。
### <a name="optional-parameters"></a>選擇性參數
#### `--inputs`
應用程式中的輸入參數 CSV`name=value`格式。
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
## <a name="mssqlctl-app-describe"></a>mssqlctl 應用程式描述
描述應用程式。
```bash
mssqlctl app describe [--spec -s] 
                      [--name -n]  
                      [--version -v]
```
### <a name="examples"></a>範例
描述應用程式。
```bash
mssqlctl app describe --name reduce --version v1    
```
### <a name="optional-parameters"></a>選擇性參數
#### `--spec -s`
描述應用程式的 YAML 規格的檔案與目錄路徑。
#### `--name -n`
應用程式名稱
#### `--version -v`
應用程式版本。
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