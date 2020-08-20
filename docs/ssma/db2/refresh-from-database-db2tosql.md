---
description: '從資料庫重新整理 (DB2ToSQL) '
title: 從資料庫重新整理 (DB2ToSQL) |Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: 613a8368-b372-443f-8252-fb6dc31a003d
author: nahk-ivanov
ms.author: alexiva
ms.openlocfilehash: 973f3aae444b27be93b675d16c9b9a73d8fac518
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88463475"
---
# <a name="refresh-from-database-db2tosql"></a>從資料庫重新整理 (DB2ToSQL) 
[ **從資料庫** 重新整理] 對話方塊可讓您從 DB2 資料庫中選取要重新整理的物件。 對話方塊中的資料列會根據中繼資料的狀態進行色彩編碼：  
  
-   如果物件中繼資料在本機和 DB2 資料庫中有變更，資料列就會是藍色。  
  
-   如果在 DB2 資料庫中的物件中繼資料已變更，但 SSMA 中沒有變更，則資料列為黃色。  
  
-   如果物件中繼資料已在本機變更，而不是在 DB2 資料庫中變更，則資料列會是綠色。  
  
-   如果物件在 DB2 資料庫中是新的，資料列就是粉紅色。  
  
您可以在 [ **專案設定** ] 對話方塊中指定預設的物件重新整理設定。 如需詳細資訊，請參閱 [&#40;同步處理的專案設定&#41; &#40;DB2ToSQL&#41;](../../ssma/db2/project-settings-synchronization-db2tosql.md)。  
  
若要存取 [ **從資料庫** 重新整理] 對話方塊，請以滑鼠右鍵按一下 DB2 Metadata Explorer 中的物件，然後按一下 [ **從資料庫**重新整理]。  
  
## <a name="options"></a>選項。  
**折迭 (-) **  
折迭所有物件群組以隱藏個別物件。  
  
**展開 (+) **  
展開 [所有物件群組] 以顯示個別物件。  
  
**隱藏/顯示相等的物件**  
如果在 DB2 資料庫和 SSMA 中的物件中繼資料相同，則隱藏清單中的物件。  
  
**從資料庫重新整理 (箭號按鈕) **  
使用箭號按鈕來指定應在 SSMA 中更新所選物件的中繼資料。  
  
**不要從資料庫 (X 按鈕重新整理) **  
使用 [X] 按鈕來指定不應該在 SSMA 中更新所選物件的中繼資料。  
  
**圖例**  
顯示 [ **圖例** ] 對話方塊。 圖例包含資料列色彩和中繼資料狀態之間的對應。  
  
若要將 [ **圖例** ] 對話方塊保留在 [ **從資料庫** 重新整理] 對話方塊的上方，請選取 [ **在上方顯示** ] 核取方塊。  
  
