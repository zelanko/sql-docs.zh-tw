---
title: mssqlctl 應用程式範本參考
titleSuffix: SQL Server big data clusters
description: Mssqlctl 應用程式範本命令的參考文件。
author: rothja
ms.author: jroth
manager: jroth
ms.date: 06/26/2019
ms.topic: reference
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 20d8b332643c9ef749aae5be0ab9e778a593d6ff
ms.sourcegitcommit: ce5770d8b91c18ba5ad031e1a96a657bde4cae55
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/25/2019
ms.locfileid: "67388188"
---
# <a name="mssqlctl-app-template"></a>mssqlctl app template

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

下列文章提供的參考**應用程式範本**中的命令**mssqlctl**工具。 如需其他詳細資訊**mssqlctl**命令，請參閱[mssqlctl 參考](reference-mssqlctl.md)。

## <a name="commands"></a>命令
|     |     |
| --- | --- |
[mssqlctl 應用程式範本清單](#mssqlctl-app-template-list) | 擷取支援的範本。
[mssqlctl 應用程式範本提取](#mssqlctl-app-template-pull) | 下載支援的範本。
## <a name="mssqlctl-app-template-list"></a>mssqlctl 應用程式範本清單
擷取在指定的 [URL] github 存放庫的支援的範本。
```bash
mssqlctl app template list [--url -u] 
                           
```
### <a name="examples"></a>範例
擷取預設範本儲存機制位置下的所有範本。
```bash
mssqlctl app template list
```
擷取不同的存放庫位置下的所有範本。
```bash
mssqlctl app template list --url https://github.com/diffrent/templates.git
```
### <a name="optional-parameters"></a>選擇性參數
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
## <a name="mssqlctl-app-template-pull"></a>mssqlctl 應用程式範本提取
在指定的 [URL] github 存放庫下載支援範本。
```bash
mssqlctl app template pull [--name -n] 
                           [--url -u]  
                           [--destination -d]
```
### <a name="examples"></a>範例
下載預設範本儲存機制位置下的所有範本。
```bash
mssqlctl app template pull
```
下載不同的存放庫位置下的所有範本。
```bash
mssqlctl app template list --url https://github.com/diffrent/templates.git
```
下載個別的範本名稱。
```bash
mssqlctl app template pull --name ssis            
```
### <a name="optional-parameters"></a>選擇性參數
#### `--name -n`
範本名稱。 如需完整清單，支援的範本 namesrun 關閉 `mssqlctl app template list`
#### `--url -u`
指定不同的範本存放庫位置。 預設值： https://github.com/Microsoft/SQLBDC-AppDeploy.git
#### `--destination -d`
應用程式基本架構的範本放在何處。
`./templates`
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