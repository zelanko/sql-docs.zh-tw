---
title: "卸除組件 |Microsoft 文件"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: clr
ms.reviewer: 
ms.suite: sql
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: reference
helpviewer_keywords:
- removing assemblies
- DROP ASSEMBLY statement
- assemblies [CLR integration], removing
- dropping assemblies
ms.assetid: 03481034-dc91-4488-ab24-ba44243e2690
caps.latest.revision: "16"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 5c3f4ddb7618756878da84112ea713520a0d3e01
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/08/2018
---
# <a name="dropping-an-assembly"></a>卸除組件
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]中已註冊的組件[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]使用 CREATE ASSEMBLY 陳述式可以刪除或卸除，當不再需要所提供的功能。 卸除組件會從資料庫中移除組件及其所有相關聯的檔案 (例如偵錯檔案)。 若要卸除組件，請使用 DROP ASSEMBLY 陳述式搭配下列語法：  
  
```  
DROP ASSEMBLY MyDotNETAssembly  
```  
  
 雖然 DROP ASSEMBLY 不會干擾參考目前執行中組件的任何程式碼，但是在 DROP ASSEMBLY 執行之後，任何嘗試叫用此組件的行為都會失敗。  
  
 如果組件是由資料庫中的另一個組件所參考，或者如果它是由目前資料庫中的 Common Language Runtime (CLR) 函數、程序、觸發程序、使用者定義型別 (UDT) 或使用者定義彙總 (UDA) 所使用，DROP ASSEMBLY 就會傳回錯誤。 請先使用 DROP AGGREGATE、DROP FUNCTION、DROP PROCEDURE、DROP TRIGGER 和 DROP TYPE 陳述式來刪除此組件所包含的任何 Managed 資料庫物件。  
  
## <a name="removing-a-udt-from-the-database"></a>從資料庫移除 UDT  
 DROP TYPE 陳述式會從目前資料庫移除 UDT。 一旦卸除 UDT 之後，您就可以使用 DROP ASSEMBLY 陳述式，從資料庫中卸除組件。  
  
 如果物件相依於 UDT，DROP TYPE 陳述式就會失敗，如下列情況所示：  
  
-   資料庫中包含使用 UDT 定義之資料行的資料表。  
  
-   使用 WITH SCHEMABINDING 子句在資料庫中建立的函數、預存程序或觸發程序 (這些項目會使用 UDT 變數或參數)。  
  
### <a name="finding-udt-dependencies"></a>尋找 UDT 相依性  
 您必須先卸除所有相依物件，然後再執行 DROP TYPE 陳述式。 下列[!INCLUDE[tsql](../../../includes/tsql-md.md)]查詢找出使用 UDT 的參數與資料行的所有**AdventureWorks**資料庫。  
  
```  
USE Adventureworks;  
SELECT o.name AS major_name, o.type_desc AS major_type_desc  
     , c.name AS minor_name, c.type_desc AS minor_type_desc  
     , at.assembly_class  
  FROM (  
        SELECT object_id, name, user_type_id, 'SQL_COLUMN' AS type_desc  
          FROM sys.columns  
     UNION ALL  
        SELECT object_id, name, user_type_id, 'SQL_PROCEDURE_PARAMETER'  
          FROM sys.parameters  
     ) AS c  
  JOIN sys.objects AS o  
    ON o.object_id = c.object_id  
  JOIN sys.assembly_types AS at  
    ON at.user_type_id = c.user_type_id;   
```  
  
## <a name="see-also"></a>請參閱  
 [管理 CLR 整合組件](../../../relational-databases/clr-integration/assemblies/managing-clr-integration-assemblies.md)   
 [變更組件](../../../relational-databases/clr-integration/assemblies/altering-an-assembly.md)   
 [建立組件](../../../relational-databases/clr-integration/assemblies/creating-an-assembly.md)   
 [卸除彙總 &#40;TRANSACT-SQL &#41;](../../../t-sql/statements/drop-aggregate-transact-sql.md)   
 [卸除函數 &#40;TRANSACT-SQL &#41;](../../../t-sql/statements/drop-function-transact-sql.md)   
 [卸除程序 &#40;TRANSACT-SQL &#41;](../../../t-sql/statements/drop-procedure-transact-sql.md)   
 [DROP TRIGGER &#40;Transact-SQL&#41;](../../../t-sql/statements/drop-trigger-transact-sql.md)   
 [卸除類型 &#40;TRANSACT-SQL &#41;](../../../t-sql/statements/drop-type-transact-sql.md)  
  
  
