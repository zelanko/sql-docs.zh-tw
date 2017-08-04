---
title: "變更追蹤 (Master Data Services) |Microsoft 文件"
ms.custom: 
ms.date: 03/15/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- master-data-services
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- change tracking [SQL Server]
ms.assetid: 5e879c65-0d38-454f-9a20-62a6e72c89f7
caps.latest.revision: 7
author: sabotta
ms.author: carlasab
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 6851da978ab681f0236bc9737e7f628c0089abe0
ms.contentlocale: zh-tw
ms.lasthandoff: 08/02/2017

---
# <a name="change-tracking-master-data-services"></a>變更追蹤 (Master Data Services)
  在 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] 中，您可以使用變更追蹤群組在屬性值變更時採取動作。 當您不知道新值，但想要知道是否發生任何變更時，請使用變更追蹤。  
  
## <a name="configuring-change-tracking"></a>設定變更追蹤  
 若要設定變更追蹤，您要將屬性加入至變更追蹤群組。 此群組可以包含一個或多個屬性。 接著，您要建立商務規則來定義群組中的任何屬性變更時所要採取的動作。  
  
> [!NOTE]  
>  變更追蹤商務規則會將暫存 (匯入的) 資料視為變更。  
  
## <a name="related-tasks"></a>相關工作  
  
|工作描述|主題|  
|----------------------|-----------|  
|將屬性加入至變更追蹤群組。|[將屬性加入至變更追蹤群組 &#40;Master Data services&#41;](../master-data-services/add-attributes-to-a-change-tracking-group-master-data-services.md)|  
|建立根據屬性變更來起始動作的商務規則。|[根據屬性值的變更 &#40; 起始動作Master Data services&#41;](../master-data-services/initiate-actions-based-on-attribute-value-changes-master-data-services.md)|  
  
## <a name="related-content"></a>相關內容  
  
-   [驗證 &#40;Master Data services&#41;](../master-data-services/validation-master-data-services.md)  
  
-   [商務規則 &#40;Master Data services&#41;](../master-data-services/business-rules-master-data-services.md)  
  
-   [屬性 &#40;Master Data services&#41;](../master-data-services/attributes-master-data-services.md)  
  
  
