---
title: 工作 10： 加入模糊群組轉換來識別重複項目 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- data-quality-services
- integration-services
- master-data-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 90b2b323-babd-464a-8914-9dc5e66aca74
caps.latest.revision: 6
author: douglaslms
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 843d79da1d5e9aba58a80ea93ee36a68cd689916
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/02/2018
ms.locfileid: "37312748"
---
# <a name="task-10-adding-fuzzy-group-transform-to-identify-duplicates"></a>工作 10：加入模糊群組轉換來識別重複項
  在這項工作中，您會將模糊群組轉換加入至資料流程。 模糊群組轉換有助於識別來源資料中的重複項。 請參閱[Fuzzy Grouping Transformation](http://msdn.microsoft.com/library/ms141764.aspx)如需詳細資訊。  
  
1.  拖放**模糊群組**轉換**其他轉換**上**SSIS 工具箱**至**資料流程**索引標籤下**結合正確與更正的記錄**。  
  
2.  以滑鼠右鍵按一下**模糊群組**轉換**資料流程**索引標籤，然後按一下**重新命名**。 型別**分組具有相符識別碼的供應商**然後按**ENTER**。  
  
3.  連接**結合正確和已更正的記錄**要**分組具有相符識別碼的供應商**使用藍色連接器。  
  
     ![連接至 分組具有相符識別碼的供應商](../../2014/tutorials/media/et-addingfgttoidentifyduplicates-01.jpg "分組具有相符識別碼的供應商的連線")  
  
4.  按兩下**分組具有相符識別碼的供應商**。  
  
5.  在 [**模糊群組轉換編輯器**，按一下**新增**旁**OLE DB 連接管理員下拉式清單**以啟動**設定 OLE DB 連接管理員**] 對話方塊。  
  
6.  在對話方塊中，按一下**的新**來啟動**連線管理員** 對話方塊。  
  
7.  型別 **(local)** 或是**期間**（.） 做為伺服器名稱。  
  
8.  選取  **MDS** for**選取或輸入資料庫名稱**欄位。 要做為 MDS 資料庫的暫存儲存體**模糊群組轉換**。 **模糊群組**轉換需要連接到要建立轉換演算法執行其工作所需的暫存 SQL Server 資料表的 SQL Server 執行個體。 您可以建立資料庫，或使用另一個現有的資料庫供此用途使用。  
  
9. 按一下 **測試連接**來測試連線，然後按一下**確定**訊息方塊上。  
  
10. 在 [**連接管理員**] 對話方塊中，按一下**確定**。  
  
11. 選取 **(local)。MDS** (或**localhost。MDS**) 從**清單中的資料連線**然後按一下 **[確定]**。  
  
12. 在 **模糊群組轉換編輯器**，確認 **(local)。MDS**或**localhost。MDS**已選取**OLE DB 連接管理員**。  
  
13. 若要切換**資料行** 索引標籤。  
  
14. 選取 （核取方塊） **SupplierID_Output**從清單中的**可用的輸入資料行**。 若要設定轉換，請選取在識別重複項時所要使用的輸入資料行。 為了維持單純化，您在此步驟中只會使用 SupplierID。  
  
     ![模糊群組轉換編輯器](../../2014/tutorials/media/et-addingfgttoidentifyduplicates-02.jpg "模糊群組轉換編輯器")  
  
15. 按一下  **確定**以關閉**模糊群組轉換編輯器**。  
  
## <a name="next-step"></a>下一個步驟  
 [工作 11：新增條件式分割轉換來篩選重複項](../../2014/tutorials/task-11-adding-conditional-split-transform-to-filter-duplicates.md)  
  
  
