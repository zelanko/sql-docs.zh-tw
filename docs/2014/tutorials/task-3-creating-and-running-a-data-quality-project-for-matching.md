---
title: 工作 3：建立和執行資料品質專案進行比對 |Microsoft Docs
ms.custom: ''
ms.date: 04/27/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: data-quality-services
ms.topic: conceptual
ms.assetid: 6260e911-ea8b-4c69-a39d-d1bccd565a32
author: lrtoyou1223
ms.author: lle
manager: craigg
ms.openlocfilehash: ca7c735f00f4fa5c7baf102b26edb6634f57b90f
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "65489235"
---
# <a name="task-3-creating-and-running-a-data-quality-project-for-matching"></a>工作 3：建立及執行資料品質專案以進行比對
  在這項工作中，您會針對比對活動建立資料品質專案，並針對已清理的供應商資料執行比對程序，以移除資料中的任何重複項。  
  
1.  在主頁面上**DQS 用戶端**，按一下**新增資料品質專案**。  
  
2.  型別**移除供應商重複項目**從**專案的名稱**。  
  
3.  選取 **供應商**從清單中的知識庫**使用知識庫**欄位。 在上一課，您已經在此知識庫中建立比對原則。  
  
4.  選取 **比對**從**活動的清單**從右下方的窗格。  
  
     ![新增資料品質專案-比對所選](../../2014/tutorials/media/et-creatingandrunningadqpformatching.jpg "新增資料品質專案-比對所選")  
  
5.  按一下 [下一步]  。  
  
6.  在 [對應]  頁面上，針對 [資料來源]  選取 [Excel 檔案]  。  
  
7.  按一下 **瀏覽**，然後選取**Cleansed Supplier List.xls**，這是清理活動的輸出檔案。  
  
8.  地圖**SupplierID**來源資料行**Supplier ID**網域**Supplier Name**資料行**Supplier Name**網域及**ContactEmailAddress**資料行**Contact Email**網域。  
  
9. 按一下 **下一步**轉為**比對**頁面。  
  
10. 按一下 **啟動**啟動比對程序。 您應該會看到與上一個工作類似的結果，因為您使用了相同的輸入檔來定義比對原則。  
  
11. 請在清單方塊中檢閱所有相符記錄及其比對分數。 結果應該與您在上一個工作看到的結果相同。 請參閱上一個工作的步驟，以分析這個比對活動的結果。  
  
12. 按一下 **下一步**轉為**匯出**頁面。  
  
## <a name="next-step"></a>下一個步驟  
 [工作 4：將結果匯出比對活動到 Excel 檔案](../../2014/tutorials/task-4-exporting-the-results-from-matching-activity-to-an-excel-file.md)  
  
  
