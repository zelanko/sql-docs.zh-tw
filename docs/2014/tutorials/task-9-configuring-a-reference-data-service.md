---
title: 工作 9： 設定參考資料服務 |Microsoft 文件
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
ms.topic: article
ms.assetid: d0535fce-2bf5-4f6d-b517-ffe6fa13738d
caps.latest.revision: 7
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.openlocfilehash: 5a08d3848ddaf65b9e10b654f55e8a0a4d9be690
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36147219"
---
# <a name="task-9-configuring-a-reference-data-service"></a>工作 9：設定參考資料服務
  在這項工作中，您會設定 DQS 使用 Windows Azure Marketplace 上的參考資料服務。 在下一個工作中，您將設定**地址驗證**使用此服務的網域。 在執行階段，清理活動期間，DQS 將值傳遞中的網域**地址驗證**網域服務以進行清理。 請參閱[設定 DQS 使用參考資料](http://msdn.microsoft.com/library/hh213070.aspx)如需詳細資訊。  
  
1.  中的主頁面**DQS 用戶端**，請在**管理**] 窗格中，按一下 [**組態**。  
  
2.  請確認**參考資料**為作用中狀態。  
  
3.  在**網路設定**區域中，輸入適當的值在**Proxy 伺服器**和**連接埠**欄位，如果您需要使用 proxy 伺服器連線到網際網路。  
  
4.  型別您**Windows Azure Marketplace 帳戶金鑰**如**DataMarket 帳戶識別碼**欄位。  
  
     ![Azure 資料市場參考資料服務帳戶](../../2014/tutorials/media/et-configuringareferencedataservice.jpg "Azure 資料市場參考資料服務帳戶")  
  
5.  按一下**驗證**按鈕的文字方塊中，以驗證帳戶識別碼。  
  
6.  按一下**確定**訊息方塊上。  
  
7.  按一下**關閉**来切換到 DQS 用戶端主頁面之頁面的底部。  
  
## <a name="next-task"></a>下一項工作  
 [工作 10： 設定複合定義域使用參考資料服務](../../2014/tutorials/task-10-configuring-composite-domain-to-use-reference-data-service.md)  
  
  