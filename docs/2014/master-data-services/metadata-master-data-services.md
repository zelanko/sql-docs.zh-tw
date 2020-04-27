---
title: 中繼資料（Master Data Services） |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2019
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
helpviewer_keywords:
- user-defined metadata [Master Data Services], about user-defined metadata
- metadata [Master Data Services], about metadata
- metadata [Master Data Services]
- user-defined metadata [Master Data Services]
ms.assetid: ac1aabe3-d8d4-4d7a-8954-50ee3c185d81
author: lrtoyou1223
ms.author: lle
manager: craigg
ms.openlocfilehash: 2bbb98653dbbaad577f9a48d7a778b41d19fbf37
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/26/2020
ms.locfileid: "66054041"
---
# <a name="metadata-master-data-services"></a>中繼資料 (Master Data Services)
  在 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] 中，使用者定義的中繼資料是用來描述模型物件的資訊。 例如，您可以追蹤特定模型或實體的擁有者，或追蹤提供資料給實體的來源系統。  
  
 使用者定義的中繼資料是由稱為「**中繼資料**」的模型所管理。 當安裝時[!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] ，會自動包含此模型，而且它類似于其他所有 MDS 模型，但您無法建立其版本。  
  
 當您使用使用者定義的中繼資料來擴展中繼資料模型時，可以將其包含在訂閱檢視中，以便透過訂閱系統來取用。  
  
## <a name="metadata-entities"></a>中繼資料實體  
 中繼資料模型包含五個實體，每個實體代表一種支援使用者定義中繼資料的主要資料模型物件類型。 例如，「**模型元資料定義**」實體包含代表模型的成員，而「**屬性元資料定義**」實體具有代表所有模型中所有屬性的成員。  
  
 若要定義模型物件的中繼資料，必須擴展其中一個成員的屬性。 例如，在**實體元資料定義**實體中，您可以在價格成員的 Description 屬性中填入下列文字：**銷售給客戶時的產品價格**。  
  
 每當加入或刪除支援使用者定義中繼資料的模型物件時，中繼資料模型中的成員會自動更新。  
  
 中繼資料模型無法建立版本、加入或變更版本旗標，或是另存為模型部署封裝。 不過，它所提供的其他功能與其他主要資料模型都相同。 例如，您可以在中繼資料模型上實作一組商務規則來強制資料原則。  
  
## <a name="customizing-your-metadata-model"></a>自訂中繼資料模型  
 每個中繼資料定義實體都包含名稱、代碼和描述屬性。 您可以建立其他屬性，進一步描述模型物件。  
  
 例如，您可以建立：  
  
-   名稱為 [擁有者] 的網域屬性，用來追蹤每個模型物件的擁有者。  
  
-   名稱為 [上次檢閱日期] 的自由格式屬性，用來追蹤擁有者上次檢閱物件的日期。  
  
-   名為 [來源] 的網域屬性，用來追蹤和管理與[!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]實例互動的來源系統。  
  
## <a name="related-tasks"></a>相關工作  
  
|工作描述|主題|  
|----------------------|-----------|  
|將中繼資料加入至模型物件。|[新增中繼資料 &#40;Master Data Services&#41;](add-metadata-master-data-services.md)
|&nbsp;|&nbsp;|
  
## <a name="related-content"></a>相關內容  
  
-   [將資料匯出 &#40;Master Data Services&#41;](overview-exporting-data-master-data-services.md)  
  
  
