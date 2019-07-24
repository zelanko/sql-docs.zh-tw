---
title: azdata 筆記本參考
titleSuffix: SQL Server big data clusters
description: Azdata 筆記本命令的參考文章。
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 07/24/2019
ms.topic: reference
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: b96c5e06ec51f53964a28cac86f385d6b42c1dc4
ms.sourcegitcommit: 1f222ef903e6aa0bd1b14d3df031eb04ce775154
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/23/2019
ms.locfileid: "68426008"
---
# <a name="azdata-notebook"></a>azdata 筆記本

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

下列文章提供**azdata**工具中**筆記本**命令的參考。 如需其他**azdata**命令的詳細資訊, 請參閱[azdata 參考](reference-azdata.md)

## <a name="commands"></a>命令
|     |     |
| --- | --- |
[azdata 筆記本視圖](#azdata-notebook-view) | 觀看筆記本。  在第一個資料格執行錯誤時停止的選項。
[azdata 筆記本執行](#azdata-notebook-run) | 執行筆記本。  執行會在第一個錯誤時停止。
## <a name="azdata-notebook-view"></a>azdata 筆記本視圖
此命令可以接受筆記本檔案, 並將 markdown、程式碼和輸出轉換成色彩端子格式。
```bash
azdata notebook view --path -p 
                     [--continue-on-error -c]
```
### <a name="examples"></a>範例
觀看筆記本。  這會顯示所有儲存格。
```bash
azdata notebook view --path '/home/me/notebooks/demo_notebook.ipynb'
```
觀看筆記本。  這會顯示所有儲存格, 除非遇到其輸出中含有錯誤的資料格。  在這種情況下, 輸出就會停止。
```bash
azdata notebook view --path '/home/me/notebooks/demo_notebook.ipynb' --stop-on-error
```
### <a name="required-parameters"></a>必要參數
#### `--path -p`
要查看的筆記本路徑。
### <a name="optional-parameters"></a>選擇性參數
#### `--continue-on-error -c`
繼續顯示其他資料格, 忽略在筆記本輸出中找到的任何資料格錯誤。  預設行為是在發生錯誤時停止。  停止時, 會看到第一個發生錯誤的資料格變得更容易。
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
## <a name="azdata-notebook-run"></a>azdata 筆記本執行
此命令會建立臨時目錄, 並在其中執行指定的筆記本做為工作目錄。
```bash
azdata notebook run --path -p 
                    [--output-path]  
                    [--output-html]
```
### <a name="examples"></a>範例
執行筆記本。
```bash
azdata notebook run --path '/home/me/notebooks/demo_notebook.ipynb'
```
### <a name="required-parameters"></a>必要參數
#### `--path -p`
要執行之筆記本的檔案路徑。
### <a name="optional-parameters"></a>選擇性參數
#### `--output-path`
要用於筆記本輸出的目錄路徑。  具有輸出資料的筆記本和產生的任何筆記本檔案都會產生相對於此目錄的。
#### `--output-html`
選擇性旗標 indicatingg 是否要另外將輸出筆記本轉換成 HTML 格式。  建立第二個輸出檔。
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

如需有關如何安裝**azdata**工具的詳細資訊, 請參閱[install azdata to manage SQL Server 2019 big data](deploy-install-azdata.md)叢集。
