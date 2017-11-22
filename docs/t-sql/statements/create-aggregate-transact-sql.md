---
title: "建立彙總 (TRANSACT-SQL) |Microsoft 文件"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: sql-database
ms.service: 
ms.component: t-sql|statements
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- CREATE_AGGREGATE_TSQL
- CREATE AGGREGATE
- AGGREGATE_TSQL
- AGGREGATE
dev_langs: TSQL
helpviewer_keywords:
- CREATE AGGREGATE statement
- aggregate functions [SQL Server], user-defined
- user-defined functions [CLR integration]
ms.assetid: 62eebc19-9f15-4245-94fa-b3fcd64a9d42
caps.latest.revision: "50"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: 877e72a18d11fbf31a6ea61f6abed515f5b746f6
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/17/2017
---
# <a name="create-aggregate-transact-sql"></a>CREATE AGGREGATE (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  建立使用者定義的彙總函式 (其實作定義在 [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] 的組件類別中)。 若要使 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 將彙總函式繫結到它的實作，您必須先利用 CREATE ASSEMBLY 陳述式，將包含這項實作的 [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] 組件上傳到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體中。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
CREATE AGGREGATE [ schema_name . ] aggregate_name  
        (@param_name <input_sqltype>   
        [ ,...n ] )  
RETURNS <return_sqltype>  
EXTERNAL NAME assembly_name [ .class_name ]  
  
<input_sqltype> ::=  
        system_scalar_type | { [ udt_schema_name. ] udt_type_name }  
  
<return_sqltype> ::=  
        system_scalar_type | { [ udt_schema_name. ] udt_type_name }  
  
```  
  
## <a name="arguments"></a>引數  
 *schema_name*  
 這是使用者定義彙總函式所屬的結構描述名稱。  
  
 *aggregate_name*  
 這是您要建立之彙總函式的名稱。  
  
 **@***param_name*  
 使用者定義彙總中的一或多個參數。 在執行彙總函式時，使用者必須提供參數的值。 指定參數名稱，使用"at"記號 (**@**) 作為第一個字元。 參數名稱必須遵守的規則[識別碼](../../relational-databases/databases/database-identifiers.md)。 這些參數是函數的本機參數。  
  
 *system_scalar_type*  
 這是用來保留輸入參數值或傳回值的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 系統純量資料類型。 所有純量資料類型可以做為參數中使用使用者定義彙總的除了**文字**， **ntext**，和**映像**。 非純量類型，例如**游標**和**資料表**，不能指定。  
  
 *udt_schema_name*  
 這是 CLR 使用者自訂類型所屬的結構描述名稱。 如果未指定，[!INCLUDE[ssDE](../../includes/ssde-md.md)]參考*udt_type_name*順序如下：  
  
-   原生 SQL 類型命名空間。  
  
-   目前資料庫中之目前使用者的預設結構描述。  
  
-   目前資料庫中的 **dbo** 結構描述。  
  
 *udt_type_name*  
 這是目前資料庫中已建立之 CLR 使用者自訂類型的名稱。 如果*udt_schema_name*未指定，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]假設類型屬於目前使用者的結構描述。  
  
 *assembly_name* [ **。***class_name* ]  
 指定要繫結使用者定義彙總函式的組件，以及 (選擇性) 組件所屬的結構描述名稱和實作使用者自訂彙總的組件中之類別名稱。 這個組件必須已利用 CREATE ASSEMBLY 陳述式建立在資料庫中。 *class_name*必須是有效[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]識別碼，且符合組件中現有的類別名稱。 *class_name*可能是命名空間限定名稱，如果用來撰寫類別的程式設計語言使用命名空間，例如 C#。 如果*class_name*未指定，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]假設它是與相同*aggregate_name*。  
  
## <a name="remarks"></a>備註  
 依預設，會關閉 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行 CLR 程式碼的能力。 您可以建立、 修改和卸除參考 managed 程式碼模組的資料庫物件，但無法在這些模組中的程式碼的執行個體中執行[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]除非[clr enabled 選項](../../database-engine/configure-windows/clr-enabled-server-configuration-option.md)啟用利用[sp_設定](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md)。  
  
 在參考的組件類別*assembly_name* ，且它的方法，可滿足使用者定義的彙總函式實作的執行個體中的所有需求[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。 如需詳細資訊，請參閱[clr 使用者定義彙總](../../relational-databases/clr-integration-database-objects-user-defined-functions/clr-user-defined-aggregates.md)。  
  
## <a name="permissions"></a>Permissions  
 需要 CREATE AGGREGATE 權限，以及 EXTERNAL NAME 子句所指定之組件的 REFERENCES 權限。  
  
## <a name="examples"></a>範例  
 下列範例會假設 StringUtilities.csproj 範例應用程式已編譯。 如需詳細資訊，請參閱[字串公用程式函數範例](http://msdn.microsoft.com/library/9623013f-15f1-4614-8dac-1155e57c880c)。  
  
 下列範例會建立彙總 `Concatenate`。 在建立這項彙總之前，會將 `StringUtilities.dll` 組件註冊在本機資料庫中。  
  
```  
USE AdventureWorks2012;  
GO  
DECLARE @SamplesPath nvarchar(1024)  
-- You may have to modify the value of the this variable if you have  
--installed the sample some location other than the default location.  
  
SELECT @SamplesPath = REPLACE(physical_name, 'Microsoft SQL Server\MSSQL13.MSSQLSERVER\MSSQL\DATA\master.mdf', 'Microsoft SQL Server\130\Samples\Engine\Programmability\CLR\')   
     FROM master.sys.database_files   
     WHERE name = 'master';  
  
CREATE ASSEMBLY StringUtilities FROM @SamplesPath + 'StringUtilities\CS\StringUtilities\bin\debug\StringUtilities.dll'  
WITH PERMISSION_SET=SAFE;  
GO  
  
CREATE AGGREGATE Concatenate(@input nvarchar(4000))  
RETURNS nvarchar(4000)  
EXTERNAL NAME [StringUtilities].[Microsoft.Samples.SqlServer.Concatenate];  
GO  
```  
  
## <a name="see-also"></a>請參閱＜  
 [卸除彙總 &#40;TRANSACT-SQL &#41;](../../t-sql/statements/drop-aggregate-transact-sql.md)  
  
  
