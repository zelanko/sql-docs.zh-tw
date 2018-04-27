---
title: 重新整理從資料庫 (DB2ToSQL) |Microsoft 文件
ms.prod: sql
ms.prod_service: sql-tools
ms.service: ''
ms.component: ssma-db2
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.technology:
- sql-ssma
ms.tgt_pltfrm: ''
ms.topic: article
applies_to:
- Azure SQL Database
- SQL Server
ms.assetid: 613a8368-b372-443f-8252-fb6dc31a003d
caps.latest.revision: 5
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 90e9c214011f4526afa92abbdd275b8dce998b41
ms.sourcegitcommit: a85a46312acf8b5a59a8a900310cf088369c4150
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/26/2018
---
# <a name="refresh-from-database-db2tosql"></a>從資料庫 (DB2ToSQL) 重新整理
**從資料庫重新整理** 對話方塊可讓您選取要重新整理從 DB2 資料庫的物件。 在對話方塊中的資料列會以色彩標示在中繼資料的狀態：  
  
-   如果在本機和 DB2 資料庫中，已變更物件中繼資料，資料列是藍色。  
  
-   如果物件中繼資料已變更，但不是在 SSMA DB2 資料庫內，資料列是黃色。  
  
-   如果已在本機，變更物件中繼資料，但不是在 DB2 資料庫中，將資料列是綠色。  
  
-   如果是新 DB2 資料庫中的物件，該資料列是粉紅色。  
  
您可以指定預設物件中的重新整理設定**專案設定** 對話方塊。 如需詳細資訊，請參閱[專案設定&#40;同步&#41; &#40;DB2ToSQL&#41;](../../ssma/db2/project-settings-synchronization-db2tosql.md)。  
  
若要存取**從資料庫重新整理**對話方塊中，以滑鼠右鍵按一下物件，在 DB2 中繼資料總管 按一下**從資料庫重新整理**。  
  
## <a name="options"></a>選項  
**摺疊 （-）**  
摺疊以隱藏個別物件的所有物件群組。  
  
**展開 （+）**  
展開以顯示個別物件的所有物件群組。  
  
**隱藏/顯示相等的物件**  
如果物件中繼資料相同的 SSMA 和 DB2 資料庫中，會隱藏從清單中的物件。  
  
**重新整理從資料庫 （箭號按鈕）**  
使用箭號按鈕來指定，應該在 SSMA 更新所選物件的中繼資料。  
  
**從資料庫中執行 重新整理 (X 按鈕）**  
若要指定不應在 SSMA 更新所選物件的中繼資料使用 X 按鈕。  
  
**圖例**  
顯示**圖例** 對話方塊。 圖例會包含資料列色彩和中繼資料狀態之間的對應。  
  
要保留**圖例**對話方塊頂端的**從資料庫重新整理**對話方塊中，選取**顯示在最上層**核取方塊。  
  
