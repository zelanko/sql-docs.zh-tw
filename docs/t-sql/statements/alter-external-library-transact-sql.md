---
title: "ALTER 外部程式庫 (TRANSACT-SQL) |Microsoft 文件"
ms.custom: 
ms.date: 08/18/2017
ms.prod: sql-server-2017
ms.reviewer: 
ms.suite: 
ms.technology:
- r-services
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- ALTER EXTERNAL LIBRARY
- ALTER_EXTERNAL_LIBRARY_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- ALTER EXTERNAL LIBRARY
author: jeannt
ms.author: jeannt
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 541419770828e01cca82fb33ead1b22170f8e4f3
ms.contentlocale: zh-tw
ms.lasthandoff: 09/01/2017

---
# <a name="alter-external-library-transact-sql"></a>ALTER 外部程式庫 (TRANSACT-SQL)  
[!INCLUDE[tsql-appliesto-ssvnxt-xxxx-xxxx-xxx](../../includes/tsql-appliesto-ssvnxt-xxxx-xxxx-xxx.md)]  

修改現有的文件庫內容。  

## <a name="syntax"></a>語法

```
ALTER EXTERNAL LIBRARY library_name
[ AUTHORIZATION owner_name ]
SET <file_spec>
WITH ( LANGUAGE = 'R' )
[ ; ]

<file_spec> ::=
{
(CONTENT = { <client_library_specifier> | <library_bits> | NONE}
[, PLATFORM = WINDOWS )
}

<client_library_specifier> :: =
  '[\\computer_name\]share_name\[path\]manifest_file_name'
| '[local_path\]manifest_file_name'
| '<relative_path_in_external_data_source>'

<library_bits> :: =
{ varbinary_literal | varbinary_expression }
```

### <a name="arguments"></a>引數

**library_name**

指定現有的封裝程式庫名稱。 程式庫的範圍給使用者。 也就是程式庫名稱會視為特定使用者或擁有者的內容中唯一的。

**owner_name**

指定使用者或角色擁有外部的程式庫的名稱。

**file_spec**

指定在特定平台的套件內容。 支援每個平台只能有一個檔案成品。

可以是本機路徑或網路路徑的形式指定的檔案。 如果指定的資料來源的選項，檔案名稱可以是相對路徑相對於參考中的容器`EXTERNAL DATA SOURCE`。

（選擇性） 您可以指定檔案的作業系統平台。 每個作業系統平台特定的語言或執行階段允許只能有一個檔案成品或內容。

**DATA_SOURCE = external_data_source_name**

指定包含程式庫檔案的位置的外部資料來源的名稱。 這個位置應該參考 Azure blob 儲存體路徑。 若要建立外部資料來源，使用[CREATE EXTERNAL DATA SOURCE (TRANSACT-SQL)](create-external-data-source-transact-sql.md)。

**平台 = WINDOWS**

指定的平台程式庫的內容。 修改現有的程式庫加入不同的平台時，則需要此值。 視窗是唯一支援的平台。

## <a name="remarks"></a>備註

R 語言中，封裝必須先備妥的 zip 的封存檔案格式。適用於 Windows 的 ZIP 延伸模組。 目前支援 Windows 平台。  
`ALTER EXTERNAL LIBRARY`陳述式只會將上傳的文件庫的位元到資料庫。 修改過的程式庫不實際安裝直到使用者執行外部指令碼之後，藉由執行[sp_execute_external_script (TRANSACT-SQL)](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md)。

## <a name="permissions"></a>Permissions
需要`ALTER ANY EXTERNAL LIBRARY`權限。 建立外部程式庫的使用者可以改變該外部的程式庫。

## <a name="examples"></a>範例

下列範例會修改呼叫 customPackage 外部程式庫。

```sql  
ALTER EXTERNAL LIBRARY customPackage 
SET 
  (CONTENT = 'C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\customPackage.zip')
WITH (LANGUAGE = 'R');
```  
然後執行`sp_execute_external_script`程序中，安裝程式庫。

```sql   
EXEC sp_execute_external_script 
@language =N'R', 
@script=N'
# load customPackage
library(customPackage)

# call customPackageFunc
OutputDataSet <- customPackageFunc()
'
with result sets (([result] int));    
```


## <a name="see-also"></a>另請參閱  
[建立外部程式庫 (TRANSACT-SQL)](create-external-library-transact-sql.md)
[卸除的外部程式庫 (TRANSACT-SQL)](drop-external-library-transact-sql.md)  
[sys.external_library_files](../../relational-databases/system-catalog-views/sys-external-library-files-transact-sql.md)  
[sys.external_libraries](../../relational-databases/system-catalog-views/sys-external-libraries-transact-sql.md)  

