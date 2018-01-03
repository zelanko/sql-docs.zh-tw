---
title: "建立外部程式庫 (TRANSACT-SQL) |Microsoft 文件"
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
- CREATE EXTERNAL LIBRARY
- CREATE_EXTERNAL_LIBRARY_TSQL
- EXTERNAL LIBRARY
- EXTERNAL_LIBRARY_TSQL
dev_langs: TSQL
helpviewer_keywords: CREATE EXTERNAL LIBRARY
author: jeannt
ms.author: jeannt
manager: jhubbard
ms.openlocfilehash: bf4807943521308cb2907adab8cfc6e701325b8a
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/21/2017
---
# <a name="create-external-library-transact-sql"></a>建立外部程式庫 (TRANSACT-SQL)  

[!INCLUDE[tsql-appliesto-ss2017-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2017-xxxx-xxxx-xxx-md.md)]  

上載至資料庫的 R 封裝，從指定的位元組資料流或檔案路徑。

這個陳述式做為上傳所需的任何新外部語言執行階段 （R、 Python、 Java 等） 成品與所支援的作業系統平台的資料庫系統管理員的一般機制[!INCLUDE[ssnoversion](../../includes/ssnoversion.md)]。 目前支援 R 語言和 Windows 平台。

## <a name="syntax"></a>語法

```
CREATE EXTERNAL LIBRARY library_name  
    [ AUTHORIZATION owner_name ]  
FROM <file_spec> [,…2]  
WITH ( LANGUAGE = 'R' )  
[ ; ]  

<file_spec> ::=  
{  
(CONTENT = { <client_library_specifier> | <library_bits> }  
[, PLATFORM = WINDOWS ])  
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

程式庫會加入至資料庫使用者範圍中。 也就是文件庫名稱視為代表特定使用者或擁有者的內容內的唯一和程式庫名稱必須是唯一的每個使用者。 例如，兩位使用者**RUser1**和**RUser2**可以同時分開個別和上傳的 R 程式庫`ggplot2`。

**owner_name**

指定使用者或角色擁有外部的程式庫的名稱。 若未指定，擁有權便歸目前使用者。

資料庫擁有者所擁有的程式庫會被視為全域範圍中的資料庫和執行階段。 換句話說，資料庫擁有者可以建立含有一組常用的程式庫或套件，許多使用者共用的程式庫。 當外部程式庫由使用者建立以外`dbo`使用者，外部程式庫是私用，只有該使用者。

當使用者**RUser1**執行 R 指令碼時，值`libPath`可以包含多個路徑。 第一個路徑一律是資料庫擁有者所建立的共用程式庫的路徑。 第二個部分`libPath`指定包含個別的上傳封裝的路徑**RUser1**。

**file_spec**

指定在特定平台的套件內容。 支援每個平台只能有一個檔案成品。

中的本機路徑或網路路徑格式，可以指定的檔案。

（選擇性） 您可以指定檔案的作業系統平台。 每個作業系統平台特定的語言或執行階段允許只能有一個檔案成品或內容。

**library_bits**

指定套件的內容做為十六進位常值，類似於組件。 此選項可讓使用者建立文件庫來變更文件庫，如果有必要的權限，但不是需要任何伺服器可以存取的資料夾檔案路徑存取。

**平台 = WINDOWS**

指定的平台程式庫的內容。 預設值為 SQL Server 執行所在的主機平台。 因此，在使用者不需要指定的值。 萬一其中多個平台都有支援，或使用者必須指定不同的平台，此為必要。 視窗是唯一支援的平台。

## <a name="remarks"></a>備註

R 語言，使用檔案時，封裝必須先備妥的 zip 的封存檔案格式。適用於 Windows 的 ZIP 延伸模組。 目前支援 Windows 平台

`CREATE EXTERNAL LIBRARY`陳述式只會將上傳的文件庫的位元到資料庫。 程式庫不實際安裝到使用者執行外部指令碼之後，藉由執行[sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md)。  

文件庫上傳到的執行個體可以是公用或私用。 如果程式庫建立的成員所`dbo`，程式庫時為公用，且可以與所有使用者共用。 否則，程式庫是私用，只有該使用者。

您無法使用 blob 做為 SQL Server 2017 版本中的資料來源。

## <a name="permissions"></a>Permissions

需要`CREATE ANY EXTERNAL LIBRARY`權限。

若要修改的程式庫需要不同的權限， `ALTER ANY EXTERNAL LIBRARY`。

## <a name="examples"></a>範例

### <a name="a-add-an-external-library-to-a-database"></a>A. 將外部程式庫加入至資料庫  

下列範例會將外部程式庫呼叫 customPackage 至資料庫。

```sql
CREATE EXTERNAL LIBRARY customPackage 
FROM 
  (CONTENT = 'C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\customPackage.zip')
