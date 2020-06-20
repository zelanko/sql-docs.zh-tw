---
title: 工作10：設定複合定義域使用參考資料服務 |Microsoft Docs
ms.custom: ''
ms.date: 04/27/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: data-quality-services
ms.topic: conceptual
ms.assetid: 752eefde-8b87-4f54-878e-9963ccbadc8e
author: lrtoyou1223
ms.author: lle
ms.openlocfilehash: dd1727ffaa24edf12ed7ad8a5fb4f55f4910855e
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/18/2020
ms.locfileid: "85064820"
---
# <a name="task-10-configuring-composite-domain-to-use-reference-data-service"></a>工作 10：設定複合定義域使用參考資料服務
  在這項工作中，您會設定**位址驗證**複合定義域，以使用**Melissa 的資料位址檢查**服務。 在執行階段的清理活動期間，DQS 會將地址驗證定義域中的定義域值傳遞給服務以進行清理。 如需詳細資訊，請參閱[將定義域/複合定義域對應至參考資料](https://msdn.microsoft.com/library/hh213030.aspx)。  
  
1.  在**DQS 用戶端**的主頁面中，按一下 [**最近使用的知識庫**] 底下的 [**供應商（定義域管理）** ]，啟動 [**定義域管理**] 頁面。  
  
2.  在**定義域清單**中選取 [**位址驗證**] 複合定義域。  
  
3.  在右窗格中，切換至 [**參考資料**] 索引標籤。  
  
     ![[參考資料] 索引標籤](../../2014/tutorials/media/et-configuringcdtouserds-01.jpg "[參考資料] 索引標籤")  
  
4.  按一下工具列上的 **[流覽]** 按鈕。  
  
5.  在 [**線上參考資料提供者目錄**] 對話方塊中，選取 [ **Melissa 資料-位址檢查**] 旁的**核取方塊**。  
  
     ![選取 [Melissa Data – 地址檢查]](../../2014/tutorials/media/et-configuringcdtouserds-02.jpg "選取 [Melissa Data – 地址檢查]")  
  
6.  在右窗格的 [**架構**] 區段中，使用下拉式清單將 [**位址行**] 定義域對應至 [**位址行（M）** ] 架構專案。  
  
     ![將 RDS 結構描述項目對應至定義域](../../2014/tutorials/media/et-configuringcdtouserds-03.jpg "將 RDS 結構描述項目對應至定義域")  
  
7.  按一下工具列上的 **[加入架構專案] （+）** 按鈕，在清單中建立專案。  
  
     ![[加入架構專案] 工具列按鈕](../../2014/tutorials/media/et-configuringcdtouserds-04.jpg "[加入架構專案] 工具列按鈕")  
  
8.  使用下拉式清單對應以下 DQS 定義域，如下圖所示。  
  
     ![將 RDS 結構描述項目對應至定義域](../../2014/tutorials/media/et-configuringcdtouserds-05.jpg "將 RDS 結構描述項目對應至定義域")  
  
9. 按一下 [確定]  關閉對話方塊。  
  
## <a name="next-step"></a>後續步驟  
 [工作 11：發行知識庫](../../2014/tutorials/task-11-publishing-the-knowledge-base.md)  
  
  
