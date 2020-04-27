---
title: 在管理中心將 PowerPivot 服務應用程式連接到 SharePoint Web 應用程式 |Microsoft Docs
ms.custom: ''
ms.date: 03/09/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: a5da8e29-7ffd-44e7-bf61-344fa5bea8ce
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: da816635ab978e7baadfb810aed78fa0f3258dd8
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/26/2020
ms.locfileid: "66071682"
---
# <a name="connect-a-powerpivot-service-application-to-a-sharepoint-web-application-in-central-administration"></a>在管理中心將 PowerPivot 服務應用程式連接到 SharePoint Web 應用程式
  PowerPivot 服務應用程式可由伺服陣列中任何數目的 SharePoint Web 應用程式使用。 若要讓 PowerPivot 服務應用程式可用，請將它加入至服務關聯清單。  
  
> [!IMPORTANT]  
>  預設群組中必須有一個 PowerPivot 服務應用程式，才能確保 PowerPivot 管理儀表板能夠適當運作。 請勿將多個 PowerPivot 服務應用程式加入到預設群組。 加入相同服務應用程式類型的多個項目並不是支援的組態，而且可能會發生錯誤。 如果您要建立其他服務應用程式，請將它們加入到自訂清單。  
  
 本主題包含下列幾節：  
  
 [將 PowerPivot 服務應用程式加入至預設群組](#default)  
  
 [將 PowerPivot 服務應用程式加入至自訂服務關聯清單](#custom)  
  
##  <a name="add-powerpivot-services-application-to-the-default-group"></a><a name="default"></a>將 PowerPivot 服務應用程式加入至預設群組  
 服務關聯清單是提供資源給伺服陣列中的其他 SharePoint Web 應用程式之共用服務清單。 伺服陣列有一個預設的服務關聯群組。  
  
 若要在清單上，當您建立應用程式時或之後使用下列步驟時，會加入 PowerPivot 服務應用程式。  
  
1.  在 [管理中心] 的 [應用程式管理]**** 中，按一下 [設定服務應用程式關聯]****。  
  
2.  在 [應用程式 Proxy 群組] 中，按一下 [預設值]****。  
  
3.  選取 PowerPivot 服務應用程式旁邊的核取方塊 (由類型名稱 `PowerPivot Service Application Proxy` 所指出)。 如果您有一個以上的 PowerPivot 服務應用程式，請只選擇一個。  
  
4.  按一下 [確定]  。  
  
##  <a name="add-powerpivot-services-application-a-custom-service-association-list"></a><a name="custom"></a>將 PowerPivot 服務應用程式加入至自訂服務關聯清單  
 預設群組可由自訂清單取代。 自訂清單是特別為單一 SharePoint Web 應用程式所建立。 它會覆寫預設的群組，並僅用伺服陣列或服務管理員指定的服務關聯來取代。 如果您建立了多個 PowerPivot 服務應用程式，必須使用自訂清單來指定要使用哪一個。 自訂清單無法由其他 Web 應用程式重複使用。 它只適用於建立它的 Web 應用程式。  
  
1.  在 [管理中心] 的 **[應用程式管理]** 中，按一下 **[管理 Web 應用程式]**。  
  
2.  選取應用程式 (例如 SharePoint -80)。  
  
3.  在 [Web 應用程式] 的 [管理] 中，按一下 [服務連線]****。  
  
4.  在 [編輯下列連線群組]**** 中選取 [自訂]****。  
  
5.  選取您想要使用的每個服務應用程式連接旁邊的核取方塊。 如果您具有多個 PowerPivot 服務應用程式 (由 [類型] 設定為 `PowerPivot Service Application Proxy` 來指出)，請務必只選擇一個。  
  
6.  按一下 [確定]  。  
  
## <a name="see-also"></a>另請參閱  
 [在管理中心建立和設定 PowerPivot 服務應用程式](create-and-configure-power-pivot-service-application-in-ca.md)   
 [初始設定 &#40;PowerPivot for SharePoint&#41;](../../sql-server/install/initial-configuration-powerpivot-for-sharepoint.md)  
  
  
