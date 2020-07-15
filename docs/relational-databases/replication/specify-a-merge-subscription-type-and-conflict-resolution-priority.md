---
title: 指定類型與衝突解決優先權 (合併式)
description: 了解如何指定適用於 SQL Server 的合併訂閱使用之類型和衝突解決原則。
ms.custom: seo-lt-2019
ms.date: 03/07/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- merge replication conflict resolution [SQL Server replication], merge subscription resolvers
- conflict resolution [SQL Server replication], merge replication
ms.assetid: 2b828d83-2341-4924-b92a-4f81a22246c0
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 2981f84bd2cbf6c813a4adf761ddd271c8b68fd1
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/01/2020
ms.locfileid: "85737053"
---
# <a name="specify-a-merge-subscription-type-and-conflict-resolution-priority"></a>指定合併訂閱類型和衝突解決方法優先權
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  在「新增訂閱精靈」的 **[訂閱類型]** 頁面中指定合併訂閱類型和衝突解決優先權。 如需使用此精靈的詳細資訊，請參閱＜ [Create a Pull Subscription](../../relational-databases/replication/create-a-pull-subscription.md) ＞和＜ [Create a Push Subscription](../../relational-databases/replication/create-a-push-subscription.md)＞。  
  
 訂閱建立後即無法修改其類型，但可在 [訂閱屬性 - \<Publisher> \<PublicationDatabase>] 對話方塊中修改伺服器訂閱類型的優先權。 如需有關存取這個對話方塊的詳細資訊，請參閱＜ [View and Modify Push Subscription Properties](../../relational-databases/replication/view-and-modify-push-subscription-properties.md) ＞與＜ [View and Modify Pull Subscription Properties](../../relational-databases/replication/view-and-modify-pull-subscription-properties.md)＞。  
  
### <a name="to-specify-a-merge-subscription-type-and-conflict-resolution-priority"></a>若要指定合併訂閱類型與衝突解決優先權  
  
1.  在「新增訂閱精靈」的 **[訂閱類型]** 頁面上，為 **[訂閱類型]** 選項選取 **[用戶端]** 或 **[伺服器]** 。  
  
2.  如果您選取了 **[伺服器]** 訂閱類型，請同時輸入 **[衝突解決優先權]** 選項的值 (0.00 到 99.99)。  
  
### <a name="to-modify-the-conflict-resolution-priority"></a>若要修改衝突解決優先權  
  
1.  在發行者端的 [訂閱屬性 - \<Publisher> \<PublicationDatabase>] 中，輸入 [優先權] 選項的值 (0.00 到 99.99)。  
  
2.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
## <a name="see-also"></a>另請參閱  
 [進階合併式複寫衝突偵測與解決](../../relational-databases/replication/merge/advanced-merge-replication-conflict-detection-and-resolution.md)   
 [訂閱發行集](../../relational-databases/replication/subscribe-to-publications.md)  
  
  
