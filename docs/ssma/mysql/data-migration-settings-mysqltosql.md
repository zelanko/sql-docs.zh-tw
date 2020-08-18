---
description: 資料移轉設定 (MySQLToSQL)
title: 資料移轉設定 (MySQLToSQL) |Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: 9c396df4-5676-4f32-9c57-70d4f15f9b7a
author: nahk-ivanov
ms.author: alexiva
ms.openlocfilehash: 3dbf44933ae4abe26f5dacfc79bad0d971bfe5ad
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88492442"
---
# <a name="data-migration-settings-mysqltosql"></a>資料移轉設定 (MySQLToSQL)
  
## <a name="data-migration-settings"></a>資料移轉設定  
**資料移轉設定** 可讓使用者撰寫自訂查詢以進行資料移轉。  
  
-   當 [ **擴充資料移轉選項** ] 設定為 [ **顯示** ]，並且在 [專案設定] 中設定為 [ **隱藏** ] 時，就可以使用此索引標籤。 如需有關專案遷移設定的詳細資訊，請參閱 [ (遷移) 的專案設定 ](https://msdn.microsoft.com/2a3cba9e-cd54-4a8b-b858-8fc4cf2580d9) 。  
  
-   將在資料表節點的 [ **資料移轉設定** ] 索引標籤中，執行自訂 SQL 語句的剖析。  
  
-   以下是 [ **資料移轉設定** 視覺效果] 中可用的兩個核取方塊：  
  
    1.  截斷 SQL Server 資料表  
  
    2.  使用自訂選取  
  
1.  **截斷 SQL Server 資料表：**  
     此選項可讓使用者清楚瞭解目標資料庫上已遷移的資料。  
  
    -   預設會選取這個文字方塊。  
  
    -   如果未選取此文字方塊，則會將遷移的資料加入目標資料庫的現有資料。  
  
2.  **使用自訂選取：**  
     此選項可讓使用者修改所顯示的 **select** 語句 (**select** 語句可讓使用者選取要在目標資料庫) 顯示的資料。  
  
    1.  依預設，不會選取這個文字方塊。  
  
    2.  如果選取此文字方塊，則會允許使用者修改現有的 **select** 語句。  
  
有兩個按鈕出現視覺效果。：  
  
-   **適用于：** 按一下 **[** 套用] 以套用已變更的設定。  
  
-   **取消：** 按一下 [ **取消** ]，以在進行變更之前還原存在的設定。  
  
## <a name="see-also"></a>另請參閱  
[將 MySQL 資料移轉至 SQL Server/SQL Azure](https://msdn.microsoft.com/a6a7f4d6-68aa-4a38-93bf-53eba0d7dc82)  
  
