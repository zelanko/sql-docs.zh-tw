---
title: 資料移轉設定 (OracleToSQL) |Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.technology: ssma
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 91f7f558-025d-4f4d-ac2c-aa095e7d1ace
caps.latest.revision: 3
author: Shamikg
ms.author: Shamikg
manager: v-thobro
ms.openlocfilehash: 15a0727397346451e07f85556bd183df35d13796
ms.sourcegitcommit: c7a98ef59b3bc46245b8c3f5643fad85a082debe
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/12/2018
ms.locfileid: "38983330"
---
# <a name="data-migration-settings-oracletosql"></a>資料移轉設定 (OracleToSQL)
  
## <a name="data-migration-settings"></a>資料移轉設定  
**資料移轉設定**可讓使用者撰寫自訂查詢的資料移轉。  
  
-   此索引標籤時可以使用**擴充資料移轉選項**設為**顯示**，並隱藏時設定設為**隱藏**專案設定中。 如需有關移轉的專案設定的詳細資訊，請參閱[專案設定 （移轉）](http://msdn.microsoft.com/fcd6b988-633b-4b2b-9f36-6368b5e86b60) 。  
  
-   剖析的自訂 SQL 陳述式將會實作**資料移轉設定**資料表節點 索引標籤。  
  
-   以下是用於兩個核取方塊**資料移轉設定**上來。:  
  
    1.  截斷 SQL Server 資料表  
  
    2.  選取 使用自訂  
  
1.  **截斷 SQL Server 資料表：**  
     此選項可讓使用者在目標資料庫有清楚的移轉的資料檢視。  
  
    -   根據預設，會檢查此文字方塊中。  
  
    -   如果未選取此文字方塊中，已移轉的資料將會新增到目標資料庫的現有資料。  
  
2.  **選取 使用自訂：**  
     此選項可讓使用者修改**選取 **存在的陳述式 (**選取**陳述式可讓使用者選取要顯示在目標資料庫的資料)。  
  
    1.  根據預設，這個文字方塊未核取。  
  
    2.  如果勾選此文字方塊，則它可讓使用者修改**選取**出現的陳述式。  
  
有兩個按鈕出現的閱聽。:  
  
-   **套用：** 按一下 **套用**套用已變更的設定。  
  
-   **取消：** 按一下 **取消**還原出現設定進行變更之前。  
  
## <a name="see-also"></a>另請參閱  
[將 Oracle 資料移轉至 SQL Server](http://msdn.microsoft.com/e23c5268-41ed-4e55-9fe7-a11376202a13)  
  
