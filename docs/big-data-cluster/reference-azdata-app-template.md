---
title: azdata 應用程式範本參考
titleSuffix: SQL Server big data clusters
description: Azdata 應用程式範本命令的參考文章。
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 07/24/2019
ms.topic: reference
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 3b257a2bacc56a7907ab0d25f492ed0ebd605543
ms.sourcegitcommit: 1f222ef903e6aa0bd1b14d3df031eb04ce775154
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/23/2019
ms.locfileid: "68426328"
---
# <a name="azdata-app-template"></a>azdata 應用程式範本

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

下列文章提供**azdata**工具中**應用程式範本**命令的參考。 如需其他**azdata**命令的詳細資訊, 請參閱[azdata 參考](reference-azdata.md)。

## <a name="commands"></a>命令
|     |     |
| --- | --- |
[azdata 應用程式範本清單](#azdata-app-template-list) | 提取支援的範本。
[azdata 應用程式範本提取](#azdata-app-template-pull) | 下載支援的範本。
## <a name="azdata-app-template-list"></a>azdata 應用程式範本清單
在指定的 [URL] github 存放庫下提取支援的範本。
```bash
azdata app template list [--url -u] 
                         
```
### <a name="examples"></a>範例
提取預設範本存放庫位置底下的所有範本。
```bash
azdata app template list
```
提取不同存放庫位置下的所有範本。
```bash
azdata app template list --url https://github.com/diffrent/templates.git
```
### <a name="optional-parameters"></a>選擇性參數
#### `--url -u`
指定不同的範本存放庫位置。 預設 https://github.com/Microsoft/SQLBDC-AppDeploy.git
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
## <a name="azdata-app-template-pull"></a>azdata 應用程式範本提取
在指定的 [URL] github 存放庫底下下載支援的範本。
```bash
azdata app template pull [--name -n] 
                         [--url -u]  
                         [--destination -d]
```
### <a name="examples"></a>範例
下載預設範本存放庫位置底下的所有範本。
```bash
azdata app template pull
```
下載位於不同存放庫位置下的所有範本。
```bash
azdata app template list --url https://github.com/diffrent/templates.git
```
依名稱下載個別範本。
```bash
azdata app template pull --name ssis            
```
### <a name="optional-parameters"></a>選擇性參數
#### `--name -n`
範本名稱。 如需完整清單, 請從支援的範本 namesrun`azdata app template list`
#### `--url -u`
指定不同的範本存放庫位置。 預設 https://github.com/Microsoft/SQLBDC-AppDeploy.git
#### `--destination -d`
應用程式基本架構範本的放置位置。
`./templates`
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
