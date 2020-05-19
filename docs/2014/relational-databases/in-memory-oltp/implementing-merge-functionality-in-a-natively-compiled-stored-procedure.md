---
title: 執行合併功能 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: in-memory-oltp
ms.topic: conceptual
ms.assetid: d4bcdc36-3302-4abc-9b35-64ec2b920986
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: e762c1999a4206d5277050934e82b5d5d5c59371
ms.sourcegitcommit: b72c9fc9436c44c6a21fd96223c73bf94706c06b
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/01/2020
ms.locfileid: "82715122"
---
# <a name="implementing-merge-functionality"></a>實作 MERGE 功能
  根據資料庫中是否已有某個特殊資料列存在而定，資料庫可能需要執行插入或更新。  
  
 在不使用 `MERGE` 陳述式的情況下，以下提供可在 [!INCLUDE[tsql](../../includes/tsql-md.md)] 中使用的一種方式：  
  
```sql  
UPDATE mytable SET col=@somevalue WHERE myPK = @parm  
IF @@ROWCOUNT = 0  
    INSERT mytable (columns) VALUES (@parm, @other values)  
```  
  
 實作合併的另一種 [!INCLUDE[tsql](../../includes/tsql-md.md)] 方法：  
  
```sql  
IF EXISTS (SELECT 1 FROM mytable WHERE myPK = @parm)  
    UPDATE....  
ELSE  
    INSERT  
```  
  
 針對原生編譯預存程序  
  
```sql  
DECLARE @i  int  = 0  -- or whatever your PK data type is  
UPDATE mytable SET @i=myPK, othercolums = other values WHERE myPK = @parm  
IF @i = 0  
   INSERT....  
```  
  
## <a name="see-also"></a>另請參閱  
 [原生編譯預存程序的移轉問題](migration-issues-for-natively-compiled-stored-procedures.md)   
 [記憶體中的 OLTP 不支援 Transact-SQL 建構](transact-sql-constructs-not-supported-by-in-memory-oltp.md)  
  
  
