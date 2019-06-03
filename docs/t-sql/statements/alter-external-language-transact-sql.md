---
title: ALTER EXTERNAL LANGUAGE (Transact-SQL) - SQL Server | Microsoft Docs
ms.custom: ''
ms.date: 05/22/2019
ms.prod: sql
ms.reviewer: dphansen
ms.technology: t-sql
ms.topic: language-reference
author: nelgson
ms.author: negust
manager: cgronlun
monikerRange: '>=sql-server-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 41faa953036692a0fa633a2d1ccc7244e02e13e4
ms.sourcegitcommit: be09f0f3708f2e8eb9f6f44e632162709b4daff6
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/21/2019
ms.locfileid: "65994946"
---
# <a name="create-external-language-transact-sql"></a>CREATE EXTERNAL LANGUAGE (Transact-SQL)
[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

修改資料庫現有外部語言延伸模組中的內容。

## <a name="syntax"></a>語法

```text
ALTER EXTERNAL LANGUAGE language_name  
[ AUTHORIZATION owner_name ]
{
    SET <file_spec>
    | ADD <file_spec>
    | REMOVE <file_spec>
}
[ ; ]  

<file_spec> ::=  
{
    ( CONTENT = {<external_lang_specifier> | <content_bits>,
    FILE_NAME = <external_lang_file_name>
    [, PLATFORM = <platform> ]
    [, PARAMETERS = <external_lang_parameters> ]
    [, ENVIRONMENT_VARIABLES = <external_lang_env_variables> ] )
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

< external_lang_parameters > :: =  
'extension_specific_parameters'
```

### <a name="arguments"></a>引數

**language_name**

語言是資料庫範圍的物件。 語言名稱在資料庫內必須是唯一的。

**owner_name**

指定擁有外部語言的使用者或角色名稱。 若未指定，擁有權便歸目前使用者。 視權限而定，其他使用者可能需要獲得明確的權限，才能使用特定語言來執行指令碼。

**file_spec**

指定語言擴充功能的內容。每個平台的特定語言只允許一種檔案規格。 

**external_lang_specifier**

.zip 或 .tar.gz 檔案的完整檔案路徑包含延伸模組程式碼。 此內容可以是 .zip 檔案 (Windows) 或 .tar.gz (Linux) 的路徑。

**content_bits**

以十六進位常值的形式指定語言內容，類似於組件。
如果您必須建立語言或更改現有的語言 (且具備執行此操作所需的權限)，但伺服器上的檔案系統受到限制，而您無法將程式庫檔案複製到伺服器能夠存取的位置，則此選項會相當有用。

**external_lang_file_name**

副檔名為 .dll 或 .so 檔案的名稱。 當 <external_lang_specifier> .zip 或 tar.gz 有數個 .dll 或 .so 檔案時，那麼一定要有此項目才能識別正確的檔案。

**external_lang_parameters**

這有可能向外部語言執行階段提供一組參數。 外部處理序啟動之後，向外部執行階段提供參數值。 但在外部處理序啟動之前，語言延伸模組可以存取環境變數。

**external_lang_env_variables**

這可能會在外部處理序啟動之前，向外部語言執行階段提供一組環境變數。 例如，執行階段本身的主目錄即為環境變數範例。 例如：JRE_HOME。

**平台**

混合式作業系統案例需要此參數。 在混合式架構中，語言需要在每個平台註冊一次。 平台和語言名稱會是每種外部語言的唯一索引鍵。 如未指定任何平台，則假設為目前的作業系統。

## <a name="remarks"></a>Remarks

在 CTP 3.0 中，不支援 **PARAMETERS** 和 **ENVIRONMENT_VARIABLES**。

## <a name="permissions"></a>權限

需要 `ALTER ANY EXTERNAL LANGUAGE` 權限。 根據預設，任何具有 **dbo** 或為 **db_owner** 角色成員的使用者，都有更改外部語言的權限。 金對其他所有使用者，您必須使用 [GRANT](https://docs.microsoft.com/sql/t-sql/statements/grant-database-permissions-transact-sql) 陳述式指定 ALTER ANY EXTERNAL LANGUAGE 為權限，明確授與其權限。

## <a name="examples"></a>範例

### <a name="alter-an-external-language-in-a-database"></a>更改資料庫中的外部語言  

下例會將外部語言呼叫的 Java 新增至 Windows 之 SQL Server 的資料庫。

```sql
ALTER EXTERNAL LANGUAGE Java 
SET (CONTENT = N'<path-to-zip>', FILE_NAME = 'javaextension.dll');
GO
```

## <a name="see-also"></a>另請參閱

[CREATE EXTERNAL LANGUAGE (Transact-SQL)](create-external-language-transact-sql.md)  
[DROP EXTERNAL LANGUAGE (Transact-SQL)](drop-external-language-transact-sql.md)  
[sys.external_languages](../../relational-databases/system-catalog-views/sys-external-languages-transact-sql.md)  
[sys.external_language_files](../../relational-databases/system-catalog-views/sys-external-language-files-transact-sql.md)  
