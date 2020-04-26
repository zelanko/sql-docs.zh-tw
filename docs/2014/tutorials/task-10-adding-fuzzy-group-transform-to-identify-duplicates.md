---
title: 工作10：新增模糊群組轉換以識別重複專案 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: data-quality-services
ms.topic: conceptual
ms.assetid: 90b2b323-babd-464a-8914-9dc5e66aca74
author: lrtoyou1223
ms.author: lle
manager: craigg
ms.openlocfilehash: 48e233c6f2c7a55bf2420825b9fb3064db6e89e1
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/26/2020
ms.locfileid: "65481255"
---
# <a name="task-10-adding-fuzzy-group-transform-to-identify-duplicates"></a>工作 10：新增模糊群組轉換來識別重複項
  在這項工作中，您會將模糊群組轉換加入至資料流程。 模糊群組轉換有助於識別來源資料中的重複項。 如需詳細資訊，請參閱[模糊群組轉換](../integration-services/data-flow/transformations/fuzzy-grouping-transformation.md)。  
  
1.  將 [ **SSIS 工具箱**] 的**其他轉換**中的 [**模糊群組**轉換] 拖放到 [**結合正確和更正的記錄**] 底下的 [**資料流程**] 索引標籤。  
  
2.  以滑鼠右鍵**按一下 [資料流程**] 索引標籤中的 [**模糊群組**轉換]，然後按一下 [**重新命名**]。 輸入**群組具有相符識別碼的供應商**，然後按**enter**鍵。  
  
3.  使用藍色連接器，將**正確和已更正的記錄結合**為符合**識別碼的群組供應商**。  
  
     ![連接有相符識別碼的 [供應商] 群組](../../2014/tutorials/media/et-addingfgttoidentifyduplicates-01.jpg "連接有相符識別碼的 [供應商] 群組")  
  
4.  按兩下 [**群組具有相符識別碼的供應商**]。  
  
5.  在 [**模糊群組轉換編輯器**] 中，按一下 [ **OLE DB 連接管理員] 下拉式清單**旁邊的 [**新增**]，以啟動 [**設定 OLE DB 連線管理員**] 對話方塊。  
  
6.  在對話方塊中，按一下 [**新增**] 以啟動 [**連線管理員**] 對話方塊。  
  
7.  在 [伺服器名稱] 中輸入 **（local）** 或**句號**（.）。  
  
8.  針對 [**選取或輸入資料庫名稱**] 欄位選取 [ **MDS** ]。 您將使用 MDS 資料庫做為**模糊群組轉換**的暫存儲存體。 「**模糊群組**」轉換需要連接到 SQL Server 的實例，以建立轉換演算法執行其工作所需的暫存 SQL Server 資料表。 您可以建立資料庫，或使用另一個現有的資料庫供此用途使用。  
  
9. 按一下 [**測試連接**] 來測試連接，然後按一下訊息方塊上的 **[確定]** 。  
  
10. 在 [**連線管理員**] 對話方塊中，按一下 **[確定]**。  
  
11. 選取 **[（本機）]。MDS** （或**localhost。MDS**），從**資料連線清單**中按一下 **[確定]**。  
  
12. 在 [**模糊群組轉換編輯器**] 中，確認 **（本機）。MDS**或**localhost。** 已針對**OLE DB 連線管理員**選取 MDS。  
  
13. 切換至 [資料**行**] 索引標籤。  
  
14. 從**可用輸入資料行**的清單中選取 [（核取方塊）] **SupplierID_Output** 。 若要設定轉換，請選取在識別重複項時所要使用的輸入資料行。 為了維持單純化，您在此步驟中只會使用 SupplierID。  
  
     ![模糊群組轉換編輯器](../../2014/tutorials/media/et-addingfgttoidentifyduplicates-02.jpg "模糊群組轉換編輯器")  
  
15. 按一下 **[確定]** 以關閉 [**模糊群組轉換編輯器**]。  
  
## <a name="next-step"></a>後續步驟  
 [工作 11：新增條件式分割轉換來篩選重複項](../../2014/tutorials/task-11-adding-conditional-split-transform-to-filter-duplicates.md)  
  
  
