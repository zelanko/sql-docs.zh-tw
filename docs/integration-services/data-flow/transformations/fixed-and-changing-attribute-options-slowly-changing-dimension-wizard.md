---
title: 固定與變更屬性選項 (緩時變維度精靈) | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.dts.loaddimwizard.attriboption.f1
ms.assetid: c841345c-7d03-452f-9379-1c8c464f029c
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 3e54fc003f2bb61a5e94f521ddb1a0221261610e
ms.sourcegitcommit: e8af8cfc0bb51f62a4f0fa794c784f1aed006c71
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/26/2019
ms.locfileid: "71291425"
---
# <a name="fixed-and-changing-attribute-options-slowly-changing-dimension-wizard"></a>固定與變更屬性選項 (緩時變維度精靈)

[!INCLUDE[ssis-appliesto](../../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  使用 **[固定與變更屬性選項]** 對話方塊，來指定如何回應固定與變更屬性中的變更。  
  
 若要深入了解這個精靈，請參閱＜ [Slowly Changing Dimension Transformation](../../../integration-services/data-flow/transformations/slowly-changing-dimension-transformation.md)＞。  
  
## <a name="options"></a>選項。  
 **固定屬性**  
 針對固定的屬性，指出在固定屬性中偵測到變更時，工作是否應視為失敗。  
  
 **變更屬性**  
 針對變更的屬性，指出在變更屬性中偵測到變更時，除了目前的記錄外，工作是否還應變更過期或逾時的記錄。 逾時的記錄是由記錄屬性中的變更，以較新的記錄所取代的記錄 (也就是「Type 2」變更)。 選取這個選項，可能會對在關聯式資料倉儲上建構的多維度物件造成其他的處理需求。  
  
## <a name="see-also"></a>另請參閱  
 [使用緩時變維度精靈來設定輸出](../../../integration-services/data-flow/transformations/configure-outputs-using-the-slowly-changing-dimension-wizard.md)  
  
  
