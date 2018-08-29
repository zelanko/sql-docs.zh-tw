---
title: ALTER EXTERNAL LIBRARY (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/05/2018
ms.prod: sql
ms.reviewer: ''
ms.suite: sql
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- ALTER EXTERNAL LIBRARY
- ALTER_EXTERNAL_LIBRARY_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- ALTER EXTERNAL LIBRARY
author: HeidiSteen
ms.author: heidist
manager: cgronlund
monikerRange: '>=sql-server-2017||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: fd521263853eee1d0c8c25eb135ff2d309eb4a75
ms.sourcegitcommit: 4183dc18999ad243c40c907ce736f0b7b7f98235
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/27/2018
ms.locfileid: "43100816"
---
# <a name="alter-external-library-transact-sql"></a>ALTER EXTERNAL LIBRARY (Transact-SQL)  

[!INCLUDE[tsql-appliesto-ss2017-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2017-xxxx-xxxx-xxx-md.md)]

修改現有外部套件程式庫的內容。

## <a name="syntax"></a>語法

```text
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

指定現有套件程式庫的名稱。 程式庫的範圍限制為使用者。 程式庫名稱在特定使用者或擁有者的內容中必須是唯一的。

程式庫名稱不能任意指派。 也就是說，您必須使用呼叫執行階段載入套件時所預期的名稱。

**owner_name**

指定擁有外部程式庫的使用者或角色名稱。

**file_spec**

指定適用於特定平台的套件內容。 只支援每個平台一個檔案成品。

檔案可以本機路徑或網路路徑形式來指定。 如果指定了資料來源選項，檔案名稱就可以是相對於 `EXTERNAL DATA SOURCE` 中所參考之容器的相對路徑。

(選擇性) 可以指定檔案的 OS 平台。 針對特定語言或執行階段，每個 OS 平台只允許一個檔案成品或內容。

**library_bits**

以十六進位常值的形式指定套件的內容，類似於組件。 

如果您具備改變程式庫的必要權限，但在伺服器上的檔案存取受到限制，且您無法將內容儲存至伺服器可存取的路徑，這個選項就非常有用。

您可以改為以二進位格式的變數來傳遞套件內容。

**PLATFORM = WINDOWS**

指定程式庫內容的平台。 修改現有程式庫以加入不同平台時，需要此值。 Windows 是唯一支援的平台。

## <a name="remarks"></a>Remarks

對於 R 語言，必須先針對 Windows，以具備 .ZIP 副檔名的 ZIP 壓縮封存檔案形式備妥套件。 目前僅支援 Windows 平台。  

`ALTER EXTERNAL LIBRARY` 陳述式只會將程式庫位元上傳至資料庫。 當使用者在 [sp_execute_external_script (Transact-SQL)](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md) 中執行呼叫程式庫的程式碼時，就會安裝已修改的程式庫。

## <a name="permissions"></a>[權限]

根據預設，**dbo** 使用者或 **db_owner** 角色的任何成員都有執行 ALTER EXTERNAL LIBRARY 的權限。 此外，建立外部程式庫的使用者可以改變該外部程式庫。

## <a name="examples"></a>範例

下列範例會變更名為 `customPackage` 的外部程式庫。

### <a name="a-replace-the-contents-of-a-library-using-a-file"></a>A. 使用檔案取代程式庫的內容

下列範例會使用包含更新位元的 ZIP 壓縮檔案，來修改名為 `customPackage` 的外部程式庫。

```sql
ALTER EXTERNAL LIBRARY customPackage 
SET 
  (CONTENT = 'C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\customPackage.zip')
WITH (LANGUAGE = 'R');
```

若要安裝更新的程式庫，請執行 `sp_execute_external_script` 預存程序。

```sql
EXEC sp_execute_external_script 
@language =N'R', 
@script=N'library(customPackage)'
;
```

### <a name="b-alter-an-existing-library-using-a-byte-stream"></a>B. 使用位元組資料流改變現有程式庫

下列範例會以十六進位常值傳遞新位元，藉以改變現有程式庫。

```SQL
ALTER EXTERNAL LIBRARY customLibrary 
SET (CONTENT = 0xabc123) WITH (LANGUAGE = 'R');
```

> [!NOTE]
> 此程式碼範例僅示範語法；`CONTENT =` 中的二進位值已被截斷以提高可讀性，且並不會建立可運作的程式庫。 二進位變數的實際內容會更長。

## <a name="see-also"></a>另請參閱

[CREATE EXTERNAL LIBRARY (Transact-SQL)](create-external-library-transact-sql.md)
[DROP EXTERNAL LIBRARY (Transact-SQL)](drop-external-library-transact-sql.md)  
[sys.external_library_files](../../relational-databases/system-catalog-views/sys-external-library-files-transact-sql.md)  
[sys.external_libraries](../../relational-databases/system-catalog-views/sys-external-libraries-transact-sql.md) 
