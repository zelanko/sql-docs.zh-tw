---
title: HOST_NAME 值 | Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
f1_keywords:
- sql12.rep.newsubwizard.hostnamevalue.f1
ms.assetid: 21548f08-2910-4a55-baac-b911ba9afaf1
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 4f8f7f1304b0d72cf59467aee16c04481fbd51ad
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "62721195"
---
# <a name="hostname-values"></a>HOST_NAME 值
  具有參數化篩選的合併式發行集，會使用 SUSER_SNAME() 函數及/或 HOST_NAME() 函數來篩選資料。 函數是在新增發行集精靈或 **[發行集屬性]** 對話方塊中指定。  
  
 依預設，HOST_NAME() 函數會傳回連接到發行者的電腦名稱。 使用參數化篩選時，通常會在精靈的這個頁面上提供一個值，來覆寫此值。 HOST_NAME() 函數就會傳回您指定的值，而非電腦的名稱。 如需詳細資訊，請參閱[參數化資料列篩選](merge/parameterized-filters-parameterized-row-filters.md)的＜覆寫 HOST_NAME() 值＞一節。  
  
> [!NOTE]  
>  如果您覆寫 HOST_NAME()，則所有對 HOST_NAME() 函數的呼叫均會傳回您指定的值。 請確定其他應用程式不會相依於由 HOST_NAME() 傳回電腦名稱。  
  
## <a name="options"></a>選項。  
 **訂閱屬性**  
 在 **[HOST_NAME 值]** 資料行中，輸入每一個訂閱者的值，或接受預設值 (訂閱者電腦的名稱)。  
  
## <a name="see-also"></a>另請參閱  
 [建立提取訂閱](create-a-pull-subscription.md)   
 [Create a Push Subscription](create-a-push-subscription.md)   
 [檢視及修改提取訂閱屬性](view-and-modify-pull-subscription-properties.md)   
 [檢視及修改發送訂閱屬性](view-and-modify-push-subscription-properties.md)   
 [HOST_NAME &#40;Transact-SQL&#41;](/sql/t-sql/functions/host-name-transact-sql)   
 [訂閱發行集](subscribe-to-publications.md)  
  
  
