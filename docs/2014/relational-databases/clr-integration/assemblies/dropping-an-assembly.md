---
title: 卸除組件 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: clr
ms.topic: reference
helpviewer_keywords:
- removing assemblies
- DROP ASSEMBLY statement
- assemblies [CLR integration], removing
- dropping assemblies
ms.assetid: 03481034-dc91-4488-ab24-ba44243e2690
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: d7dceef4651804dabf4080d6f8b85d0597b1957b
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/02/2018
ms.locfileid: "48135271"
---
# <a name="dropping-an-assembly"></a>卸除組件
  如果您不再需要已經使用 CREATE ASSEMBLY 陳述式在 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 中註冊之組件所提供的功能，就可以刪除或卸除這些組件。 卸除組件會從資料庫中移除組件及其所有相關聯的檔案 (例如偵錯檔案)。 若要卸除組件，請使用 DROP ASSEMBLY 陳述式搭配下列語法：  
  
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
 您必須先卸除所有相依物件，然後再執行 DROP TYPE 陳述式。 下列[!INCLUDE[tsql](../../../includes/tsql-md.md)]查詢找出使用 UDT 中的參數與資料行的所有**AdventureWorks**資料庫。  
  
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
  
## <a name="see-also"></a>另請參閱  
 [管理 CLR 整合組件](managing-clr-integration-assemblies.md)   
 [變更組件](altering-an-assembly.md)   
 [建立組件](creating-an-assembly.md)   
 [卸除彙總&#40;Transact SQL&#41;](/sql/t-sql/statements/drop-aggregate-transact-sql)   
 [DROP FUNCTION &#40;Transact-SQL&#41;](/sql/t-sql/statements/drop-function-transact-sql)   
 [DROP PROCEDURE &#40;Transact-SQL&#41;](/sql/t-sql/statements/drop-procedure-transact-sql)   
 [DROP TRIGGER &#40;Transact-SQL&#41;](/sql/t-sql/statements/drop-trigger-transact-sql)   
 [卸除類型&#40;Transact SQL&#41;](/sql/t-sql/statements/drop-type-transact-sql)  
  
  
