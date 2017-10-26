---
title: "固定與變更屬性選項 (緩時變維度精靈 |Microsoft 文件"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.dts.loaddimwizard.attriboption.f1
ms.assetid: c841345c-7d03-452f-9379-1c8c464f029c
caps.latest.revision: 29
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: e248bb1fc4e5f4d638f1cbd417cc243c59bbd5d4
ms.contentlocale: zh-tw
ms.lasthandoff: 09/28/2017

---
# <a name="fixed-and-changing-attribute-options-slowly-changing-dimension-wizard"></a>固定與變更屬性選項 (緩時變維度精靈)
  使用 **[固定與變更屬性選項]** 對話方塊，來指定如何回應固定與變更屬性中的變更。  
  
 若要深入了解這個精靈，請參閱＜ [Slowly Changing Dimension Transformation](../../../integration-services/data-flow/transformations/slowly-changing-dimension-transformation.md)＞。  
  
## <a name="options"></a>選項。  
 **固定屬性**  
 針對固定的屬性，指出在固定屬性中偵測到變更時，工作是否應視為失敗。  
  
 **變更屬性**  
 針對變更的屬性，指出在變更屬性中偵測到變更時，除了目前的記錄外，工作是否還應變更過期或逾時的記錄。 逾時的記錄是由記錄屬性中的變更，以較新的記錄所取代的記錄 (也就是「Type 2」變更)。 選取這個選項，可能會對在關聯式資料倉儲上建構的多維度物件造成其他的處理需求。  
  
## <a name="see-also"></a>另請參閱  
 [使用緩時變維度精靈來設定輸出](../../../integration-services/data-flow/transformations/configure-outputs-using-the-slowly-changing-dimension-wizard.md)  
  
  

