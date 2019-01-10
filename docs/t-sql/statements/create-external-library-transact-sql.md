---
title: CREATE EXTERNAL LIBRARY (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 12/07/2018
ms.prod: sql
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- CREATE EXTERNAL LIBRARY
- CREATE_EXTERNAL_LIBRARY_TSQL
- EXTERNAL LIBRARY
- EXTERNAL_LIBRARY_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- CREATE EXTERNAL LIBRARY
author: HeidiSteen
ms.author: heidist
manager: cgronlund
monikerRange: '>=sql-server-2017||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: bd47fd06404dad6e6896d377e95de677a08c5ae3
ms.sourcegitcommit: 6443f9a281904af93f0f5b78760b1c68901b7b8d
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/11/2018
ms.locfileid: "53205157"
---
# <a name="create-external-library-transact-sql"></a>CREATE EXTERNAL LIBRARY (Transact-SQL)  

[!INCLUDE[tsql-appliesto-ss2017-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2017-xxxx-xxxx-xxx-md.md)]  

將 R 套件檔案從指定的位元組資料流或檔案路徑上傳到資料庫。 此陳述式可作為一般機制，供資料庫管理員上傳 [!INCLUDE[ssnoversion](../../includes/ssnoversion-md.md)] 所支援之任何新外部語言執行階段 (目前只有 R) 和 OS 平台所需的成品。 

在 SQL Server 2017 和更新版本中，支援 R 語言和 Windows 平台。 預計在稍後的版本中將會支援 Python 和 Linux。

## <a name="syntax"></a>語法

```text
CREATE EXTERNAL LIBRARY library_name  
    [ AUTHORIZATION owner_name ]  
FROM <file_spec> [,...2]  
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

程式庫會新增至使用者的資料庫範圍。 程式庫名稱在特定使用者或擁有者的內容中必須是唯一的。 例如，兩個使用者 **RUser1** 和 **RUser2** 都可以各自且分別上傳 R 程式庫 `ggplot2`。 不過，如果 **RUser1** 想要上傳 `ggplot2` 的新版本，則第二個執行個體必須有不同名稱，否則會取代現有的程式庫。 

不可任意指派程式庫名稱；程式庫名稱應該與從 R 載入 程式庫時所需的名稱相同。

**owner_name**

指定擁有外部程式庫的使用者或角色名稱。 若未指定，擁有權便歸目前使用者。

資料庫擁有者所擁有的程式庫會被視為資料庫和執行階段的全域程式庫。 換句話說，資料庫擁有者所建立的程式庫可以包含許多使用者所共用的一組通用程式庫或套件。 當外部程式庫是由 `dbo` 使用者以外的使用者所建立時，該外部程式庫僅是該使用者的私用程式庫。

當使用者 **RUser1** 執行 R 指令碼時，`libPath` 的值可能包含多個路徑。 第一個路徑一律是資料庫擁有者所建立之共用程式庫的路徑。 `libPath` 的第二個部分會指定包含 **RUser1** 個別上傳之套件的路徑。

**file_spec**

指定適用於特定平台的套件內容。 只支援每個平台一個檔案成品。

指定檔案時，可以採用本機路徑或網路路徑的形式來指定。

(選擇性) 可以指定檔案的 OS 平台。 針對特定語言或執行階段，每個 OS 平台只允許一個檔案成品或內容。

**library_bits**

以十六進位常值的形式指定套件的內容，類似於組件。 

如果您必須建立程式庫或更改現有的程式庫 (並且具備執行此操作所需的權限)，但伺服器上的檔案系統受到限制，而您無法將程式庫檔案複製到伺服器能夠存取的位置，此選項會相當有用。

**PLATFORM = WINDOWS**

指定程式庫內容的平台。 此值會預設為 SQL Server 執行所在的主機平台。 因此，使用者不需要指定此值。 當支援多個平台或使用者必須指定不同的平台時，才需要指定此值。 

Windows 是目前唯一支援的平台。

## <a name="remarks"></a>Remarks

針對 R 語言，當使用檔案時，必須針對 Windows，以具有 .ZIP 副檔名的 ZIP 壓縮封存檔案形式備妥套件。 目前僅支援 Windows 平台。 

`CREATE EXTERNAL LIBRARY` 陳述式會將程式庫位元上傳至資料庫。 當使用者使用 [sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md)來執行外部指令碼並呼叫套件或程式庫時，就會安裝程式庫。

上傳至執行個體的程式庫可以是公用或私用程式庫。 如果程式庫是由 `dbo` 的成員所建立，該程式庫就是公用程式庫，而可以與所有使用者共用。 否則，程式庫就只是該使用者的私用程式庫。

## <a name="permissions"></a>[權限]

需要 `CREATE EXTERNAL LIBRARY` 權限。 根據預設，任何具有 **dbo** 或為 **db_owner** 角色成員的使用者，都有建立外部程式庫的權限。 對於其他所有使用者，您必須使用 [GRANT](https://docs.microsoft.com/sql/t-sql/statements/grant-database-permissions-transact-sql) 陳述式指定 CREATE EXTERNAL LIBRARY 做為權限，以明確授予權限給他們。

若要修改程式庫，需要個別的權限 `ALTER ANY EXTERNAL LIBRARY`。

## <a name="examples"></a>範例

### <a name="a-add-an-external-library-to-a-database"></a>A. 將外部程式庫新增至資料庫  

下列範例會將名為 `customPackage` 的外部程式庫新增至資料庫。

```sql
CREATE EXTERNAL LIBRARY customPackage
FROM (CONTENT = 'C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\customPackage.zip') WITH (LANGUAGE = 'R');
```

將程式庫成功上傳至執行個體之後，使用者需執行 `sp_execute_external_script` 程序來安裝該程式庫。

```sql
EXEC sp_execute_external_script 
@language =N'R', 
@script=N'library(customPackage)'
```

### <a name="b-installing-packages-with-dependencies"></a>B. 安裝具有相依性的套件

如果您想要安裝的套件具有許多相依性，請務必在嘗試安裝目標套件「之前」，先分析第一層和第二層的相依性，並確定所有必要的套件都可供使用。

例如，假設您想要安裝新套件 `packageA`：

+ `packageA` 具有 `packageB` 相依性
+ `packageB` 具有 `packageC` 相依性

若要成功安裝 `packageA`，您必須在將 `packageA` 新增至 SQL Server 時，為 `packageB` 和 `packageC` 建立程式庫。 請務必一併檢查所需的套件版本。

實際上，常用套件的套件相依性通常比這個簡單範例複雜許多。 例如，**ggplot2** 可能需要超過 30 個套件，而這些套件可能需要伺服器上所未提供的額外套件。 任何套件遺失或套件版本錯誤都可能造成安裝失敗。

由於只從查看套件資訊清單很難判斷所有相依性，因此建議您使用 [miniCRAN](https://cran.r-project.org/web/packages/miniCRAN/index.html) 之類的套件，以識別成功完成安裝可能需要的所有套件。

+ 上傳目標套件及其相依性。 所有檔案都必須位於伺服器能夠存取的一個資料夾中。

    ```sql
    CREATE EXTERNAL LIBRARY packageA 
    FROM (CONTENT = 'C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\packageA.zip') 
    WITH (LANGUAGE = 'R'); 
    GO

    CREATE EXTERNAL LIBRARY packageB FROM (CONTENT = 'C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\packageB.zip') 
    WITH (LANGUAGE = 'R');
    GO

    CREATE EXTERNAL LIBRARY packageC FROM (CONTENT = 'C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\packageC.zip') 
    WITH (LANGUAGE = 'R');
    GO
    ```

+ 先安裝必要套件。

    如果已經將必要套件上傳至執行個體，就無須再次新增。 只要確認現有套件的版本是否正確即可。 
    
    第一次執行 `sp_execute_external_script` 來安裝套件 `packageA` 時，會依照正確順序安裝必要套件 `packageC` 和 `packageB`。

    不過，如果有任何必要套件無法供使用，安裝目標套件 `packageA` 時就會失敗。

    ```sql
    EXEC sp_execute_external_script 
    @language =N'R', 
    @script=N'
    # load the desired package packageA
    library(packageA)
    print(packageVersion("packageA"))
    '
    ```

### <a name="c-create-a-library-from-a-byte-stream"></a>C. 從位元組資料流建立程式庫

如果您無法將套件檔案儲存在伺服器上的位置，則可以在變數中傳遞套件內容。 下列範例會將位元作為十六進位常值傳遞以建立程式庫。

```SQL
CREATE EXTERNAL LIBRARY customLibrary FROM (CONTENT = 0xabc123) WITH (LANGUAGE = 'R');
```

> [!NOTE]
> 此程式碼範例僅示範語法；`CONTENT =` 中的二進位值已被截斷以提高可讀性，且並不會建立可運作的程式庫。 二進位變數的實際內容會更長。

### <a name="d-change-an-existing-package-library"></a>D. 變更現有的套件程式庫

`ALTER EXTERNAL LIBRARY` DDL 陳述式可用來新增程式庫內容，或修改現有的程式庫內容。 若要修改現有的程式庫，需要 `ALTER ANY EXTERNAL LIBRARY` 權限。

如需詳細資訊，請參閱 [ALTER EXTERNAL LIBRARY](alter-external-library-transact-sql.md)。

## <a name="see-also"></a>另請參閱

[ALTER EXTERNAL LIBRARY (Transact-SQL)](alter-external-library-transact-sql.md)  
[DROP EXTERNAL LIBRARY (Transact-SQL)](drop-external-library-transact-sql.md)  
[sys.external_library_files](../../relational-databases/system-catalog-views/sys-external-library-files-transact-sql.md)  
[sys.external_libraries](../../relational-databases/system-catalog-views/sys-external-libraries-transact-sql.md)  
