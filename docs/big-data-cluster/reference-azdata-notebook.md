---
title: azdata notebook 參考
titleSuffix: SQL Server big data clusters
description: azdata notebook 命令的參考文章。
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 11/04/2019
ms.topic: reference
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 0a866dcca1debba47abf2e2e241d00151b8641ff
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/29/2020
ms.locfileid: "74820967"
---
# <a name="azdata-notebook"></a>azdata notebook

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]  

下文提供 `azdata` 工具中 `notebook` 命令的參考。 如需其他 `azdata` 命令的詳細資訊，請參閱 [azdata 參考](reference-azdata.md)

## <a name="commands"></a>命令
|     |     |
| --- | --- |
[azdata notebook view](#azdata-notebook-view) | 檢視筆記本。  在第一個儲存格執行錯誤時停止的選項。
[azdata notebook run](#azdata-notebook-run) | 執行筆記本。  執行會在第一個錯誤時停止。
## <a name="azdata-notebook-view"></a>azdata notebook view
此命令可以接受筆記本檔案，並將 Markdown、程式碼和輸出轉換成色彩終端格式。
```bash
azdata notebook view --path -p 
                     [--continue-on-error -c]
```
### <a name="examples"></a>範例
檢視筆記本。  這會顯示所有儲存格。
```bash
azdata notebook view --path '/home/me/notebooks/demo_notebook.ipynb'
```
檢視筆記本。  除非遇到輸出中包含錯誤的儲存格，否則顯示所有儲存格。  在這種情況下，輸出就會停止。
```bash
azdata notebook view --path '/home/me/notebooks/demo_notebook.ipynb' --stop-on-error
```
### <a name="required-parameters"></a>必要參數
#### `--path -p`
要檢視之筆記本的路徑。
### <a name="optional-parameters"></a>選擇性參數
#### `--continue-on-error -c`
繼續顯示其他儲存格，忽略在筆記本輸出中找到的任何儲存格錯誤。  預設行為是在發生錯誤時停止。  停止讓查看發生錯誤的第一個單元格變得更容易。
### <a name="global-arguments"></a>全域引數
#### `--debug`
增加記錄詳細資訊，以顯示所有偵錯記錄。
#### `--help -h`
顯示此說明訊息並結束。
#### `--output -o`
輸出格式。  允許的值：json、jsonc、table、tsv。  預設值：json。
#### `--query -q`
JMESPath 查詢字串。 如需詳細資訊和範例，請參閱 [http://jmespath.org/](http://jmespath.org/)。
#### `--verbose`
增加記錄詳細資訊。 使用 --debug 來取得完整偵錯記錄。
## <a name="azdata-notebook-run"></a>azdata notebook run
此命令會建立暫存目錄，並在其中執行指定的筆記本作為工作目錄。
```bash
azdata notebook run --path -p 
                    [--output-path]  
                    [--output-html]  
                    [--arguments -a]  
                    [--interactive -i]  
                    [--clear -c]  
                    [--timeout -t]
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
要用於筆記本輸出的目錄路徑。  包含輸出資料的筆記本和任何筆記本產生的檔案都會相對於此目錄產生。
#### `--output-html`
選擇性旗標指出是否要另外將輸出筆記本轉換成 HTML 格式。  建立第二個輸出檔。
#### `--arguments -a`
要插入 Notebook 執行的選擇性筆記本引數清單。  編碼為 JSON 字典。  範例：'{"name":"value", "name2":"value2"}'
#### `--interactive -i`
以互動模式執行筆記本。
#### `--clear -c`
在互動模式下，在呈現資料格之前清除主控台。
#### `--timeout -t`
等待執行完成的秒數。 值 -1 表示永遠等待。
`600`
### <a name="global-arguments"></a>全域引數
#### `--debug`
增加記錄詳細資訊，以顯示所有偵錯記錄。
#### `--help -h`
顯示此說明訊息並結束。
#### `--output -o`
輸出格式。  允許的值：json、jsonc、table、tsv。  預設值：json。
#### `--query -q`
JMESPath 查詢字串。 如需詳細資訊和範例，請參閱 [http://jmespath.org/](http://jmespath.org/)。
#### `--verbose`
增加記錄詳細資訊。 使用 --debug 來取得完整偵錯記錄。

## <a name="next-steps"></a>後續步驟

如需其他 `azdata` 命令的詳細資訊，請參閱 [azdata 參考](reference-azdata.md)。 如需如何安裝 `azdata` 工具的詳細資訊，請參閱[安裝 azdata 來管理 SQL Server 2019 巨量資料叢集](deploy-install-azdata.md)。
