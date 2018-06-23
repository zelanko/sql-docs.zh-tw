---
title: 指定合併訂閱類型和衝突解決優先權 (SQL Server Management Studio) |Microsoft 文件
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- replication
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- merge replication conflict resolution [SQL Server replication], merge subscription resolvers
- conflict resolution [SQL Server replication], merge replication
ms.assetid: 2b828d83-2341-4924-b92a-4f81a22246c0
caps.latest.revision: 33
author: craigg-msft
ms.author: craigg
manager: jhubbard
ms.openlocfilehash: de41a4bf6075a816b751574b5505e324d07aa89f
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36036771"
---
# <a name="specify-a-merge-subscription-type-and-conflict-resolution-priority-sql-server-management-studio"></a>指定合併訂閱類型和衝突解決優先權 (SQL Server Management Studio)
  在「新增訂閱精靈」的 **[訂閱類型]** 頁面中指定合併訂閱類型和衝突解決優先權。 如需使用此精靈的詳細資訊，請參閱＜ [Create a Pull Subscription](create-a-pull-subscription.md) ＞和＜ [Create a Push Subscription](create-a-push-subscription.md)＞。  
  
 訂閱建立後便無法修改其類型，但可以在 [訂閱屬性 - \<發行者>: \<發行集資料庫>] 對話方塊中修改伺服器訂閱類型的優先權。 如需有關存取這個對話方塊的詳細資訊，請參閱＜ [View and Modify Push Subscription Properties](view-and-modify-push-subscription-properties.md) ＞與＜ [View and Modify Pull Subscription Properties](view-and-modify-pull-subscription-properties.md)＞。  
  
### <a name="to-specify-a-merge-subscription-type-and-conflict-resolution-priority"></a>若要指定合併訂閱類型與衝突解決優先權  
  
1.  在「新增訂閱精靈」的 **[訂閱類型]** 頁面上，為 **[訂閱類型]** 選項選取 **[用戶端]** 或 **[伺服器]** 。  
  
2.  如果您選取了 **[伺服器]** 訂閱類型，請同時輸入 **[衝突解決優先權]** 選項的值 (0.00 到 99.99)。  
  
### <a name="to-modify-the-conflict-resolution-priority"></a>若要修改衝突解決優先權  
  
1.  在發行者端的 [訂閱屬性 - \<發行者>: \<發行集資料庫>] 中輸入 [優先權] 選項的值 (0.00 到 99.99)。  
  
2.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
## <a name="see-also"></a>另請參閱  
 [進階合併式複寫衝突偵測與解決](merge/advanced-merge-replication-conflict-detection-and-resolution.md)   
 [訂閱發行集](subscribe-to-publications.md)  
  
  