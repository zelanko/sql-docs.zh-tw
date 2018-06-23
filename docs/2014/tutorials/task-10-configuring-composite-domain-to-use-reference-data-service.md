---
title: 工作 10： 設定複合定義域使用參考資料服務 |Microsoft 文件
ms.custom: ''
ms.date: 04/27/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- data-quality-services
- integration-services
- master-data-services
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 752eefde-8b87-4f54-878e-9963ccbadc8e
caps.latest.revision: 8
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.openlocfilehash: 2a5d37578ac8336b67201161ef4de59baf90649c
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36032447"
---
# <a name="task-10-configuring-composite-domain-to-use-reference-data-service"></a>工作 10：設定複合定義域使用參考資料服務
  在這個工作中，您會設定**地址驗證**複合定義域使用**Melissa Data – Address Check**服務。 在執行階段的清理活動期間，DQS 會將地址驗證定義域中的定義域值傳遞給服務以進行清理。 請參閱[將定義域/複合定義域對應至參考資料](http://msdn.microsoft.com/library/hh213030.aspx)如需詳細資訊。  
  
1.  中的主頁面**DQS 用戶端**，按一下  **Suppliers （定義域管理）** 下**最近使用的知識庫**啟動**定義域管理**頁面。  
  
2.  選取**地址驗證**複合定義域中的**的網域清單**。  
  
3.  在右窗格中，切換至**參考資料** 索引標籤。  
  
     ![參考資料 索引標籤](../../2014/tutorials/media/et-configuringcdtouserds-01.jpg "參考資料 索引標籤")  
  
4.  按一下**瀏覽**工具列上的按鈕。  
  
5.  在**線上參考資料提供者目錄**對話方塊中，選取**核取方塊**旁**Melissa Data – Address Check**。  
  
     ![選取 [Melissa Data – 地址檢查]](../../2014/tutorials/media/et-configuringcdtouserds-02.jpg "選取 Melissa Data – 地址檢查")  
  
6.  在右窗格中，在**結構描述**區段中，對應**Address Line**網域**地址行 (M)** 結構描述項目，使用下拉式清單。  
  
     ![將 RDS 結構描述項目對應到定義域](../../2014/tutorials/media/et-configuringcdtouserds-03.jpg "將 RDS 結構描述項目對應到定義域")  
  
7.  按一下**新增結構描述項目 （+）** 清單中建立項目工具列上的按鈕。  
  
     ![將結構描述項目工具列按鈕加入](../../2014/tutorials/media/et-configuringcdtouserds-04.jpg "新增結構描述項目工具列按鈕")  
  
8.  使用下拉式清單對應以下 DQS 定義域，如下圖所示。  
  
     ![將 RDS 結構描述項目對應至定義域](../../2014/tutorials/media/et-configuringcdtouserds-05.jpg "將 RDS 結構描述項目對應至定義域")  
  
9. 按一下 **[確定]** ，關閉對話方塊。  
  
## <a name="next-step"></a>下一個步驟  
 [工作 11： 發行知識庫](../../2014/tutorials/task-11-publishing-the-knowledge-base.md)  
  
  