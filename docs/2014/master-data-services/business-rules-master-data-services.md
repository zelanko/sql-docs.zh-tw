---
title: 商務規則 (Master Data Services) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- master-data-services
ms.topic: conceptual
helpviewer_keywords:
- business rules [Master Data Services], about business rules
- business rules [Master Data Services]
ms.assetid: a9f9e41a-2461-4845-b947-58b3a205543f
author: leolimsft
ms.author: lle
manager: craigg
ms.openlocfilehash: f32495e2e12ab56ac2adb8ad5686a669714b81dc
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/02/2018
ms.locfileid: "48074329"
---
# <a name="business-rules-master-data-services"></a>商務規則 (Master Data Services)
  在 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]中，商務規則是用來確保主要資料品質和正確性的規則。 您可以使用商務規則自動更新資料、傳送電子郵件，或啟動商務程序或工作流程。  
  
## <a name="create-and-publish-business-rules"></a>建立及發行商務規則  
 商務規則是您在 [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] 中建立的 `If/Then` 陳述式。 如果屬性值符合指定的條件，便會執行動作。 可能的動作包含設定預設值或變更值。 這些動作可以結合傳送電子郵件通知。  
  
 商務規則可以以特定的屬性值 (例如，如果 Color=Blue，則採取動作) 為基礎，或當屬性值變更 (例如，如果 Color 屬性的值變更時，則採取動作)。 如需追蹤非特定變更的詳細資訊，請參閱[變更追蹤 &#40;Master Data Services&#41;](change-tracking-master-data-services.md)。  
  
 若要使用商務規則，您必須先建立並發行規則，然後將已發行的規則套用至資料。 您可以透過驗證版本，將規則套用至某個版本的資料子集或所有資料。 直到所有屬性都通過商務規則驗證之後，才能認可版本。  
  
 如果使用者所要加入的屬性值未通過商務規則驗證，此值仍然可以儲存。 您可以檢閱及更正 [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)]中顯示的驗證問題。  
  
 當您建立模型部署封裝時，若要包含商務規則，必須從封裝中的版本包含資料。  
  
 如果您建立使用 **OR** 運算子的商務規則，您應該為每個可獨立評估的條件陳述式建立不同的規則。 然後您可以視需要排除規則，提供更多彈性和輕鬆疑難排解。  
  
## <a name="how-business-rules-are-applied"></a>如何套用商務規則  
 您可以設定執行規則的優先順序。 但是在考量優先順序之前，將會根據商務規則所採取的動作類型套用該規則。 順序如下：  
  
1.  **預設值**  
  
2.  **變更值**  
  
3.  **驗證**  
  
4.  **外部動作**  
  
 在這些群組中，將會依照從最低到最高的優先順序來套用動作。 例如，四個不同的規則可能有 **[預設值]** 動作。 發生的 **[預設值]** 動作首先取決於 Web UI 中所指定的優先順序。  
  
 其他有關套用規則的重要注意事項：  
  
-   如果商務規則被排除在外或不是以 **作用中**狀態發行，此規則仍然可以使用但在套用商務規則時未包含在內。  
  
-   商務規則套用至所有分葉或所有合併成員的屬性值，但非兩者同時套用。  
  
-   商務規則可以套用至 **[開啟]** 或 **[已鎖定]** 之任何版本的模型。  
  
-   套用商務規則時對資料所做的變更不會記錄為交易。  
  
-   商務規則不得包含一個以上的 **[啟動工作流程]** 動作。  
  
## <a name="system-settings"></a>系統設定  
 [!INCLUDE[ssMDScfgmgr](../includes/ssmdscfgmgr-md.md)] 中有兩項設定會影響商務規則。 您可以在 [!INCLUDE[ssMDScfgmgr](../includes/ssmdscfgmgr-md.md)] 中或直接在 [系統設定] 表格中調整這些設定。 如需詳細資訊，請參閱 [系統設定 &#40;Master Data Services&#41;](../../2014/master-data-services/system-settings-master-data-services.md)。  
  
## <a name="related-tasks"></a>相關工作  
  
|工作描述|主題|  
|----------------------|-----------|  
|建立及發行新的商務規則。|[建立及發行商務規則&#40;Master Data Services&#41;](../../2014/master-data-services/create-and-publish-a-business-rule-master-data-services.md)|  
|將多個條件加入至商務規則。|[將多個條件新增至商務規則 &#40;Master Data Services&#41;](../../2014/master-data-services/add-multiple-conditions-to-a-business-rule-master-data-services.md)|  
|建立商務規則來要求屬性包含值。|[要求屬性值 &#40;Master Data Services&#41;](../../2014/master-data-services/require-attribute-values-master-data-services.md)|  
|建立商務規則根據屬性值變更來執行動作。|[根據屬性值變更起始動作&#40;Master Data Services&#41;](../../2014/master-data-services/initiate-actions-based-on-attribute-value-changes-master-data-services.md)|  
|變更現有商務規則的名稱。|[變更商務規則名稱 &#40;Master Data Services&#41;](../../2014/master-data-services/change-a-business-rule-name-master-data-services.md)|  
|設定 [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] 在套用商務規則時傳送通知。|[設定商務規則來傳送通知&#40;Master Data Services&#41;](../../2014/master-data-services/configure-business-rules-to-send-notifications-master-data-services.md)|  
|將商務規則套用至特定成員。|[根據商務規則驗證特定成員&#40;Master Data Services&#41;](../../2014/master-data-services/validate-specific-members-against-business-rules-master-data-services.md)|  
|排除商務規則以便不使用該規則。|[排除商務規則 &#40;Master Data Services&#41;](../../2014/master-data-services/exclude-a-business-rule-master-data-services.md)|  
|刪除現有商務規則。|[刪除商務規則 &#40;Master Data Services&#41;](../../2014/master-data-services/delete-a-business-rule-master-data-services.md)|  
  
## <a name="related-content"></a>相關內容  
  
-   [Master Data Services 概觀](master-data-services-overview-mds.md)  
  
-   [版本&#40;Master Data Services&#41;](../../2014/master-data-services/versions-master-data-services.md)  
  
-   [驗證&#40;Master Data Services&#41;](../../2014/master-data-services/validation-master-data-services.md)  
  
-   [變更追蹤 &#40;Master Data Services&#41;](change-tracking-master-data-services.md)  
  
  
