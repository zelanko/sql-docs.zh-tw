---
title: 工作9：設定參考資料服務 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: data-quality-services
ms.topic: conceptual
ms.assetid: d0535fce-2bf5-4f6d-b517-ffe6fa13738d
author: lrtoyou1223
ms.author: lle
manager: craigg
ms.openlocfilehash: e4c756463c43ede8c6dae0cda0a184f0ec7f9956
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "70154937"
---
# <a name="task-9-configuring-a-reference-data-service"></a>工作 9：設定參考資料服務
  在這項工作中，您會設定 DQS 在 Azure Marketplace 上使用參考資料服務。 在下一項工作中，您會將**位址驗證**網域設定為使用此服務。 在執行時間，在清理活動期間，DQS 會將**位址驗證**定義域中的定義域值傳遞給服務以進行清理。 如需詳細資訊，請參閱[設定 DQS 使用參考資料](https://msdn.microsoft.com/library/hh213070.aspx)。  
  
1.  在**DQS 用戶端**的主頁面中 **，按一下 [** 系統**管理**] 窗格中的 [設定]。  
  
2.  確定 [**參考資料**] 索引標籤為作用中狀態。  
  
3.  如果您需要使用 proxy 伺服器連線到網際網路，請在 [**網路設定**] 區域中，于 [ **proxy 伺服器**] 和 [**埠**] 欄位中輸入適當的值。  
  
4.  輸入 [ **DataMarket 帳戶識別碼**] 欄位的**Azure Marketplace 帳戶金鑰**。  
  
     ![Azure DataMarket 參考資料服務帳戶](../../2014/tutorials/media/et-configuringareferencedataservice.jpg "Azure DataMarket 參考資料服務帳戶")  
  
5.  按一下文字方塊旁的 [**驗證**] 按鈕，以驗證帳戶識別碼。  
  
6.  在訊息方塊上按一下 **[確定]** 。  
  
7.  按一下頁面底部的 [**關閉**]，切換到 DQS 用戶端的主頁面。  
  
## <a name="next-task"></a>下一項工作  
 [工作 10：設定複合定義域使用參考資料服務](../../2014/tutorials/task-10-configuring-composite-domain-to-use-reference-data-service.md)  
  
  
