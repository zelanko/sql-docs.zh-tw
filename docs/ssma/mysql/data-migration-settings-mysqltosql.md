---
title: "資料移轉設定 (MySQLToSQL) |Microsoft 文件"
ms.prod: sql-non-specified
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: 
ms.technology:
- sql-ssma
ms.tgt_pltfrm: 
ms.topic: article
applies_to:
- Azure SQL Database
- SQL Server
ms.assetid: 9c396df4-5676-4f32-9c57-70d4f15f9b7a
caps.latest.revision: 9
author: Shamikg
ms.author: Shamikg
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 0b832a9306244210e693bde7c476269455e9b6d8
ms.openlocfilehash: 86d7e6160ab17ecb7a12beb058d33172705342a8
ms.contentlocale: zh-tw
ms.lasthandoff: 10/25/2017

---
# <a name="data-migration-settings-mysqltosql"></a>資料移轉設定 (MySQLToSQL)
  
## <a name="data-migration-settings"></a>資料移轉設定  
**資料移轉設定**可讓使用者撰寫自訂查詢的資料移轉。  
  
-   此索引標籤時，才能使用**擴充資料移轉選項**設**顯示**和時的設定設定為隱藏**隱藏**專案設定中。 如需專案移轉設定的詳細資訊，請參閱[（移轉） 的專案設定](http://msdn.microsoft.com/en-us/2a3cba9e-cd54-4a8b-b858-8fc4cf2580d9)。  
  
-   自訂 SQL 陳述式剖析實作**資料移轉設定**資料表節點 索引標籤。  
  
-   以下是兩個核取方塊中提供**資料移轉設定**viz。:  
  
    1.  截斷 SQL Server 資料表  
  
    2.  選取 使用自訂  
  
1.  **截斷 SQL Server 資料表：**  
     此選項可讓使用者在目標資料庫有清楚的移轉的資料檢視。  
  
    -   根據預設，會檢查此文字方塊。  
  
    -   如果未選取此文字方塊中，移轉的資料會加入至位於目標資料庫的現有資料。  
  
2.  **選取 使用自訂：**  
     此選項可讓使用者修改**選取**出現的陳述式 (**選取**陳述式可讓使用者選取要顯示在目標資料庫的資料)。  
  
    1.  根據預設，這個文字方塊中未核取。  
  
    2.  如果勾選此文字方塊，則它可讓使用者修改**選取**陳述式存在。  
  
有兩個按鈕出現的 viz。:  
  
-   **套用：**按一下**套用**來套用設定，已變更。  
  
-   **取消：**按一下**取消**進行變更之前，還原目前的設定。  
  
## <a name="see-also"></a>另請參閱  
[將 MySQL 資料移轉至 SQL Server/SQL Azure](http://msdn.microsoft.com/en-us/a6a7f4d6-68aa-4a38-93bf-53eba0d7dc82)  
  

