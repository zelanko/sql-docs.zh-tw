---
title: 實作 MERGE 功能 |Microsoft 文件
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine-imoltp
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: d4bcdc36-3302-4abc-9b35-64ec2b920986
caps.latest.revision: 6
author: stevestein
ms.author: sstein
manager: jhubbard
ms.openlocfilehash: e2d4c6255b7b6a91fad1d99c2676bf76fae68385
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36034561"
---
# <a name="implementing-merge-functionality"></a>實作 MERGE 功能
  根據資料庫中是否已有某個特殊資料列存在而定，資料庫可能需要執行插入或更新。  
  
 不使用`MERGE`陳述式中，以下是您可以使用中的其中一個方法[!INCLUDE[tsql](../../includes/tsql-md.md)]:  
  
```tsql  
UPDATE mytable SET col=@somevalue WHERE myPK = @parm  
IF @@ROWCOUNT = 0  
    INSERT mytable (columns) VALUES (@parm, @other values)  
```  
  
 實作合併的另一種 [!INCLUDE[tsql](../../includes/tsql-md.md)] 方法：  
  
```tsql  
IF EXISTS (SELECT 1 FROM mytable WHERE myPK = @parm)  
    UPDATE….  
ELSE  
    INSERT  
```  
  
 針對原生編譯預存程序  
  
```tsql  
DECLARE @i  int  = 0  -- or whatever your PK data type is  
UPDATE mytable SET @i=myPK, othercolums = other values WHERE myPK = @parm  
IF @i = 0  
   INSERT….  
```  
  
## <a name="see-also"></a>另請參閱  
 [原生編譯預存程序的移轉問題](migration-issues-for-natively-compiled-stored-procedures.md)   
 [記憶體中的 OLTP 不支援 Transact-SQL 建構](transact-sql-constructs-not-supported-by-in-memory-oltp.md)  
  
  