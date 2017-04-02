---
title: "變更資料庫鏡像工作階段中的異動安全性 (Transact-SQL) | Microsoft Docs"
ms.custom: ""
ms.date: "03/04/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dbe-high-availability"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "交易安全性 [SQL Server 資料庫鏡像]"
ms.assetid: 8b03bb82-8589-4558-8545-9942fe008391
caps.latest.revision: 38
author: "MikeRayMSFT"
ms.author: "mikeray"
manager: "jhubbard"
caps.handback.revision: 38
---
# 變更資料庫鏡像工作階段中的異動安全性 (Transact-SQL)
  交易安全性是控制工作階段作業模式的屬性。 不過，資料庫擁有者可隨時變更交易安全性。 依預設，交易安全性的等級會設定為 FULL (同步作業模式)。  
  
 關閉交易安全性會將工作階段轉換為非同步作業模式，可達到最大效能。 如果主體無法使用，鏡像就會停止，但可以當做暖待命伺服器使用 (容錯移轉需要強制服務，且可能遺失資料)。  
  
### 若要開啟交易安全性  
  
1.  連接到主體伺服器。  
  
2.  發出下列 Transact-SQL 陳述式：  
  
    ```  
    ALTER DATABASE <database> SET PARTNER SAFETY FULL  
    ```  
  
     其中 \<資料庫> 是鏡像資料庫的名稱。  
  
### 關閉交易安全性  
  
1.  連接到主體伺服器。  
  
2.  發出下列陳述式：  
  
    ```  
    ALTER DATABASE <database> SET PARTNER SAFETY OFF  
    ```  
  
     其中 \<資料庫> 是鏡像資料庫。  
  
## 另請參閱  
 [ALTER DATABASE 資料庫鏡像 &#40;Transact-SQL&#41;](../Topic/ALTER%20DATABASE%20Database%20Mirroring%20\(Transact-SQL\).md)   
 [資料庫鏡像作業模式](../../database-engine/database-mirroring/database-mirroring-operating-modes.md)  
  
  