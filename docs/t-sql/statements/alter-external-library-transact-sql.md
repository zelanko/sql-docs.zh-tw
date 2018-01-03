---
title: "ALTER 外部程式庫 (TRANSACT-SQL) |Microsoft 文件"
ms.custom: 
ms.date: 10/05/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: t-sql|statements
ms.reviewer: 
ms.suite: sql
ms.technology: r-services
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- ALTER EXTERNAL LIBRARY
- ALTER_EXTERNAL_LIBRARY_TSQL
dev_langs: TSQL
helpviewer_keywords: ALTER EXTERNAL LIBRARY
author: jeannt
ms.author: jeannt
manager: jhubbard
ms.openlocfilehash: 28a62f00b479506e919faf2cbdbf1202045192eb
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/21/2017
---
# <a name="alter-external-library-transact-sql"></a>ALTER 外部程式庫 (TRANSACT-SQL)  

[!INCLUDE[tsql-appliesto-ss2017-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2017-xxxx-xxxx-xxx-md.md)]

修改現有的外部封裝程式庫的內容。

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

> [!IMPORTANT] 
> 目前，blob 不支援做為 SQL Server 2017 版本中的資料來源。

**library_bits**

指定套件的內容做為十六進位常值，類似於組件。 此選項可讓使用者建立文件庫來變更文件庫，如果有必要的權限，但不是需要任何伺服器可以存取的資料夾檔案路徑存取。

**平台 = WINDOWS**

指定的平台程式庫的內容。 修改現有的程式庫加入不同的平台時，則需要此值。 視窗是唯一支援的平台。

## <a name="remarks"></a>備註

R 語言中，封裝必須先備妥的 zip 的封存檔案格式。適用於 Windows 的 ZIP 延伸模組。 目前支援 Windows 平台。  

`ALTER EXTERNAL LIBRARY`陳述式只會將上傳的文件庫的位元到資料庫。 修改過的程式庫不實際安裝直到使用者執行外部指令碼之後，藉由執行[sp_execute_external_script (TRANSACT-SQL)](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md)。

## <a name="permissions"></a>Permissions

需要`ALTER ANY EXTERNAL LIBRARY`權限。 建立外部程式庫的使用者可以改變該外部的程式庫。

## <a name="examples"></a>範例

下列範例會修改呼叫 customPackage 外部程式庫。

### <a name="a-replace-the-contents-of-a-library-using-a-file"></a>A. 取代文件庫使用檔案的內容

下列範例會修改外部程式庫呼叫 customPackage，使用包含更新的位元的 zip 的檔案。

```sql
ALTER EXTERNAL LIBRARY customPackage 
SET 
  (CONTENT = 'C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\customPackage.zip')
WITH (LANGUAGE = 'R');
```  

若要安裝更新的程式庫，執行預存程序`sp_execute_external_script`。

```sql   
EXEC sp_execute_external_script 
@language =N'R', 
@script=N'
# load customPackage
library(customPackage)
# call customPackageFunc
OutputDataSet <- customPackageFunc()
'
WITH RESULT SETS (([result] int));
```

### <a name="b-alter-an-existing-library-using-a-byte-stream"></a>B. 改變現有的程式庫使用位元組資料流

下例會變更現有的程式庫傳遞做為十六進位的新位元常值。

```SQL
ALTER EXTERNAL LIBRARY customLibrary FROM (CONTENT = 0xabc123) WITH (LANGUAGE = 'R');
```

## <a name="see-also"></a>另請參閱  

[建立外部程式庫 (TRANSACT-SQL)](create-external-library-transact-sql.md)
[卸除的外部程式庫 (TRANSACT-SQL)](drop-external-library-transact-sql.md)  
[sys.external_library_files](../../relational-databases/system-catalog-views/sys-external-library-files-transact-sql.md)  
[sys.external_libraries](../../relational-databases/system-catalog-views/sys-external-libraries-transact-sql.md)  
