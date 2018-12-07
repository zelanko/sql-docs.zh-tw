---
title: 驗證 (Master Data Services) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: mds
ms.reviewer: ''
ms.technology:
- master-data-services
ms.topic: conceptual
ms.assetid: 98eb49e7-b190-4a21-8316-08c07cde14ed
author: leolimsft
ms.author: lle
manager: craigg
ms.openlocfilehash: 5e4691d20c5dbbe67c7d457dbee2042cfd9ad203
ms.sourcegitcommit: 1ab115a906117966c07d89cc2becb1bf690e8c78
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/27/2018
ms.locfileid: "52395461"
---
# <a name="validation-master-data-services"></a>驗證 (Master Data Services)

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

  在 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]中，會驗證資料以確保其正確性。 其中一部分驗證會自動發生，而另外一部分驗證則會根據管理員建立的商務規則。  
  
## <a name="when-data-validation-occurs"></a>當資料驗證發生時  
 驗證發生在不同的時間，並以不同的方式顯示在 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] Web 應用程式中。  
  
|驗證類型|決定標準的人員|發生時機|在主資料管理員 Web UI 中顯示成|在適用於 Excel 的增益集中顯示成|資料是否會儲存至 MDS 儲存機制？|  
|---------------------|-----------------------------|--------------------|---------------------------------------------------|-------------------------------------------|------------------------------------------|  
|商務規則驗證|MDS 管理員|使用者加入或編輯資料時自動發生。<br /><br /> 使用者套用商務規則時手動發生。<br /><br /> 管理員在 **Web 應用程式的** [版本管理] [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] 功能區域中，根據商務規則驗證版本時手動發生。|驗證錯誤|ValidationStatus|是|  
|資料類型和內容驗證|MDS 管理員，建立模型物件時 (例如，屬性的長度或資料類型)|使用者加入或編輯資料時自動發生|輸入錯誤|InputStatus|否|  
|資料類型和內容驗證|[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 或 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]|使用者加入或編輯資料時自動發生|輸入錯誤|InputStatus|否|  
  
## <a name="related-tasks"></a>相關工作  
  
|工作描述|主題|  
|----------------------|-----------|  
|建立並發行商務規則，以根據商務規則驗證資料。|[建立及發行商務規則 &#40;Master Data Services&#41;](../master-data-services/create-and-publish-a-business-rule-master-data-services.md)|  
|依商務規則驗證資料版本 僅限管理員。|[根據商務規則驗證版本 &#40;Master Data Services&#41;](../master-data-services/validate-a-version-against-business-rules-master-data-services.md)|  
|根據商務規則驗證資料的特定子集。 具有 **[總管]** 功能區域權限的所有使用者。|[根據商務規則驗證特定成員 &#40;Master Data Services&#41;](../master-data-services/validate-specific-members-against-business-rules-master-data-services.md)|  
|根據商務規則驗證資料的特定子集。 具有 **[總管]** 功能區域權限並且使用 [!INCLUDE[ssMDSXLS](../includes/ssmdsxls-md.md)]的所有使用者。|[套用商務規則 &#40;適用於 Excel 的 MDS 增益集&#41;](../master-data-services/microsoft-excel-add-in/apply-business-rules-mds-add-in-for-excel.md)|  
  
## <a name="see-also"></a>另請參閱  
 [商務規則 &#40;Master Data Services&#41;](../master-data-services/business-rules-master-data-services.md)  
  
  
