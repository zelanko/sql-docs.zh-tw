---
title: 從資料庫 (MySQLToSQL) 重新整理 |Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: 59a6db8f-2db6-4071-9005-928a7231de92
author: Shamikg
ms.author: Shamikg
ms.openlocfilehash: 5acc3153d7305f404c5fc6a0478b83cc0c98bad6
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/15/2019
ms.locfileid: "68066699"
---
# <a name="refresh-from-database-mysqltosql"></a>從資料庫重新整理 (MySQLToSQL)
**從資料庫重新整理**對話方塊可讓您選取要重新整理從 MySQL 資料庫的物件。 在對話方塊中的資料列的色彩標示根據中繼資料的狀態：  
  
-   如果在本機和 MySQL 資料庫中，已變更物件中繼資料，資料列會變成藍色。  
  
-   如果在 MySQL 資料庫，但不是在 SSMA 中，已變更物件中繼資料，資料列是黃色。  
  
-   如果已在本機變更物件中繼資料，但不是在 MySQL 資料庫，資料列是綠色。  
  
-   如果是新的 MySQL 資料庫中的物件，該資料列是粉紅色。  
  
您可以指定中的預設物件重新整理設定**專案設定** 對話方塊。 如需詳細資訊，請參閱 <<c0> [ 專案設定&#40;同步處理&#41; &#40;MySQLToSQL&#41;</c0>](../../ssma/mysql/project-settings-synchronization-mysqltosql.md)  
  
若要存取**從資料庫重新整理** 對話方塊中，以滑鼠右鍵按一下物件，在 MySQL 中繼資料總管，然後按一下**從資料庫重新整理**。  
  
## <a name="options"></a>選項。  
  
|||  
|-|-|  
|**詞彙**|**[定義]**|  
|**摺疊 （-）**|摺疊所有的物件群組，若要隱藏個別的物件。|  
|**展開 （+）**|展開以顯示個別物件的所有物件群組。|  
|**隱藏/顯示相等的物件**|如果物件中繼資料相同的 MySQL 資料庫中，並在 SSMA 中，會隱藏清單中的物件。|  
|**從資料庫 （箭號按鈕） 重新整理**|指定所選物件的中繼資料，應該更新 SSMA 中使用的箭號按鈕。|  
|**從資料庫中執行 重新整理 (X 按鈕）**|您可以使用 [X] 按鈕，指定不應在 SSMA 中更新所選物件的中繼資料。|  
|**圖例**|顯示**圖例** 對話方塊。 圖例會包含資料列的色彩和中繼資料狀態之間的對應。<br /><br />保留**圖例**對話方塊的上方**從資料庫重新整理**對話方塊中，選取**顯示在最上層**核取方塊。|  
  
