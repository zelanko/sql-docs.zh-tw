---
title: Power Pivot 服務應用程式連線到 CA 中的 SharePoint Web 應用程式 |Microsoft 文件
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: ppvt-sharepoint
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: b4699746404fcc7e5f4384f2ce9871232d9aa44a
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/10/2018
---
# <a name="connect-power-pivot-service-app-to-sharepoint-web-app-in-ca"></a>Power Pivot 服務應用程式連線到 CA 中的 SharePoint Web 應用程式
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 服務應用程式可由伺服陣列中任何數目的 SharePoint Web 應用程式使用。 若要讓 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 服務應用程式可用，請將它加入至服務關聯清單。  
  
> [!IMPORTANT]  
>  預設群組中必須有一個 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 服務應用程式，才能確保 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 管理儀表板能夠適當運作。 請勿將多個 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 服務應用程式加入到預設群組。 加入相同服務應用程式類型的多個項目並不是支援的組態，而且可能會發生錯誤。 如果您要建立其他服務應用程式，請將它們加入到自訂清單。  
  
 本主題包含下列幾節：  
  
 [將 Power Pivot 服務應用程式加入至預設群組](#default)  
  
 [將 Power Pivot 服務應用程式加入至自訂服務關聯清單](#custom)  
  
##  <a name="default"></a> 將服務應用程式加入至預設群組  
 服務關聯清單是提供資源給伺服陣列中的其他 SharePoint Web 應用程式之共用服務清單。 伺服陣列有一個預設的服務關聯群組。  
  
 若要在清單上，當您建立應用程式時或之後使用下列步驟時，會加入 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 服務應用程式。  
  
1.  在 [管理中心] 的 [應用程式管理] 中，按一下 [設定服務應用程式關聯]。  
  
2.  在 [應用程式 Proxy 群組] 中，按一下 [預設值]。  
  
3.  選取 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 服務應用程式旁邊的核取方塊 (由類型名稱 **Power Pivot 服務應用程式 Proxy** 所指出)。 如果您有一個以上的 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 服務應用程式，請只選擇一個。  
  
4.  按一下 **[確定]**。  
  
##  <a name="custom"></a> 將 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 服務應用程式加入至自訂服務關聯清單  
 預設群組可由自訂清單取代。 自訂清單是特別為單一 SharePoint Web 應用程式所建立。 它會覆寫預設的群組，並僅用伺服陣列或服務管理員指定的服務關聯來取代。 如果您建立了多個 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 服務應用程式，必須使用自訂清單來指定要使用哪一個。 自訂清單無法由其他 Web 應用程式重複使用。 它只適用於建立它的 Web 應用程式。  
  
1.  在 [管理中心] 的 **[應用程式管理]** 中，按一下 **[管理 Web 應用程式]**。  
  
2.  選取應用程式 (例如 SharePoint -80)。  
  
3.  在 [Web 應用程式] 的 [管理] 中，按一下 [服務連線]。  
  
4.  在 [編輯下列連線群組] 中選取 [自訂]。  
  
5.  選取您想要使用的每個服務應用程式連接旁邊的核取方塊。 如果您具有多個 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 服務應用程式 (由設為 [Power Pivot 服務應用程式 Proxy] 的類型指出)，請務必只選擇一個。  
  
6.  按一下 **[確定]**。  
  
## <a name="see-also"></a>另請參閱  
 [在管理中心建立和設定 Power Pivot 服務應用程式](../../analysis-services/power-pivot-sharepoint/create-and-configure-power-pivot-service-application-in-ca.md)   
 [初始組態 (Power Pivot for SharePoint)](http://msdn.microsoft.com/en-us/3a0ec2eb-017a-40db-b8d4-8aa8f4cdc146)  
  
  
