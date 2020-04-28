---
title: 從資料庫重新整理（OracleToSQL） |Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: 84492f44-c368-4c75-954d-7307a2d2bbc0
author: Shamikg
ms.author: Shamikg
manager: shamikg
ms.openlocfilehash: ba9a56c5fb47be4db081aebb3753db2c3e9ed6ad
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "68266538"
---
# <a name="refresh-from-database-oracletosql"></a>從資料庫重新整理 (OracleToSQL)
[**從資料庫**重新整理] 對話方塊可讓您選取要從 Oracle 資料庫中重新整理的物件。 對話方塊中的資料列會根據中繼資料的狀態，以色彩標示：  
  
-   如果物件中繼資料在本機和 Oracle 資料庫中已變更，則資料列會是藍色。  
  
-   如果 Oracle 資料庫中的物件中繼資料已變更，而不是在 SSMA 中，則該資料列為黃色。  
  
-   如果物件中繼資料已在本機變更，而不是在 Oracle 資料庫中，則該資料列為綠色。  
  
-   如果物件在 Oracle 資料庫中是新的，則該資料列為粉紅色。  
  
您可以在 [**專案設定**] 對話方塊中指定預設物件重新整理設定。 如需詳細資訊，請參閱[&#40;同步處理&#41; &#40;OracleToSQL&#41;的專案設定](../../ssma/oracle/project-settings-synchronization-oracletosql.md)。  
  
若要存取 [**從資料庫**重新整理] 對話方塊，請以滑鼠右鍵按一下 [Oracle Metadata Explorer] 中的物件，然後按一下 [**從資料庫**重新整理]。  
  
## <a name="options"></a>選項  
**Collapse （-）**  
折迭所有物件群組以隱藏個別物件。  
  
**展開（+）**  
展開 [所有物件群組] 以顯示個別物件。  
  
**隱藏/顯示相等的物件**  
如果 Oracle 資料庫和 SSMA 中的物件中繼資料相同，就隱藏清單中的物件。  
  
**從資料庫重新整理（箭號按鈕）**  
使用箭號按鈕來指定要在 SSMA 中更新所選物件的中繼資料。  
  
**不要從資料庫重新整理（X 按鈕）**  
使用 [X] 按鈕，指定不應在 SSMA 中更新所選物件的中繼資料。  
  
**圖例**  
顯示 [**圖例**] 對話方塊。 圖例包含資料列色彩和中繼資料狀態之間的對應。  
  
若要將 [**圖例**] 對話方塊保留在 [**從資料庫**重新整理] 對話方塊的頂端，請選取 [**在頂端顯示**] 核取方塊。  
  
