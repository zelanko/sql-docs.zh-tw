---
title: 變更資料庫鏡像工作階段中的交易安全性 (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
helpviewer_keywords:
- transaction safety [SQL Server database mirroring]
ms.assetid: 8b03bb82-8589-4558-8545-9942fe008391
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: d8bc9d0fb639770d33507c29a6ec67f60bd0434a
ms.sourcegitcommit: 9ee72c507ab447ac69014a7eea4e43523a0a3ec4
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/17/2020
ms.locfileid: "84934392"
---
# <a name="change-transaction-safety-in-a-database-mirroring-session-transact-sql"></a>變更資料庫鏡像工作階段中的異動安全性 (Transact-SQL)
  交易安全性是控制工作階段作業模式的屬性。 不過，資料庫擁有者可隨時變更交易安全性。 依預設，交易安全性的等級會設定為 FULL (同步作業模式)。  
  
 關閉交易安全性會將工作階段轉換為非同步作業模式，可達到最大效能。 如果主體無法使用，鏡像就會停止，但可以當做暖待命伺服器使用 (容錯移轉需要強制服務，且可能遺失資料)。  
  
### <a name="to-turn-on-transaction-safety"></a>若要開啟交易安全性  
  
1.  連接到主體伺服器。  
  
2.  發出下列 Transact-SQL 陳述式：  
  
    ```  
    ALTER DATABASE <database> SET PARTNER SAFETY FULL  
    ```  
  
     其中 *\<database>* 是鏡像資料庫的名稱。  
  
### <a name="to-turn-off-transaction-safety"></a>關閉交易安全性  
  
1.  連接到主體伺服器。  
  
2.  發出下列陳述式：  
  
    ```  
    ALTER DATABASE <database> SET PARTNER SAFETY OFF  
    ```  
  
     其中 *\<database>* 是鏡像資料庫。  
  
## <a name="see-also"></a>另請參閱  
 [ALTER DATABASE 資料庫鏡像 &#40;Transact-sql&#41;](/sql/t-sql/statements/alter-database-transact-sql-database-mirroring)   
 [Database Mirroring Operating Modes](database-mirroring-operating-modes.md)  
  
  
