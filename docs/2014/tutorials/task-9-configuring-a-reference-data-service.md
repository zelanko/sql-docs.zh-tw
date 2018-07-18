---
title: 工作 9： 設定參考資料服務 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- data-quality-services
- integration-services
- master-data-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: d0535fce-2bf5-4f6d-b517-ffe6fa13738d
caps.latest.revision: 7
author: douglaslms
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 3a743fd3fe576296a67072762cdfa3a186584cd0
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/02/2018
ms.locfileid: "37326854"
---
# <a name="task-9-configuring-a-reference-data-service"></a>工作 9：設定參考資料服務
  在這項工作中，您會設定 DQS 使用 Windows Azure Marketplace 上的參考資料服務。 在下一個工作中，您會設定**地址驗證**網域以使用這項服務。 在執行階段，清理活動期間，DQS 會將值傳遞中的網域**地址驗證**網域服務以進行清理。 請參閱[設定 DQS 使用參考資料](http://msdn.microsoft.com/library/hh213070.aspx)如需詳細資訊。  
  
1.  中的主頁面**DQS 用戶端**，請在**管理**窗格中，按一下  **Configuration**。  
  
2.  請確認**參考資料** 索引標籤為作用中。  
  
3.  在**網路設定**區域中，輸入適當的值，在**Proxy 伺服器**並**連接埠**欄位，如果您需要使用 proxy 伺服器連線到網際網路。  
  
4.  輸入您**Windows Azure Marketplace 帳戶金鑰**for **DataMarket 帳戶識別碼**欄位。  
  
     ![Azure Data Market 參考資料服務帳戶](../../2014/tutorials/media/et-configuringareferencedataservice.jpg "Azure Data Market 參考資料服務帳戶")  
  
5.  按一下 **驗證**按鈕的文字方塊中，以驗證帳戶識別碼。  
  
6.  按一下 **確定**訊息方塊上。  
  
7.  按一下 **關閉**底部的頁面，即可切換到 DQS 用戶端的主頁面。  
  
## <a name="next-task"></a>下一項工作  
 [工作 10：設定複合定義域以使用參考資料服務](../../2014/tutorials/task-10-configuring-composite-domain-to-use-reference-data-service.md)  
  
  
