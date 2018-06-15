---
title: OBJECT_DEFINITION (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.component: t-sql|functions
ms.reviewer: ''
ms.suite: sql
ms.technology: t-sql
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- OBJECT_DEFINITION_TSQL
- OBJECT_DEFINITION
dev_langs:
- TSQL
helpviewer_keywords:
- viewing source text
- source text [SQL Server]
- displaying source text
- OBJECT_DEFINITION function
ms.assetid: 2ac837c7-eca9-4d29-b06e-72e30450c68d
caps.latest.revision: 27
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: 4da307c294b754ec58fe4b68fd1bdbae8c35af07
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
ms.locfileid: "33053185"
---
# <a name="objectdefinition-transact-sql"></a>OBJECT_DEFINITION (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  傳回指定物件定義的 [!INCLUDE[tsql](../../includes/tsql-md.md)] 來源文字。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
OBJECT_DEFINITION ( object_id )  
```  
  
## <a name="arguments"></a>引數  
 *object_id*  
 這是所要使用的物件識別碼。 *object_id* 為 **int**，並會用來代表目前資料庫內容中的物件。  
  
## <a name="return-types"></a>傳回類型  
 **nvarchar(max)**  
  
## <a name="exceptions"></a>例外狀況  
 當發生錯誤，或呼叫端沒有檢視物件的權限時，便會傳回 NULL。  
  
 使用者只能檢視使用者擁有或被授與某些權限之安全性實體的中繼資料。 這表示發出中繼資料的內建函數 (例如，OBJECT_DEFINITION) 會在使用者不具有該物件任何權限時傳回 NULL。 如需相關資訊，請參閱 [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md)。  
  
## <a name="remarks"></a>Remarks  
 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 假設 *object_id* 在目前資料庫內容中。 物件定義的定序一律符合發出呼叫之資料庫內容的定序。  
  
 OBJECT_DEFINITION 適用於下列物件類型：  
  
-   C = 檢查條件約束  
  
-   D = 預設值 (條件約束或獨立式)  
  
-   P = SQL 預存程序  
  
-   FN = SQL 純量函數  
  
-   R = 規則  
  
-   RF = 複寫篩選程序  
  
-   TR = SQL 觸發程序 (結構描述範圍的 DML 觸發程序，或在資料庫或伺服器範圍的 DDL 觸發程序)  
  
-   IF = SQL 嵌入資料表值函式  
  
-   TF = SQL 資料表值函式  
  
-   V = 檢視  
  
## <a name="permissions"></a>Permissions  
 系統物件定義是公開顯示的。 凡具有 ALTER、CONTROL、TAKE OWNERSHIP 或 VIEW DEFINITION 任一權限的物件擁有者或被授與者，都看得到使用者物件的定義。 **db_owner**、 **db_ddladmin**和 **db_securityadmin** 固定資料庫角色的成員隱含地擁有這些權限。  
  
## <a name="examples"></a>範例  
  
### <a name="a-returning-the-source-text-of-a-user-defined-object"></a>A. 傳回使用者自訂物件的來源文字  
 下列範例會傳回 `uAddress` 結構描述中 `Person` 使用者自訂觸發程序的定義。 內建函數 `OBJECT_ID` 用來將觸發程序的物件識別碼傳回給 `OBJECT_DEFINITION` 陳述式。  
  
```  
USE AdventureWorks2012;  
GO  
SELECT OBJECT_DEFINITION (OBJECT_ID(N'Person.uAddress')) AS [Trigger Definition];   
GO  
```  
  
### <a name="b-returning-the-source-text-of-a-system-object"></a>B. 傳回系統物件的來源文字  
 下列範例會傳回系統預存程序 `sys.sp_columns` 的定義。  
  
```  
USE AdventureWorks2012;  
GO  
SELECT OBJECT_DEFINITION (OBJECT_ID(N'sys.sp_columns')) AS [Object Definition];  
GO  
```  
  
## <a name="see-also"></a>另請參閱  
 [中繼資料函數 &#40;Transact-SQL&#41;](../../t-sql/functions/metadata-functions-transact-sql.md)   
 [OBJECT_NAME &#40;Transact-SQL&#41;](../../t-sql/functions/object-name-transact-sql.md)   
 [OBJECT_ID &#40;Transact-SQL&#41;](../../t-sql/functions/object-id-transact-sql.md)   
 [sp_helptext &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helptext-transact-sql.md)   
 [sys.sql_modules &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-sql-modules-transact-sql.md)   
 [sys.server_sql_modules &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-server-sql-modules-transact-sql.md)  
  
  
