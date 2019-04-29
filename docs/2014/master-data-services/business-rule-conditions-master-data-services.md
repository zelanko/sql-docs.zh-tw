---
title: 商務規則條件 (Master Data Services) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
ms.assetid: d2e0a8c3-4c2e-407c-856e-68d95ebda9ed
author: leolimsft
ms.author: lle
manager: craigg
ms.openlocfilehash: d5089921156f97509e157f771dbe20e1c33cf569
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "62925964"
---
# <a name="business-rule-conditions-master-data-services"></a>商務規則條件 (Master Data Services)
  在 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]中，商務規則條件會確定條件必須為 true，才可以採取一個或多個動作。  
  
> [!NOTE]  
>  條件是選擇性的。 如果您未指定條件，則會在根據商務規則驗證資料時採取動作。  
  
## <a name="business-rule-conditions"></a>商務規則條件  
  
|條件名稱|描述|  
|--------------------|-----------------|  
|**等於**|選取的屬性 **等於** 特定的屬性、特定的屬性值或空白。<br /><br /> 此條件適用於文字、數字、日期及連結值。|  
|**不等於**|選取的屬性 **不等於** 特定的屬性、特定的屬性值或空白。<br /><br /> 此條件適用於文字、數字、日期及連結值。|  
|**大於**|選取的屬性 **大於** 特定的屬性、特定的屬性值或空白。<br /><br /> 此條件僅適用於文字、數字及日期值。|  
|**大於或等於**|選取的屬性 **大於或等於** 特定的屬性、特定的屬性值或空白。<br /><br /> 此條件僅適用於文字、數字及日期值。|  
|**小於**|選取的屬性 **小於** 特定的屬性、特定的屬性值或空白。<br /><br /> 此條件僅適用於文字、數字及日期值。|  
|**小於或等於**|選取的屬性 **小於或等於** 特定的屬性、特定的屬性值或空白。<br /><br /> 此條件僅適用於文字、數字及日期值。|  
|**開頭為**|選取的屬性 **開頭為** 特定的屬性、特定的屬性值或空白。<br /><br /> 此條件僅適用於文字及連結值。|  
|**結尾為**|選取的屬性 **結尾為** 特定的屬性、特定的屬性值或空白。<br /><br /> 此條件僅適用於文字及連結值。|  
|**包含**|選取的屬性 **包含** 特定的屬性、特定的屬性值或空白。<br /><br /> 此條件僅適用於文字及連結值。|  
|**包含模式**|選取的屬性 **包含特定屬性、特定屬性值或空白的模式** 。 使用 .NET Framework 規則運算式來指定模式。<br /><br /> 如需有關規則運算式的詳細資訊，請參閱 MSDN Library 中的 [規則運算式語言項目](https://go.microsoft.com/fwlink/?LinkId=164401) 。<br /><br /> 此條件僅適用於文字及連結值。|  
|**包含子集**|選取的屬性 **包含特定屬性或特定屬性值的子集** 。 您必須指定搜尋的起始位置 (例如，1 表示從第一個字元開始搜尋)。<br /><br /> 此條件僅適用於文字及連結值。|  
|**已變更**|選取的屬性自上次商務規則套用到成員之後 **已經變更** 。 您必須指定此屬性所隸屬的變更群組。<br /><br /> 如需變更追蹤群組的詳細資訊，請參閱[將屬性加入至變更追蹤群組 &#40;Master Data Services&#41;](add-attributes-to-a-change-tracking-group-master-data-services.md)。<br /><br /> 此條件適用於文字、數字、日期及連結值。|  
|**介於**|選取的屬性 **介於** 兩個特定的屬性值之間。<br /><br /> 此條件僅適用於文字、數字及日期值。|  
  
> [!NOTE]  
>  當某個商務規則包含比較兩個值的條件，而且該規則套用到兩個值都是 NULL 的成員時，該成員將無法通過驗證。  
  
## <a name="see-also"></a>另請參閱  
 [商務規則動作 &#40;Master Data Services&#41;](../../2014/master-data-services/business-rule-actions-master-data-services.md)   
 [商務規則 &#40;Master Data Services&#41;](../../2014/master-data-services/business-rules-master-data-services.md)   
 [建立及發行商務規則 &#40;Master Data Services&#41;](../../2014/master-data-services/create-and-publish-a-business-rule-master-data-services.md)  
  
  
