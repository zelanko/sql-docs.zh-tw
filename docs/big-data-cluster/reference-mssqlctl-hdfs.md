---
title: mssqlctl hdfs 參考
titleSuffix: SQL Server big data clusters
description: Mssqlctl hdfs 命令的參考文件。
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
manager: jroth
ms.date: 06/26/2019
ms.topic: reference
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 8f211faf827bdf925a8fde938fff8f96998bc359
ms.sourcegitcommit: e0c55d919ff9cec233a7a14e72ba16799f4505b2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/10/2019
ms.locfileid: "67728524"
---
# <a name="mssqlctl-hdfs"></a>mssqlctl hdfs

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

下列文章提供的參考**hdfs**中的命令**mssqlctl**工具。 如需其他詳細資訊**mssqlctl**命令，請參閱[mssqlctl 參考](reference-mssqlctl.md)。

## <a name="commands"></a>命令
|     |     |
| --- | --- |
[mssqlctl hdfs shell](#mssqlctl-hdfs-shell) | HDFS 殼層是簡單的互動式命令殼層的 HDFS 檔案系統。
[mssqlctl hdfs ls](#mssqlctl-hdfs-ls) | 列出指定的檔案或目錄的狀態。
[mssqlctl hdfs exists](#mssqlctl-hdfs-exists) | 判斷檔案或目錄是否存在。  傳回存在則為 True 和 False 否則。
[mssqlctl hdfs mkdir](#mssqlctl-hdfs-mkdir) | 建立位於指定路徑的目錄。
[mssqlctl hdfs mv](#mssqlctl-hdfs-mv) | 將指定的檔案或路徑移到指定的位置。
[mssqlctl hdfs create](#mssqlctl-hdfs-create) | 建立文字檔案，在指定的位置。  可以透過資料參數中加入簡單的文字內容。
[mssqlctl hdfs read](#mssqlctl-hdfs-read) | 讀取的檔案的內容。  位移和長度，以位元組為單位是選擇性的參數。
[mssqlctl hdfs rm](#mssqlctl-hdfs-rm) | 移除檔案或目錄。
[mssqlctl hdfs rmr](#mssqlctl-hdfs-rmr) | 以遞迴方式移除檔案或目錄。
[mssqlctl hdfs chmod](#mssqlctl-hdfs-chmod) | 變更指定的檔案或目錄的權限。
[mssqlctl hdfs chown](#mssqlctl-hdfs-chown) | 變更擁有者或群組指定的檔案。
## <a name="mssqlctl-hdfs-shell"></a>mssqlctl hdfs 殼層
HDFS 殼層是簡單的互動式命令殼層的 HDFS 檔案系統。
```bash
mssqlctl hdfs shell 
```
### <a name="examples"></a>範例
啟動 shell。
```bash
mssqlctl hdfs shell
```
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
## <a name="mssqlctl-hdfs-ls"></a>mssqlctl hdfs ls
列出指定的檔案或目錄的狀態。
```bash
mssqlctl hdfs ls --path -p 
                 
```
### <a name="examples"></a>範例
清單狀態
```bash
mssqlctl hdfs ls --path '/tmp'
```
### <a name="required-parameters"></a>必要參數
#### `--path -p`
要列示狀態的路徑。
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
## <a name="mssqlctl-hdfs-exists"></a>mssqlctl hdfs 存在
判斷檔案或目錄是否存在。  傳回存在則為 True 和 False 否則。
```bash
mssqlctl hdfs exists --path -p 
                     
```
### <a name="examples"></a>範例
檢查有檔案或目錄的檔案存在。
```bash
mssqlctl hdfs exists --path '/tmp'
```
### <a name="required-parameters"></a>必要參數
#### `--path -p`
要檢查檔案存在的路徑。
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
## <a name="mssqlctl-hdfs-mkdir"></a>mssqlctl hdfs mkdir
建立位於指定路徑的目錄。
```bash
mssqlctl hdfs mkdir --path -p 
                    
```
### <a name="examples"></a>範例
建立目錄。
```bash
mssqlctl hdfs mkdir --path '/tmp'
```
### <a name="required-parameters"></a>必要參數
#### `--path -p`
若要建立的目錄名稱。
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
## <a name="mssqlctl-hdfs-mv"></a>mssqlctl hdfs mv
將指定的檔案或路徑移到指定的位置。
```bash
mssqlctl hdfs mv --source-path -s 
                 --target-path -t
```
### <a name="examples"></a>範例
移動檔案或目錄。
```bash
mssqlctl hdfs mv --source-path '/tmp' --target-path '/dest'
```
### <a name="required-parameters"></a>必要參數
#### `--source-path -s`
要移動的目錄。
#### `--target-path -t`
要前往的位置。
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
## <a name="mssqlctl-hdfs-create"></a>建立 mssqlctl hdfs
建立文字檔案，在指定的位置。  可以透過資料參數中加入簡單的文字內容。
```bash
mssqlctl hdfs create --path -p 
                     --data -d
```
### <a name="examples"></a>範例
建立檔案。
```bash
mssqlctl hdfs create --path '/tmp/test.txt' --data "This is a test."
```
### <a name="required-parameters"></a>必要參數
#### `--path -p`
若要建立檔案的名稱。
#### `--data -d`
檔案的內容。  適用於簡單的文字內容。
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
## <a name="mssqlctl-hdfs-read"></a>讀取 mssqlctl hdfs
讀取的檔案的內容。  位移和長度，以位元組為單位是選擇性的參數。
```bash
mssqlctl hdfs read --path -p 
                   --offset  
                   --length -l
```
### <a name="examples"></a>範例
讀取檔案。
```bash
mssqlctl hdfs read --path '/tmp/test.txt'
```
### <a name="required-parameters"></a>必要參數
#### `--path -p`
要讀取之檔案的名稱。
#### `--offset`
要讀取的檔案內的位移的位元組數目。
#### `--length -l`
要讀取之資料的長度。
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
## <a name="mssqlctl-hdfs-rm"></a>mssqlctl hdfs rm
移除檔案或目錄。
```bash
mssqlctl hdfs rm --path -p 
                 
```
### <a name="examples"></a>範例
移除檔案或目錄。
```bash
mssqlctl hdfs rm --path '/tmp'
```
### <a name="required-parameters"></a>必要參數
#### `--path -p`
要移除之檔案的名稱。
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
## <a name="mssqlctl-hdfs-rmr"></a>mssqlctl hdfs rmr
以遞迴方式移除檔案或目錄。
```bash
mssqlctl hdfs rmr --path -p 
                  
```
### <a name="examples"></a>範例
遞迴移除目錄。
```bash
mssqlctl hdfs rmr --path '/tmp'
```
### <a name="required-parameters"></a>必要參數
#### `--path -p`
要移除以遞迴方式檔案的名稱。
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
## <a name="mssqlctl-hdfs-chmod"></a>mssqlctl hdfs chmod
變更指定的檔案或目錄的權限。
```bash
mssqlctl hdfs chmod --path -p 
                    --permission
```
### <a name="examples"></a>範例
變更檔案或目錄的權限。
```bash
mssqlctl hdfs chmod --permission 775 --path '/tmp/test.txt'
```
### <a name="required-parameters"></a>必要參數
#### `--path -p`
檔案或目錄上設定權限的名稱。
#### `--permission`
用來設定的權限八位元。  範例 「 775"。
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
## <a name="mssqlctl-hdfs-chown"></a>mssqlctl hdfs chown
變更擁有者或群組指定的檔案。
```bash
mssqlctl hdfs chown --path -p 
                    --owner  
                    --group -g
```
### <a name="examples"></a>範例
變更擁有者和群組。
```bash
mssqlctl hdfs chown --owner hdfs --group superusergroup --path '/tmp/test.txt'
```
### <a name="required-parameters"></a>必要參數
#### `--path -p`
檔案或目錄變更的擁有者的名稱。
#### `--owner`
若要設定為擁有者名稱。
#### `--group -g`
若要設定的群組名稱。
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

如需有關如何安裝**mssqlctl**工具，請參閱[安裝來管理 SQL Server 2019 巨量資料叢集 mssqlctl](deploy-install-mssqlctl.md)。