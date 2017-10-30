---
title: "版本 (Master Data Services) | Microsoft Docs"
ms.custom:
- SQL2016_New_Updated
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- master-data-services
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- version flags [Master Data Services], about version flags
- versions [Master Data Services]
- version flags [Master Data Services]
- versions [Master Data Services], version flags
ms.assetid: 752ec96d-53d7-4160-8ed2-92e0324645f3
caps.latest.revision: 9
author: smartysanthosh
ms.author: nagavo
manager: craigg
ms.workload: Inactive
ms.translationtype: HT
ms.sourcegitcommit: 0b832a9306244210e693bde7c476269455e9b6d8
ms.openlocfilehash: 5c633441058f1db8843de596824b235d30ec2eba
ms.contentlocale: zh-tw
ms.lasthandoff: 09/07/2017

---
# <a name="versions-master-data-services"></a>版本 (Master Data Services)
  在 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]中，您可以在模型內建立多個版本的主要資料。 系統會在您驗證資料時鎖定版本，並在驗證資料之後認可版本。 認可的版本會形成可稽核的變更記錄。 您建立的每個版本都包含該模型的所有成員、屬性值、階層成員、階層關聯性和集合。  
  
## <a name="when-to-use-versions"></a>使用版本的時機  
 使用版本可進行以下作業：  
  
-   當主要資料隨著時間而變化時，維護主資料的可稽核記錄。  
  
-   防止使用者進行變更，同時確保可根據商務規則來成功驗證所有資料。  
  
-   鎖定模型以供訂閱系統使用。  
  
-   測試不同的階層，而不立即實作。  
  
> [!NOTE]  
>  當您變更模型的結構時 (例如建立新的實體或網域屬性時)，此變更會套用至所有版本。 如果您檢視舊版的模型，將會顯示該實體或屬性，但不會有任何資料存在。  
  
## <a name="version-flags"></a>版本旗標  
 當某個版本可供使用者或訂閱系統使用時，您可以設定旗標來識別該版本。 您可以視需要在不同的版本之間移動這個旗標。 旗標可幫助使用者和訂閱系統來識別所要使用之模型的版本。  
  
## <a name="workflow-for-version-management"></a>版本管理的工作流程  
 請使用下列版本管理的工作流程：  
  
1.  當您建立模型，並使用公司的主要資料填入 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] 資料庫時，便會自動建立初始版本。 根據權限，使用者可以視需要來變更這個版本。  
  
2.  當您想要認可某個模型的版本時，請鎖定該版本，讓模型管理員才可以更新資料。 如需詳細資訊，請參閱 [Administrators &#40;Master Data Services&#41;](../master-data-services/administrators-master-data-services.md) (管理員 (Master Data Services))。 如果設定通知，每次版本狀態變更時，都會傳送電子郵件通知給模型管理員。 如需詳細資訊，請參閱[設定電子郵件通知 &#40;Master Data Services&#41;](../master-data-services/configure-email-notifications-master-data-services.md)。  
  
3.  將商務規則套用至鎖定版本的資料，並檢閱任何驗證問題。 必要時，您可以填入遺失的資訊，或還原造成問題的交易。 您也可以解除鎖定版本，以供使用者進行變更。  
  
4.  當所有資料都通過驗證時，請認可版本並為它設定旗標，以供訂閱系統使用。 已認可的版本將無法變更。  
  
5.  複製已認可的版本，並通知使用者他們可以開始使用新版本的模型。  
  
## <a name="sequential-or-simultaneous-versions"></a>循序版本或同時版本  
 您可以建立模型的循序版本或同時版本。  
  
-   **循序版本。** 每當您認可版本時，都可以建立新的複本，並為此版本提供下一個循序號碼。 例如，您可以複製模型的 **版本 7** ，並將此複本命名為 **版本 8**。  
  
-   **同時版本。** 當您想要一次處理兩個或多個版本的資料時，可以建立模型的同時版本。 當公司的重組或併購與正常的商業流程衝突，而且您想要判斷新的主資料是否適合現有的結構時，這個處理方式將會很實用。  
  
    > [!NOTE]  
    >  [!INCLUDE[ssMDScfgmgr](../includes/ssmdscfgmgr-md.md)] 中的設定會決定您是否可以複製所有版本，還是只能複製已認可的版本。 若要建立同時版本，您必須設定 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] 允許您複製所有版本。 此設定也可以在 [系統設定] 表格中使用。 如需詳細資訊，請參閱 [系統設定 &#40;Master Data Services&#41;](../master-data-services/system-settings-master-data-services.md)。  
  
## <a name="related-tasks"></a>相關工作  
  
|工作描述|主題|  
|----------------------|-----------|  
|變更現有版本的名稱。|[變更版本名稱 &#40;Master Data Services&#41;](../master-data-services/change-a-version-name-master-data-services.md)|  
|鎖定版本，僅讓管理員可以編輯其資料。|[鎖定版本 &#40;Master Data Services&#41;](../master-data-services/lock-a-version-master-data-services.md)|  
|解除鎖定版本，讓使用者可以編輯其資料。|[解除鎖定版本 &#40;Master Data Services&#41;](../master-data-services/unlock-a-version-master-data-services.md)|  
|在驗證所有資料之後認可版本。|[認可版本 &#40;Master Data Services&#41;](../master-data-services/commit-a-version-master-data-services.md)|  
|建立新旗標來標示版本。|[建立版本旗標 &#40;Master Data Services&#41;](../master-data-services/create-a-version-flag-master-data-services.md)|  
|變更現有版本旗標的名稱。|[變更版本旗標名稱 &#40;Master Data Services&#41;](../master-data-services/change-a-version-flag-name-master-data-services.md)|  
|將現有旗標指派給版本。|[將旗標指派給版本 &#40;Master Data Services&#41;](../master-data-services/assign-a-flag-to-a-version-master-data-services.md)|  
|建立現有版本的新副本|[複製版本 &#40;Master Data Services&#41;](../master-data-services/copy-a-version-master-data-services.md)|  
|刪除現有版本。|[刪除版本 &#40;Master Data Services&#41;](../master-data-services/delete-a-version-master-data-services.md)|  
|從版本清除虛刪除成員|[清除版本成員 &#40;Master Data Services&#41;](../master-data-services/purge-version-members-master-data-services.md)|  
  
## <a name="related-content"></a>相關內容  
  
-   [反轉交易 &#40;Master Data Services&#41;](../master-data-services/reverse-a-transaction-master-data-services.md)  
  
-   [通知 &#40;Master Data Services&#41;](../master-data-services/notifications-master-data-services.md)  
  
-   [商務規則 &#40;Master Data Services&#41;](../master-data-services/business-rules-master-data-services.md)  
  
  

