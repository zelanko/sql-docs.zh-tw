---
title: HOST_NAME 值 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
f1_keywords:
- sql13.rep.newsubwizard.hostnamevalue.f1
ms.assetid: 21548f08-2910-4a55-baac-b911ba9afaf1
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 3bcfcf089d8a50f9b94498cc68f12a4d6f0ac97f
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/30/2020
ms.locfileid: "68770618"
---
# <a name="host_name-values"></a>HOST_NAME 值
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

具有參數化篩選的合併式發行集，會使用 SUSER_SNAME() 函數及/或 HOST_NAME() 函數來篩選資料。 函數是在新增發行集精靈或 **[發行集屬性]** 對話方塊中指定。  
  
依預設，HOST_NAME() 函數會傳回連接到發行者的電腦名稱。 使用參數化篩選時，通常會在精靈的這個頁面上提供一個值，來覆寫此值。 HOST_NAME() 函數就會傳回您指定的值，而非電腦的名稱。 如需詳細資訊，請參閱[參數化資料列篩選](../../relational-databases/replication/merge/parameterized-filters-parameterized-row-filters.md)的＜覆寫 HOST_NAME() 值＞一節。  
  
> [!NOTE]  
>  如果您覆寫 HOST_NAME()，則所有對 HOST_NAME() 函數的呼叫均會傳回您指定的值。 請確定其他應用程式不會相依於由 HOST_NAME() 傳回電腦名稱。  
  
## <a name="options"></a>選項。  
 **訂閱屬性**  
 在 **[HOST_NAME 值]** 資料行中，輸入每一個訂閱者的值，或接受預設值 (訂閱者電腦的名稱)。  
  
## <a name="see-also"></a>另請參閱  
 [Create a Pull Subscription](../../relational-databases/replication/create-a-pull-subscription.md)   
 [Create a Push Subscription](../../relational-databases/replication/create-a-push-subscription.md)   
 [檢視及修改提取訂閱屬性](../../relational-databases/replication/view-and-modify-pull-subscription-properties.md)   
 [檢視及修改發送訂閱屬性](../../relational-databases/replication/view-and-modify-push-subscription-properties.md)   
 [HOST_NAME &#40;Transact-SQL&#41;](../../t-sql/functions/host-name-transact-sql.md)   
 [訂閱發行集](../../relational-databases/replication/subscribe-to-publications.md)  
  
  
