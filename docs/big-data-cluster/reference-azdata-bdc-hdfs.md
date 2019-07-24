---
title: azdata bdc hdfs 參考
titleSuffix: SQL Server big data clusters
description: Azdata bdc hdfs 命令的參考文章。
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 07/24/2019
ms.topic: reference
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 8e892c2d501902ef915a297440ae5a6ffda83bce
ms.sourcegitcommit: 1f222ef903e6aa0bd1b14d3df031eb04ce775154
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/23/2019
ms.locfileid: "68426178"
---
# <a name="azdata-bdc-hdfs"></a>azdata bdc hdfs

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

下列文章提供**azdata**工具中**bdc hdfs**命令的參考。 如需其他**azdata**命令的詳細資訊, 請參閱[azdata 參考](reference-azdata.md)。

## <a name="commands"></a>命令
|     |     |
| --- | --- |
[azdata bdc hdfs shell](#azdata-bdc-hdfs-shell) | HDFS shell 是適用于 HDFS 檔案系統的簡單互動式命令 shell。
[azdata bdc hdfs ls](#azdata-bdc-hdfs-ls) | 列出指定檔案或目錄的狀態。
[azdata bdc hdfs 存在](#azdata-bdc-hdfs-exists) | 判斷檔案或目錄是否存在。  如果存在, 則傳回 True, 否則傳回 False。
[azdata bdc hdfs mkdir](#azdata-bdc-hdfs-mkdir) | 在指定的路徑建立目錄。
[azdata bdc hdfs mv](#azdata-bdc-hdfs-mv) | 將指定的檔案或路徑移動到指定的位置。
[azdata bdc hdfs 建立](#azdata-bdc-hdfs-create) | 在指定的位置建立文字檔。  簡單文字內容可以透過資料參數來新增。
[azdata bdc hdfs cat](#azdata-bdc-hdfs-cat) | 讀取檔案的內容。  Offset 和 length (以位元組為單位) 是選擇性參數。
[azdata bdc hdfs rm](#azdata-bdc-hdfs-rm) | 移除檔案或目錄。
[azdata bdc hdfs rmr](#azdata-bdc-hdfs-rmr) | 以遞迴方式移除檔案或目錄。
[azdata bdc hdfs chmod](#azdata-bdc-hdfs-chmod) | 變更指定檔案或目錄的許可權。
[azdata bdc hdfs chown](#azdata-bdc-hdfs-chown) | 變更指定檔案的擁有者或群組。
[azdata bdc hdfs 掛接](reference-azdata-bdc-hdfs-mount.md) | 管理 HDFS 中的遠端存放區裝載。
## <a name="azdata-bdc-hdfs-shell"></a>azdata bdc hdfs shell
HDFS shell 是適用于 HDFS 檔案系統的簡單互動式命令 shell。
```bash
azdata bdc hdfs shell 
```
### <a name="examples"></a>範例
啟動 shell。
```bash
azdata bdc hdfs shell
```
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
## <a name="azdata-bdc-hdfs-ls"></a>azdata bdc hdfs ls
列出指定檔案或目錄的狀態。
```bash
azdata bdc hdfs ls --path -p 
                   
```
### <a name="examples"></a>範例
清單狀態
```bash
azdata bdc hdfs ls --path '/tmp'
```
### <a name="required-parameters"></a>必要參數
#### `--path -p`
列出狀態的路徑。
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
## <a name="azdata-bdc-hdfs-exists"></a>azdata bdc hdfs 存在
判斷檔案或目錄是否存在。  如果存在, 則傳回 True, 否則傳回 False。
```bash
azdata bdc hdfs exists --path -p 
                       
```
### <a name="examples"></a>範例
檢查檔案或目錄並存。
```bash
azdata bdc hdfs exists --path '/tmp'
```
### <a name="required-parameters"></a>必要參數
#### `--path -p`
要檢查是否存在的路徑。
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
## <a name="azdata-bdc-hdfs-mkdir"></a>azdata bdc hdfs mkdir
在指定的路徑建立目錄。
```bash
azdata bdc hdfs mkdir --path -p 
                      
```
### <a name="examples"></a>範例
建立目錄。
```bash
azdata bdc hdfs mkdir --path '/tmp'
```
### <a name="required-parameters"></a>必要參數
#### `--path -p`
要建立的目錄名稱。
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
## <a name="azdata-bdc-hdfs-mv"></a>azdata bdc hdfs mv
將指定的檔案或路徑移動到指定的位置。
```bash
azdata bdc hdfs mv --source-path -s 
                   --target-path -t
```
### <a name="examples"></a>範例
移動檔案或目錄。
```bash
azdata bdc hdfs mv --source-path '/tmp' --target-path '/dest'
```
### <a name="required-parameters"></a>必要參數
#### `--source-path -s`
要移動的目錄。
#### `--target-path -t`
要移至的位置。
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
## <a name="azdata-bdc-hdfs-create"></a>azdata bdc hdfs 建立
在指定的位置建立文字檔。  簡單文字內容可以透過資料參數來新增。
```bash
azdata bdc hdfs create --path -p 
                       --data -d
```
### <a name="examples"></a>範例
建立檔案。
```bash
azdata bdc hdfs create --path '/tmp/test.txt' --data "This is a test."
```
### <a name="required-parameters"></a>必要參數
#### `--path -p`
要建立的檔案名。
#### `--data -d`
檔案的內容。  適用于簡單文字內容。
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
## <a name="azdata-bdc-hdfs-cat"></a>azdata bdc hdfs cat
讀取檔案的內容。  Offset 和 length (以位元組為單位) 是選擇性參數。
```bash
azdata bdc hdfs cat --path -p 
                    --offset  
                    --length -l
```
### <a name="examples"></a>範例
讀取檔案。
```bash
azdata bdc hdfs cat --path '/tmp/test.txt'
```
### <a name="required-parameters"></a>必要參數
#### `--path -p`
要讀取之檔案的名稱。
#### `--offset`
要讀取的檔案內的位元組位移數。
#### `--length -l`
要讀取的資料長度。
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
## <a name="azdata-bdc-hdfs-rm"></a>azdata bdc hdfs rm
移除檔案或目錄。
```bash
azdata bdc hdfs rm --path -p 
                   
```
### <a name="examples"></a>範例
移除檔案或目錄。
```bash
azdata bdc hdfs rm --path '/tmp'
```
### <a name="required-parameters"></a>必要參數
#### `--path -p`
要移除的檔案名。
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
## <a name="azdata-bdc-hdfs-rmr"></a>azdata bdc hdfs rmr
以遞迴方式移除檔案或目錄。
```bash
azdata bdc hdfs rmr --path -p 
                    
```
### <a name="examples"></a>範例
遞迴移除目錄。
```bash
azdata bdc hdfs rmr --path '/tmp'
```
### <a name="required-parameters"></a>必要參數
#### `--path -p`
要以遞迴方式移除的檔案名。
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
## <a name="azdata-bdc-hdfs-chmod"></a>azdata bdc hdfs chmod
變更指定檔案或目錄的許可權。
```bash
azdata bdc hdfs chmod --path -p 
                      --permission
```
### <a name="examples"></a>範例
變更檔案或目錄許可權。
```bash
azdata bdc hdfs chmod --permission 775 --path '/tmp/test.txt'
```
### <a name="required-parameters"></a>必要參數
#### `--path -p`
要設定許可權的檔案或目錄的名稱。
#### `--permission`
要設定的許可權八位。  範例 "775"。
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
## <a name="azdata-bdc-hdfs-chown"></a>azdata bdc hdfs chown
變更指定檔案的擁有者或群組。
```bash
azdata bdc hdfs chown --path -p 
                      --owner  
                      --group -g
```
### <a name="examples"></a>範例
變更擁有者和群組。
```bash
azdata bdc hdfs chown --owner hdfs --group superusergroup --path '/tmp/test.txt'
```
### <a name="required-parameters"></a>必要參數
#### `--path -p`
要變更擁有者之檔案或目錄的名稱。
#### `--owner`
要設定為的擁有者名稱。
#### `--group -g`
要設定為的組名。
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
