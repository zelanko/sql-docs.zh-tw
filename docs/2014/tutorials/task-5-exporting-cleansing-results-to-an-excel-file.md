---
title: 工作5：將清理結果匯出至 Excel 檔案 |Microsoft Docs
ms.custom: ''
ms.date: 04/27/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: data-quality-services
ms.topic: conceptual
ms.assetid: eaeafd65-d0d4-4a7d-a3ad-110ef644e90b
author: lrtoyou1223
ms.author: lle
manager: craigg
ms.openlocfilehash: 3c690becefb71b71c154131b6957c1063872b540
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "65489119"
---
# <a name="task-5-exporting-cleansing-results-to-an-excel-file"></a>工作 5：將清理結果匯出到 Excel 檔案
  在這項工作中，您會將清理活動的結果匯出到 Excel 檔案。 如需詳細資訊，請參閱[匯出階段](https://msdn.microsoft.com/library/hh213061.aspx#Export)主題。  
  
1.  在右窗格中，選取 [ **Excel** ] 作為 [**目的地類型**]。  
  
2.  按一下 **[流覽]**，將輸出檔案名指定為**清理供應商清單 .xls**，然後按一下 [**開啟**]。  
  
3.  僅針對**輸出**格式選取 [**資料**]，只匯出清理的資料。 第二個選項 [**資料和清理資訊**] 可讓您連同清理資料一起匯出清理活動詳細資訊。 [**標準化格式**] 選項可讓您將在網域上定義的任何輸出格式套用至該定義域的值。 在本教學課程中，您尚未在任何定義域定義輸出格式。  
  
     ![[匯出清理結果] 頁面](../../2014/tutorials/media/et-exportingcleansingresultstoanexcelfile.jpg "[匯出清理結果] 頁面")  
  
4.  按一下 [**匯出**] 匯出資料。 請不要按一下 **[完成]** 。  
  
5.  在 [**正在匯出**] 對話方塊上，按一下 [**關閉**]。  
  
6.  按一下 **[完成]** 以完成活動。 如果您在按一下 **[完成]** 之前忘記匯出結果，請在**DQS 用戶端**的主頁面中，按一下 [**開啟資料品質專案**]，從專案清單中選取 [**清理供應商清單**]，然後按一下畫面底部的 **[下一步]** ，再次進入清理程式的 [**匯出**] 階段。 您也可以按一下 [**上一步**] 按鈕，切換到 [**管理和查看結果**] 索引標籤。  
  
7.  開啟**清理供應商清單 .xls** ，然後執行下列動作：  
  
    1.  藉由在工作表中搜尋 adventure-work.com，確保沒有任何以 adventure-work.com 結尾的電子郵件地址（不含字元的 '）。  
  
    2.  查看 [**國家/地區**] 資料行中沒有任何**美國**值。  
  
    3.  搜尋洛杉磯 **，並查看****狀態**設定為 [ **CA**]。  
  
    4.  確認沒有任何「 **Co**」、「 **Corp**」和「 **inc.**」的條款。  
  
    5.  從試算表刪除 [**位址驗證**] 資料行，並儲存 excel 檔案。 此額外資料行對應至「地址驗證」複合定義域。  
  
## <a name="next-step"></a>後續步驟  
 [工作 6：從 Cleanse Supplier List 專案匯入值](../../2014/tutorials/task-6-importing-values-from-the-cleanse-supplier-list-project.md)  
  
  
