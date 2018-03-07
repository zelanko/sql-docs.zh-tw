---
title: "商務規則動作 (Master Data Services) | Microsoft Docs"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-non-specified
ms.prod_service: mds
ms.service: 
ms.component: non-specific
ms.reviewer: 
ms.suite: sql
ms.technology:
- master-data-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: cdc4daca-3dff-46d8-b7f0-57f7826dd61a
caps.latest.revision: 
author: leolimsft
ms.author: lle
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 1caf657ac063453ca5bbea7b41b46ae9164306ee
ms.sourcegitcommit: 6ac1956307d8255dc544e1063922493b30907b80
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/05/2018
---
# <a name="business-rule-actions-master-data-services"></a>商務規則動作 (Master Data Services)
  在 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]中，商務規則動作是商務規則條件評估的結果。 如果條件為 true，就會起始動作。  
  
> [!NOTE]  
>  對於預設值和變更值動作而言，如果產生的值超出屬性的最大長度，則會截斷產生的值。  
  
## <a name="default-value-actions"></a>預設值動作  
 **預設值** 動作會設定指定屬性的預設值。 具有權限的使用者可以變更這些預設值。  
  
|值名稱|描述|  
|----------------|-----------------|  
|**預設為**|選取的屬性 **預設為** 特定的屬性、特定的屬性值或空白。<br /><br /> 此動作僅適用於文字、數字、日期及連結值。|  
|**預設為產生的值**|選取的屬性 **預設為產生的值** ，這個值取決於輸入開始和增量值。<br /><br /> 此動作僅適用於文字及數值。|  
|**預設為串連值**|選取的屬性 **預設為串連值** ，這個值取決於指定多個屬性。<br /><br /> 此動作適用於文字及連結值。|  
  
## <a name="change-value-actions"></a>變更值動作  
 **變更值** 動作會更新指定屬性或屬性值的值。 只有新的值導致動作為 true 時，使用者才可以變更這些值。  
  
|值名稱|描述|  
|----------------|-----------------|  
|**等於**|選取的屬性變更為已定義的屬性值、另一個屬性或空白。<br /><br /> 此動作僅適用於文字、數字、日期及連結值。|  
|**等於串連值**|選取的屬性變更為串連值，這個值取決於指定多個屬性。<br /><br /> 此動作適用於文字及連結值。|  
  
## <a name="validation-actions"></a>驗證動作  
 **[驗證]** 動作，當無法評估為 true 時，會傳送電子郵件給指定的使用者或群組。 若要認可版本，所有的驗證動作都必須評估為 true。  
  
 唯一的例外狀況是： **強制性** 和 **無效** 動作。 這兩個動作必須與變更值動作結合，以便讓資料驗證成功，並讓版本進行認可。  
  
|驗證名稱|描述|  
|---------------------|-----------------|  
|**需要**|選取的屬性 **為需要的**，表示不能為 null 或空白。<br /><br /> 此動作僅適用於文字、數字、日期及連結值。|  
|**無效**|選取的屬性 **無效**。<br /><br /> 此動作僅適用於文字、數字、日期及連結值。|  
|**必須包含模式**|選取的屬性 **必須包含指定的模式** 。 使用 .NET Framework 規則運算式來指定模式。<br /><br /> 如需有關規則運算式的詳細資訊，請參閱 MSDN Library 中的 [規則運算式語言項目](http://go.microsoft.com/fwlink/?LinkId=164401) 。<br /><br /> 此動作適用於文字及連結值。|  
|**必須是唯一的**|選取的屬性 **必須獨立或與定義的屬性結合時是唯一的** 。<br /><br /> **最佳作法** ：結合此動作與強制性條件，以確保訂閱系統中索引欄位的有效性。<br /><br /> 此動作僅適用於文字、數字、日期及連結值。<br /><br /> **注意**：如果第一個屬性的類型是 DateTime，則無法與類型為 Numeric 或 Text 的屬性一起使用。 如果第一個屬性的類型是 Numeric，則無法與類型為 DateTime 的屬性一起使用。|  
|**必須具有下列其中一個值**|選取的屬性 **必須具有清單中指定的其中一個值** 。<br /><br /> 此動作適用於文字值。|  
|**必須大於**|選取的屬性 **必須大於** 特定的屬性、特定的屬性值或空白。<br /><br /> 此動作適用於文字、數字及日期值。|  
|**必須等於**|選取的屬性 **必須等於** 已定義的屬性值、另一個屬性或空白。<br /><br /> 此動作僅適用於文字、數字、日期及連結值。|  
|**必須大於或等於**|選取的屬性 **必須大於或等於** 特定的屬性、特定的屬性值或空白。<br /><br /> 此動作適用於文字、數字及日期值。|  
|**必須小於**|選取的屬性 **必須小於** 特定的屬性、特定的屬性值或空白。<br /><br /> 此動作適用於文字、數字及日期值。|  
|**必須小於或等於**|選取的屬性 **必須小於或等於** 特定的屬性、特定的屬性值或空白。<br /><br /> 此動作適用於文字、數字及日期值。|  
|**必須介於**|選取的屬性 **必須介於** 兩個特定的屬性或屬性值之間。<br /><br /> 此動作適用於文字、數字及日期值。|  
|**必須具有最小長度**|選取的屬性 **必須具有指定值的最小長度** 。<br /><br /> 此動作適用於文字及連結值。|  
|**必須具有最大長度**|選取的屬性 **必須具有指定值的最大長度** 。<br /><br /> 此動作適用於文字及連結值。|  
  
## <a name="external-action"></a>外部動作  
 **外部** 動作會與 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]之外的應用程式互動。  
  
|動作名稱|描述|  
|-----------------|-----------------|  
|**啟動工作流程**|起始外部工作流程。 造成此動作發生的資料會傳遞給工作流程。 如需詳細資訊，請參閱 [Master Data Services 的 SharePoint 工作流程整合](http://msdn.microsoft.com/library/gg690195.aspx)。<br /><br /> 此動作僅適用於文字、數字、日期及連結值。|  
  
## <a name="see-also"></a>另請參閱  
 [商務規則條件 &#40;Master Data Services&#41;](../master-data-services/business-rule-conditions-master-data-services.md)   
 [商務規則 &#40;Master Data Services&#41;](../master-data-services/business-rules-master-data-services.md)   
 [建立及發行商務規則 &#40;Master Data Services&#41;](../master-data-services/create-and-publish-a-business-rule-master-data-services.md)  
  
  
