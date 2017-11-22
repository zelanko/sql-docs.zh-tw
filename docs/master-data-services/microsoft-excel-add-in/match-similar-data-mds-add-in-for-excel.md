---
title: "比對相似資料 (適用於 Excel 的 MDS 增益集) | Microsoft Docs"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-non-specified
ms.prod_service: mds
ms.service: 
ms.component: microsoft-excel-add-in
ms.reviewer: 
ms.suite: sql
ms.technology: master-data-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: f6fd6fc1-3569-42a5-b6cb-87a921c88f3b
caps.latest.revision: "6"
author: smartysanthosh
ms.author: nagavo
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 02a15af6cbb80c11dbeb0bf5d2d359eaeab910c9
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/20/2017
---
# <a name="match-similar-data-mds-add-in-for-excel"></a>比對相似資料 (適用於 Excel 的 MDS 增益集)
  在 [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)][!INCLUDE[ssMDSXLS](../../includes/ssmdsxls-md.md)]中，使用 Data Quality Services (DQS) 功能來尋找資料中的相似度。  
  
 若要執行此程序，您可以：  
  
-   使用預設 Data Quality Services 知識庫。  
  
-   建立您自己的自訂 DQS 知識庫和比對原則。 如需相關資訊，請參閱 [Create a Matching Policy](../../data-quality-services/create-a-matching-policy.md)。  
  
## <a name="prerequisites"></a>必要條件  
  
-   您必須擁有包含 MDS 管理之資料的工作表。 如需詳細資訊，請參閱 [Export Data to Excel from Master Data Services](../../master-data-services/microsoft-excel-add-in/export-data-to-excel-from-master-data-services.md)(將資料從 Master Data Services 匯入 Excel)。  
  
-   選擇性。 檢查相似度之前，您可以將其他資料與 MDS 管理的資料結合。 如需詳細資訊，請參閱[結合資料 &#40;適用於 Excel 的 MDS 增益集&#41;](../../master-data-services/microsoft-excel-add-in/combine-data-mds-add-in-for-excel.md)。  
  
### <a name="to-find-similarities-by-using-the-default-knowledge-base"></a>若要使用預設知識庫尋找相似度  
  
1.  從包含 MDS 管理之資料的工作表中，按一下 [資料品質] 群組中的 [比對資料]。  
  
2.  在 [比對資料] 對話方塊中，從 [DQS 知識庫] 清單中選取 [DQS 資料 (預設值)]。  
  
3.  為包含要比對之資料的每個資料行，在對話方塊中加入一個資料列。 如需此對話方塊中的欄位資訊，請參閱[如何設定比對規則參數](../../data-quality-services/create-a-matching-policy.md#MatchingRules)。  
  
4.  當所有加權值的總和等於 100% 時，按一下 [確定]。  
  
### <a name="to-find-similarities-by-using-a-custom-knowledge-base"></a>若要使用自訂知識庫尋找相似度  
  
1.  從包含 MDS 管理之資料的工作表中，按一下 [資料品質] 群組中的 [比對資料]。  
  
2.  從 [DQS 知識庫] 清單中，選取自訂知識庫的名稱。  
  
3.  為工作表中的每個資料行，選取 DQS 定義域。  
  
4.  當所有 DQS 定義域都對應到工作表中的資料行時，請按一下 [確定]。  
  
## <a name="next-steps"></a>後續步驟  
  
-   檢視其他資訊來判斷哪些資料是相似。 如需詳細資訊，請參閱[資料品質比對資料行 &#40;適用於 Excel 的 MDS 增益集&#41;](../../master-data-services/microsoft-excel-add-in/data-quality-matching-columns-mds-add-in-for-excel.md)。  
  
## <a name="see-also"></a>另請參閱  
 [適用於 Excel 的 MDS 增益集中的資料品質比對](../../master-data-services/microsoft-excel-add-in/data-quality-matching-in-the-mds-add-in-for-excel.md)   
 [資料比對](../../data-quality-services/data-matching.md)  
  
  
