---
title: "資料移轉設定 (OracleToSQL) |Microsoft 文件"
ms.prod: sql-non-specified
ms.prod_service: sql-non-specified
ms.service: 
ms.component: ssma-oracle
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.technology: sql-ssma
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 91f7f558-025d-4f4d-ac2c-aa095e7d1ace
caps.latest.revision: "3"
author: Shamikg
ms.author: Shamikg
manager: v-thobro
ms.workload: Inactive
ms.openlocfilehash: 688d9884b63ab1f4343bb3269250f0ab368500e3
ms.sourcegitcommit: b2d8a2d95ffbb6f2f98692d7760cc5523151f99d
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/05/2017
---
# <a name="data-migration-settings-oracletosql"></a>資料移轉設定 (OracleToSQL)
  
## <a name="data-migration-settings"></a>資料移轉設定  
**資料移轉設定**可讓使用者撰寫自訂查詢的資料移轉。  
  
-   此索引標籤時，才能使用**擴充資料移轉選項**設**顯示**和時的設定設定為隱藏**隱藏**專案設定中。 如需專案移轉設定的詳細資訊，請參閱[（移轉） 的專案設定](http://msdn.microsoft.com/en-us/fcd6b988-633b-4b2b-9f36-6368b5e86b60)。  
  
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
  
## <a name="see-also"></a>請參閱  
[Oracle 資料移轉至 SQL Server](http://msdn.microsoft.com/en-us/e23c5268-41ed-4e55-9fe7-a11376202a13)  
  
