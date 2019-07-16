---
title: 暫存處理序錯誤 (Master Data Services) | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: mds
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
helpviewer_keywords:
- staging process [Master Data Services], error messages
ms.assetid: 0d9be0dd-638f-4dd4-92b2-253fda655455
author: lrtoyou1223
ms.author: lle
ms.openlocfilehash: ce64900270fd1092320a12a6cc58a744eaadae7d
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/15/2019
ms.locfileid: "68085634"
---
# <a name="staging-process-errors-master-data-services"></a>暫存處理序錯誤 (Master Data Services)

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

  當暫存處理序完成時，接移資料表中的所有處理記錄都有 ErrorCode 資料行的值。 這些值會列在下表中。  
  
|程式碼|錯誤|發生時間/詳細資料|套用至資料表|  
|----------|-----------|--------------------------|----------------------|  
|210001|暫存資料表中多次出現相同的成員代碼。|您的暫存批次多次包含相同的成員代碼。 未建立或更新任何成員。|分葉<br /><br /> 合併<br /><br /> 關聯性|  
|210003|屬性值參考的成員不存在或為非使用中。|暫存網域型屬性時，您必須使用代碼，而不是名稱。 適用於 **ImportType0**、 **1**及 **2**。|分葉<br /><br /> 合併|  
|210006|成員代碼非使用中。|**ImportType** = **1**，而且您指定的成員代碼不存在。|分葉<br /><br /> 合併<br /><br /> 關聯性|  
|210032|階層名稱遺漏或無效。|找不到明確階層，或 **HierarchyName** 值空白。|合併<br /><br /> 關聯性|  
|210035|程式碼產生商務規則不存在，因此需要 **MemberCode** 。|建立或更新成員時，除非您要使用自動程式碼產生，否則一律需要 **MemberCode** 。 如需詳細資訊，請參閱[自動建立代碼 &#40;Master Data Services&#41;](../master-data-services/automatic-code-creation-master-data-services.md)。|分葉<br /><br /> 合併|  
|210036|程式碼產生商務規則存在，因此不需要 **MemberCode** 。|建立或更新成員時，如果您要使用自動程式碼產生，則不需要 **MemberCode** 。 不過，您可以選擇指定一個代碼。 如需詳細資訊，請參閱[自動建立代碼 &#40;Master Data Services&#41;](../master-data-services/automatic-code-creation-master-data-services.md)。|分葉<br /><br /> 合併|  
|210041|"ROOT" 不是有效的成員代碼。|**MemberCode** 值包含 "ROOT" 這個字。|分葉<br /><br /> 合併<br /><br /> 關聯性|  
|210042|"MDMUNUSED" 不是有效的成員代碼。|**MemberCode** 值包含 "MDMUNUSED" 這個字。|分葉<br /><br /> 合併<br /><br /> 關聯性|  
|210052|無法停用 MemberCode，因為它是做為網域屬性值。|當 **ImportType** = **3** 或 **4**時，如果此成員當做其他成員的屬性值使用，則暫存將失敗。 使用 **ImportType5** 或 **6** 將值設為 NULL，或者在執行暫存處理序之前變更值。|分葉<br /><br /> 合併|  
|300002|成員代碼無效。|關聯性：父或子成員代碼不存在。<br /><br /> 分葉或合併：**ImportType** = **3** 或 **4**，而且成員代碼不存在。|分葉<br /><br /> 合併<br /><br /> 關聯性|  
|300004|成員代碼已經存在。|**ImportType** = **1** ，而且您使用的成員代碼已存在於實體中。|分葉<br /><br /> 合併|  
|210011|當 **RelationshipType** 為 **1**時， **ParentCode** 不可以是分葉成員。|確定 **ParentCode** 值是合併成員的代碼。|關聯性|  
|210015|在階層或批次的暫存資料表中，此成員代碼出現多次。|若為明確階層，則您在相同的批次中多次指定了相同成員的位置。|關聯性|  
|210016|無法建立關聯性，因為它會造成循環參考。|當您嘗試將子項指派為父項時，就會發生這個問題。|關聯性|  
|210046|成員不可以是 [根] 的同層級。|當 **RelationshipType** = **2** (同層級)，且 **ParentCode** 或 **ChildCode** 為 [根]  時，就會發生這個問題。 成員不得與根節點位於相同層級；它們僅能為子系。|關聯性|  
|210047|成員不可以是 [未使用] 的同層級。|當 **RelationshipType** = **2** (同層級)，且 **ParentCode** 或 **ChildCode** 為 [未使用]  時，就會發生這個問題。 成員只能是 [未使用] 節點的子項。|關聯性|  
|210048|**ParentCode** 與 **ChildCode** 不可以相同。|**ParentCode** 值與 **ChildCode** 值相同。 這些值都必須不同。|關聯性|  
  
## <a name="see-also"></a>另請參閱  
 [檢視暫存期間發生的錯誤 &#40;Master Data Services&#41;](../master-data-services/view-errors-that-occur-during-staging-master-data-services.md)   
 [概觀：從資料表匯入資料 &#40;Master Data Services&#41;](../master-data-services/overview-importing-data-from-tables-master-data-services.md)  
  
  
