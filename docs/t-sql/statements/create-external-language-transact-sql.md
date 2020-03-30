---
title: CREATE EXTERNAL LANGUAGE (Transact-SQL) - SQL Server | Microsoft Docs
ms.custom: ''
ms.date: 02/19/2020
ms.prod: sql
ms.reviewer: dphansen
ms.technology: language-extensions
ms.topic: language-reference
author: nelgson
ms.author: negust
manager: cgronlun
monikerRange: '>=sql-server-ver15||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 65f805c0d2467f3b4301ed1d237284cb61224b97
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/30/2020
ms.locfileid: "77520891"
---
# <a name="create-external-language-transact-sql"></a>CREATE EXTERNAL LANGUAGE (Transact-SQL)
[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

從指定的檔案路徑或位元組資料流，註冊資料庫中的外部延伸模組。 此陳述式可作為一般機制，供資料庫管理員在 SQL Server 支援的任何 OS 平台上註冊新外部語言延伸模組。 如需詳細資訊，請參閱[語言延伸模組](https://docs.microsoft.com/sql/language-extensions/language-extensions-overview)。

> [!NOTE]
> 目前只支援 **Java** 作為外部語言。 **R** 和 **Python** 為保留的名稱，且不能使用這些特定的名稱來建立任何外部語言。 如需如何使用 **R** 和 **Python** 的詳細資訊，請參閱 [SQL Server 機器學習服務](https://docs.microsoft.com/sql/advanced-analytics/)。

## <a name="syntax"></a>語法

```text
CREATE EXTERNAL LANGUAGE language_name  
[ AUTHORIZATION owner_name ]  
FROM <file_spec> [ ,...2 ]  
[ ; ]  

<file_spec> ::=  
{
    ( CONTENT = { <external_lang_specifier> | <content_bits> },
    FILE_NAME = <external_lang_file_name>
    [ , PLATFORM = <platform> ]
    [ , PARAMETERS = <external_lang_parameters> ]
    [ , ENVIRONMENT_VARIABLES = <external_lang_env_variables> ] )
}

<external_lang_specifier> :: =  
{
    '[file_path\]os_file_name'  
}

<content_bits> :: =  
{
    varbinary_literal
    | varbinary_expression
}

<external_lang_file_name> :: =  
'extension_file_name'


<platform> :: =
{
    WINDOWS
  | LINUX
}

<external_lang_parameters> :: =  
'extension_specific_parameters'
```

### <a name="arguments"></a>引數

**language_name**

語言是資料庫範圍的物件。 語言名稱在資料庫內必須是唯一的。

**owner_name**

指定擁有外部語言的使用者或角色名稱。 若未指定，擁有權便歸目前使用者。 視權限而定，其他使用者可能需要獲得明確的權限，才能使用特定語言來執行指令碼。

**file_spec**

指定語言延伸模組的內容。 每個平台的特定語言只允許一種檔案規格。

**external_lang_specifier**

.zip 或 .tar.gz 檔案的完整檔案路徑包含延伸模組程式碼。 此內容可以是 .zip 檔案 (Windows) 或 .tar.gz (Linux) 的路徑。

**content_bits**

以十六進位常值形式指定語言的內容，類似於組件。

如果您必須建立語言或更改現有的語言 (且具備執行此操作所需的權限)，但伺服器上的檔案系統受到限制，而您無法將程式庫檔案複製到伺服器能夠存取的位置，則此選項會相當有用。

**external_lang_file_name**

.dll 或 .so 檔案副檔名名稱。 當 <external_lang_specifier> .zip 或 tar.gz 有數個 .dll 或 .so 檔案時，那麼一定要有此項目才能識別正確的檔案。

**external_lang_parameters**

這有可能向外部語言執行階段提供一組參數。 外部處理序啟動之後，參數值會提供給外部執行階段。 但在外部處理序啟動之前，語言延伸模組可以存取環境變數。

.**external_lang_env_variables**

這可能會在外部處理序啟動之前，向外部語言執行階段提供一組環境變數。 例如，執行階段本身的主目錄即為環境變數範例。 例如：JRE_HOME。

**平台**

混合式作業系統案例需要此參數。 在混合式架構中，語言需要在每個平台註冊一次。 平台和語言名稱會是每種外部語言的唯一索引鍵。 如未指定任何平台，則假設為目前的作業系統。

## <a name="remarks"></a>備註

目前，不支援 **PARAMETERS** 和 **ENVIRONMENT_VARIABLES**。

## <a name="permissions"></a>權限

需要 `CREATE EXTERNAL LANGUAGE` 權限。 根據預設，任何具有 **dbo** 或為 **db_owner** 角色成員使用者都有建立外部語言的權限。 針對其他所有使用者，您必須使用 [GRANT](https://docs.microsoft.com/sql/t-sql/statements/grant-database-permissions-transact-sql) 陳述式指定 CREATE EXTERNAL LANGUAGE 作為權限，以明確授與權限給他們。

若要修改程式庫，需要個別的權限 `ALTER ANY EXTERNAL LANGUAGE`。

### <a name="execute-external-script-permission"></a>EXECUTE EXTERNAL SCRIPT 權限

您可以使用 EXECUTE EXTERNAL SCRIPT 權限，以便能授與特定語言的外部指令碼執行。 與 EXECUTE ANY EXTERNAL SCRIPT 資料庫權限不同，這不允許授與特定語言的執行權限。

這表示非 **dbo** 使用者必須獲授與權限來執行特定的語言：

```sql
GRANT EXECUTE EXTERNAL SCRIPT ON EXTERNAL LANGUAGE ::language_name 
TO database_principal_name;
```

### <a name="reference-permissions-to-external-libraries"></a>外部程式庫的參考權限

類似於組件，外部語言需要參考權限，才能使外部程式庫與外部語言之間產生連結。 例如，如果要卸除外部語言，使用者首先必須確定參考該語言的所有外部程式庫都已卸除。 在階層中，您可以將外部語言視為比外部程式庫更高層級的物件。

## <a name="examples"></a>範例

### <a name="a-create-an-external-language-in-a-database"></a>A. 在資料庫中建立外部語言  

下例會將外部語言呼叫的 Java 新增至 Windows 之 SQL Server 的資料庫。

```sql
CREATE EXTERNAL LANGUAGE Java 
FROM (CONTENT = N'<path-to-zip>', FILE_NAME = 'javaextension.dll');
GO
```

### <a name="b-create-an-external-language-for-both-windows-and-linux"></a>B. 建立適用於 Windows 和 Linux 的外部語言

您最多可以指定兩個 `<file_spec>`，一個用於 Windows，一個用於 Linux。

```sql
CREATE EXTERNAL LANGUAGE Java
FROM
(CONTENT = N'<path-to-zip>', FILE_NAME = 'javaextension.dll', PLATFORM = WINDOWS),
(CONTENT = N'<path-to-tar.gz>', FILE_NAME = 'javaextension.so', PLATFORM = LINUX);
GO
```
### <a name="c-grant-permissions-to-execute-external-script"></a>C. 授與執行外部指令碼的權限

下列範例對 **mylogin** 授與可使用 **Java** 外部語言執行指令碼的主體存取權。

```sql
GRANT EXECUTE EXTERNAL SCRIPT ON EXTERNAL LANGUAGE ::Java 
TO mylogin;
```


## <a name="see-also"></a>另請參閱

[ALTER EXTERNAL LANGUAGE (Transact-SQL)](alter-external-language-transact-sql.md)  
[DROP EXTERNAL LANGUAGE (Transact-SQL)](drop-external-language-transact-sql.md)  
[sys.external_languages](../../relational-databases/system-catalog-views/sys-external-languages-transact-sql.md)  
[sys.external_language_files](../../relational-databases/system-catalog-views/sys-external-language-files-transact-sql.md)  
