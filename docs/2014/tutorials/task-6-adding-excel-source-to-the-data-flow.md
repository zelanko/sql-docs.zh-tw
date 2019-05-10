---
title: 工作 6：將 Excel 來源加入至資料流程 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: data-quality-services
ms.topic: conceptual
ms.assetid: 0209055e-cb6b-4a07-909e-836596727a2c
author: lrtoyou1223
ms.author: lle
manager: craigg
ms.openlocfilehash: e31b673d7bb80a74cccd664f1e29b72dcd49f4a8
ms.sourcegitcommit: 5748d710960a1e3b8bb003d561ff7ceb56202ddb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/09/2019
ms.locfileid: "65489326"
---
# <a name="task-6-adding-excel-source-to-the-data-flow"></a>工作 6：將 Excel 來源新增至資料流程
  在這項工作中，您會將 Excel 來源加入至資料流程，以便從來源 Excel 檔案讀取供應商資料。 Excel 來源會從 Microsoft Excel 活頁簿中的工作表或範圍擷取資料。 請參閱[Excel 來源](../integration-services/data-flow/excel-source.md)如需詳細資訊。  
  
1.  拖放**Excel 來源**從**其他來源**中**SSIS 工具箱**至**資料流程** 索引標籤。  
  
2.  以滑鼠右鍵按一下**Excel 來源**中**資料流程**索引標籤，然後按一下**重新命名**。  
  
3.  型別**從 Excel 檔案讀取供應商資料**然後按**ENTER**。  
  
4.  按兩下**從 Excel 檔案讀取供應商資料**來啟動**Excel 來源編輯器** 對話方塊。  
  
5.  在 [ **Excel 來源編輯器**] 對話方塊中，按一下**新增**建立 Excel 連接。  
  
6.  在**Excel 連接管理員** 對話方塊中，按一下**瀏覽**，然後選取**Suppliers.xls**中的檔案**EIM 教學課程**資料夾. 確認**Microsoft Excel 97-2003**中選取**版本的 Excel**方塊，然後按一下**確定**。  
  
     ![Excel 連接管理員對話方塊](../../2014/tutorials/media/et-addingexcelsourcetothedataflow-01.jpg "Excel 連接管理員對話方塊")  
  
7.  在  **Excel 來源編輯器**對話方塊中，選取**IncomingSuppliers$** 中**Excel 工作表名稱**清單方塊。  
  
     ![名稱的 Excel 工作表頁-進貨供應商 $](../../2014/tutorials/media/et-addingexcelsourcetothedataflow-02.jpg "名稱的 Excel 工作表頁-進貨供應商 $")  
  
8.  按一下 **預覽**預覽 Excel 檔案中的資料。  
  
9. 按一下 **[確定]** ，關閉對話方塊。  
  
10. 拖放**DQS 清理**轉換**其他轉換**上**SSIS 工具箱**至**資料流程**索引標籤下**從 Excel 檔案讀取供應商資料**。 DQS 清理轉換會使用 Data Quality Services (DQS)，藉由套用知識庫中核准的規則來更正資料。 這項轉換在執行階段會在 DQS 伺服器上建立 DQS 清理專案。 請參閱[DQS 清理轉換](https://msdn.microsoft.com/library/ee677619.aspx)如需詳細資訊。  
  
## <a name="next-step"></a>下一個步驟  
 [工作 7:將 DQS 清理轉換加入資料流程](../integration-services/data-flow/data-flow.md)  
  
  