WITH (LANGUAGE = 'R');
```  

程式庫已成功上傳到的執行個體之後，使用者執行`sp_execute_external_script`程序中，安裝程式庫。

```sql
EXEC sp_execute_external_script 
@language =N'R', 
@script=N'
# load customPackage
library(customPackage)
'
```

### <a name="b-installing-packages-with-dependencies"></a>B. 安裝具有相依性的封裝

如果`packageB`具有相依性`packageA`，然後遵循這些一般原則：

+ 上傳目標封裝及其相依性。

    這兩個封裝必須是伺服器可存取的資料夾中。

    ```sql
    CREATE EXTERNAL LIBRARY packageA 
    FROM (CONTENT = 'C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\packageA.zip') 
    WITH (LANGUAGE = 'R'); 
    
    CREATE EXTERNAL LIBRARY packageB FROM (CONTENT = 'C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\packageB.zip') 
    WITH (LANGUAGE = 'R');
    ```

+ 第一次安裝相依項目。

    如果所需的套件`packageA`已上傳至執行個體，它必須尚未安裝分開。 必要的套件`packageA`時將會安裝`sp_execute_external_script`首次執行安裝套件`packageB`。

    不過，如果所需的套件， `packageA`，就無法使用，安裝目標套件`packageB`將會失敗。

    ```sql
    EXEC sp_execute_external_script 
    @language =N'R', 
    @script=N'
    # load packageB
    library(packageB)
    # call customPackageBFunc
    OutputDataSet <- customPackageBFunc()
    '
    with result sets (([result] int));    
    ```

### <a name="c-create-a-library-from-a-byte-stream"></a>C. 從位元組資料流建立文件庫

下列範例會建立文件庫傳遞更新為十六進位常值的位元。

```SQL
CREATE EXTERNAL LIBRARY customLibrary FROM (CONTENT = 0xabc123) WITH (LANGUAGE = 'R');
```

### <a name="d-change-an-existing-package-library"></a>D. 變更現有的封裝程式庫

`ALTER EXTERNAL LIBRARY` DDL 陳述式可用來加入新的文件庫內容或修改現有的文件庫內容。 若要修改現有的程式庫需要`ALTER ANY EXTERNAL LIBRARY`權限。

如需詳細資訊，請參閱[ALTER 外部程式庫](alter-external-library-transact-sql.md)。

### <a name="e-delete-a-package-library"></a>E. 刪除套件的文件庫

若要從資料庫刪除封裝程式庫，執行陳述式：

```sql
DROP EXTERNAL LIBRARY customPackage <user_name>;
```

> [!NOTE]
> 不同於其他`DROP`中的陳述式[!INCLUDE[ssnoversion](../../includes/ssnoversion.md)]，這個陳述式支援選擇性參數，指定的使用者授權單位。 此選項可讓使用者與角色擁有權來刪除一般使用者所上傳的文件庫。

## <a name="see-also"></a>另請參閱

[ALTER 外部程式庫 (TRANSACT-SQL)](alter-external-library-transact-sql.md)  
[卸除的外部程式庫 (TRANSACT-SQL)](drop-external-library-transact-sql.md)  
[sys.external_library_files](../../relational-databases/system-catalog-views/sys-external-library-files-transact-sql.md)  
[sys.external_libraries](../../relational-databases/system-catalog-views/sys-external-libraries-transact-sql.md)  
