---
title: azdata bdc hdfs 參考
titleSuffix: SQL Server big data clusters
description: azdata bdc hdfs 命令的參考文章。
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 11/04/2019
ms.topic: reference
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: e20e7574109ccce4caa6b4d9fd84a4fef65cf0fa
ms.sourcegitcommit: 830149bdd6419b2299aec3f60d59e80ce4f3eb80
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/04/2019
ms.locfileid: "73531782"
---
# <a name="azdata-bdc-hdfs"></a>azdata bdc hdfs

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]  

下列文章提供 `azdata` 工具中 `sql` 命令的參考。 如需其他 `azdata` 命令的詳細資訊，請參閱 [azdata 參考](reference-azdata.md)

## <a name="commands"></a>命令
|     |     |
| --- | --- |
[azdata bdc hdfs status](reference-azdata-bdc-hdfs-status.md) | Hdfs 服務狀態命令。
[azdata bdc hdfs shell](#azdata-bdc-hdfs-shell) | HDFS 殼層是適用於 HDFS 檔案系統的簡單互動式命令殼層。
[azdata bdc hdfs ls](#azdata-bdc-hdfs-ls) | 列出指定檔案或目錄的狀態。
[azdata bdc hdfs exists](#azdata-bdc-hdfs-exists) | 判斷檔案或目錄是否存在。  如果存在則傳回 True，否則傳回 False。
[azdata bdc hdfs mkdir](#azdata-bdc-hdfs-mkdir) | 在指定的路徑上建立目錄。
[azdata bdc hdfs mv](#azdata-bdc-hdfs-mv) | 將指定的檔案或路徑移至指定位置。
[azdata bdc hdfs create](#azdata-bdc-hdfs-create) | 在指定的位置建立文字檔。  可以透過資料參數加入簡單文字內容。
[azdata bdc hdfs cat](#azdata-bdc-hdfs-cat) | 讀取檔案的內容。  以位元組為單位的位移和長度是選擇性參數。
[azdata bdc hdfs rm](#azdata-bdc-hdfs-rm) | 移除檔案或目錄。
[azdata bdc hdfs rmr](#azdata-bdc-hdfs-rmr) | 以遞迴方式移除檔案或目錄。
[azdata bdc hdfs chmod](#azdata-bdc-hdfs-chmod) | 變更指定檔案或目錄上的權限。
[azdata bdc hdfs chown](#azdata-bdc-hdfs-chown) | 變更指定檔案的擁有者或群組。
[azdata bdc hdfs cp](#azdata-bdc-hdfs-cp) | 在本機電腦與 HDFS 之間複製檔案或目錄。
[azdata bdc hdfs mount](reference-azdata-bdc-hdfs-mount.md) | 管理 HDFS 中遠端存放庫的裝載。
## <a name="azdata-bdc-hdfs-shell"></a>azdata bdc hdfs shell
HDFS 殼層是適用於 HDFS 檔案系統的簡單互動式命令殼層。
```bash
azdata bdc hdfs shell 
```
### <a name="examples"></a>範例
啟動殼層。
```bash
azdata bdc hdfs shell
```
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
## <a name="azdata-bdc-hdfs-ls"></a>azdata bdc hdfs ls
列出指定檔案或目錄的狀態。
```bash
azdata bdc hdfs ls --path -p 
 ```
### <a name="examples"></a>範例
列出狀態
```bash
azdata bdc hdfs ls --path '/tmp'
```
### <a name="required-parameters"></a>必要參數
#### `--path -p`
列出狀態的路徑。
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
## <a name="azdata-bdc-hdfs-exists"></a>azdata bdc hdfs exists
判斷檔案或目錄是否存在。  如果存在則傳回 True，否則傳回 False。
```bash
azdata bdc hdfs exists --path -p 
     ```
### Examples
Check for file or directory existance.
```bash
azdata bdc hdfs exists --path '/tmp'
```
### <a name="required-parameters"></a>必要參數
#### `--path -p`
檢查是否存在的路徑。
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
## <a name="azdata-bdc-hdfs-mkdir"></a>azdata bdc hdfs mkdir
在指定的路徑上建立目錄。
```bash
azdata bdc hdfs mkdir --path -p 
    ```
### Examples
Make directory.
```bash
azdata bdc hdfs mkdir --path '/tmp'
```
### <a name="required-parameters"></a>必要參數
#### `--path -p`
要建立之目錄的名稱。
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
## <a name="azdata-bdc-hdfs-mv"></a>azdata bdc hdfs mv
將指定的檔案或路徑移至指定位置。
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
增加記錄詳細資訊，以顯示所有偵錯記錄。
#### `--help -h`
顯示此說明訊息並結束。
#### `--output -o`
輸出格式。  允許的值：json、jsonc、table、tsv。  預設值：json。
#### `--query -q`
JMESPath 查詢字串。 如需詳細資訊和範例，請參閱 [http://jmespath.org/](http://jmespath.org/)。
#### `--verbose`
增加記錄詳細資訊。 使用 --debug 來取得完整偵錯記錄。
## <a name="azdata-bdc-hdfs-create"></a>azdata bdc hdfs create
在指定的位置建立文字檔。  可以透過資料參數加入簡單文字內容。
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
要建立之檔案的名稱。
#### `--data -d`
檔案的內容。  適用於簡單文字內容。
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
## <a name="azdata-bdc-hdfs-cat"></a>azdata bdc hdfs cat
讀取檔案的內容。  以位元組為單位的位移和長度是選擇性參數。
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
要讀取之檔案內的位元組位移數目。
#### `--length -l`
要讀取之資料的長度。
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
要移除之檔案的名稱。
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
## <a name="azdata-bdc-hdfs-rmr"></a>azdata bdc hdfs rmr
以遞迴方式移除檔案或目錄。
```bash
azdata bdc hdfs rmr --path -p 
  ```
### <a name="examples"></a>範例
以遞迴方式移除目錄。
```bash
azdata bdc hdfs rmr --path '/tmp'
```
### <a name="required-parameters"></a>必要參數
#### `--path -p`
要以遞迴方式移除之檔案的名稱。
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
## <a name="azdata-bdc-hdfs-chmod"></a>azdata bdc hdfs chmod
變更指定檔案或目錄上的權限。
```bash
azdata bdc hdfs chmod --path -p 
                      --permission
```
### <a name="examples"></a>範例
變更檔案或目錄權限。
```bash
azdata bdc hdfs chmod --permission 775 --path '/tmp/test.txt'
```
### <a name="required-parameters"></a>必要參數
#### `--path -p`
要設定權限之檔案或目錄的名稱。
#### `--permission`
要設定的權限八位元。  例如 "775"。
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
要設定的擁有者名稱。
#### `--group -g`
要設定的群組名稱。
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
## <a name="azdata-bdc-hdfs-cp"></a>azdata bdc hdfs cp
在本機電腦與 HDFS 之間複製檔案或目錄。  若是輸入目錄，將會複製整個樹狀目錄。  若該目標檔案或目錄已經存在，此命令將會失敗。  若要指定遠端 HDFS 目錄，請在路徑前加上 "hdfs:"
```bash
azdata bdc hdfs cp --from-path -f 
                   --to-path -t
```
### <a name="examples"></a>範例
在本機電腦與 HDFS 之間複製檔案或目錄。
```bash
azdata bdc hdfs cp --from_path '/tmp/test.txt --to-path 'hdfs:/user/me/test.txt'
```
### <a name="required-parameters"></a>必要參數
#### `--from-path -f`
要複製之來源路徑的名稱。  在路徑前加上 "hdfs:"，以表示是 HDFS 路徑。
#### `--to-path -t`
要複製到之目標路徑的名稱。  在路徑前加上 "hdfs:"，以表示是 HDFS 路徑。
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

如需其他 `azdata` 命令的詳細資訊，請參閱 [azdata 參考](reference-azdata.md)。 如需如何安裝 `azdata` 工具的詳細資訊，請參閱[安裝 azdata 管理 SQL Server 2019 巨量資料叢集](deploy-install-azdata.md)。
