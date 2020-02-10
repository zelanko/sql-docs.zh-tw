---
title: 工作3：建立及執行資料品質專案以進行比對 |Microsoft Docs
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
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "65489235"
---
# <a name="task-3-creating-and-running-a-data-quality-project-for-matching"></a>工作 3：建立及執行資料品質專案以進行比對
  在這項工作中，您會針對比對活動建立資料品質專案，並針對已清理的供應商資料執行比對程序，以移除資料中的任何重複項。  
  
1.  在**DQS 用戶端**的主頁面上，按一下 [**新增資料品質專案**]。  
  
2.  輸入從**專案名稱**中**移除供應商重複**。  
  
3.  從 [**使用知識庫**] 欄位的 kb 清單中選取 [**供應商**]。 在上一課，您已經在此知識庫中建立比對原則。  
  
4.  從右下方的 [**活動] 清單**中選取 [比對]。 ****  
  
     ![新增資料品質專案 - 已選取 [比對]](../../2014/tutorials/media/et-creatingandrunningadqpformatching.jpg "新增資料品質專案 - 已選取 [比對]")  
  
5.  按 [下一步]  。  
  
6.  在 [對應] **** 頁面上，針對 [資料來源] **** 選取 [Excel 檔案] ****。  
  
7.  按一下 **[流覽]** 並選取 [**清理供應商清單 .xls**]，這是清理活動的輸出檔案。  
  
8.  將 [供應商**識別碼**] 欄位、[**供應商名稱**] 資料**行對應至**供應商**名稱**網域，並將 [ **ContactEmailAddress** ] 資料行對應至 [**連絡人電子郵件**網域]  
  
9. 按 **[下一步]** 切換至 [**對應**] 頁面。  
  
10. 按一下 [**啟動**] 開始比對程式。 您應該會看到與上一個工作類似的結果，因為您使用了相同的輸入檔來定義比對原則。  
  
11. 請在清單方塊中檢閱所有相符記錄及其比對分數。 結果應該與您在上一個工作看到的結果相同。 請參閱上一個工作的步驟，以分析這個比對活動的結果。  
  
12. 按 **[下一步]** 切換至 [**匯出**] 頁面。  
  
## <a name="next-step"></a>後續步驟  
 [工作 4：將比對活動的結果匯出到 Excel 檔案](../../2014/tutorials/task-4-exporting-the-results-from-matching-activity-to-an-excel-file.md)  
  
  
