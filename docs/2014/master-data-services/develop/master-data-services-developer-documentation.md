---
title: 開發人員&#39;指南 (Master Data Services) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology: master-data-services
ms.tgt_pltfrm: ''
ms.topic: reference
ms.assetid: 067b1f69-84eb-4a13-b220-120cd63704b4
author: leolimsft
ms.author: lle
manager: craigg
ms.openlocfilehash: d16e4e431a7df73cd775b635ad6ebd8efb1e1e75
ms.sourcegitcommit: 022d67cfbc4fdadaa65b499aa7a6a8a942bc502d
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/03/2018
ms.locfileid: "37349500"
---
# <a name="developer39s-guide-master-data-services"></a>開發人員&#39;指南 (Master Data Services)
  尋找有關如何撰寫程式碼以自訂您和您的使用者與 [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] 互動之方式的資訊。 了解如何：  
  
-   撰寫存取 [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] Web 服務的程式。 [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] Web 服務是一個 Windows Communication Foundation (WCF) 服務，開發人員會使用這個服務，透過程式碼控制 [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] 功能。  
  
-   將 [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] 功能納入現有的應用程式。  
  
-   撰寫程式碼以執行使用 [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] UI 難以或無法執行的重複或複雜動作。  
  
-   建立為回應您所指定之商務規則而執行的自訂工作流程。 自訂工作流程會呼叫您所撰寫、而且可以採取處理工作流程所需之任何動作的程式碼。  
  
## <a name="master-data-manager-web-service"></a>主資料管理員 Web 服務  
 [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] Web 服務可讓您以程式設計的方式，從可以存取 [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] 網站的任何電腦使用 [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] 的功能。 在您可以開始撰寫程式碼以存取 Web 服務之前，必須先產生 Proxy 類別，該類別包含在您所指定的命名空間內。 此文件集使用 <xref:Microsoft.MasterDataServices> 當做 Proxy 命名空間。 您用來執行 Web 服務作業的主要 Proxy 類別為 <xref:Microsoft.MasterDataServices.ServiceClient> 類別，此類別會實作 <xref:Microsoft.MasterDataServices.IService> 介面。 從您的程式碼中呼叫 <xref:Microsoft.MasterDataServices.ServiceClient> 類別的方法，以存取 [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] Web 服務。 命名空間內的其餘類別是由 Web 服務作業所使用。  
  
### <a name="web-service-content"></a>Web 服務內容  
 [建立主資料管理員 Web 服務 Proxy 類別](create-master-data-manager-web-service-proxy-classes.md)  
 描述如何從 [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] 網站啟用中繼資料發佈，以及如何建立可透過程式設計方式，用來存取 Web 服務作業的 Proxy 類別。  
  
 [分類的 Web 服務作業 &#40;Master Data Services&#41;](categorized-web-service-operations-master-data-services.md)  
 <xref:Microsoft.MasterDataServices.ServiceClient> 類別之 Web 服務作業的分類清單。  
  
## <a name="custom-workflows"></a>自訂工作流程  
 [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] 使用商務規則建立基本工作流程解決方案。 您可以自動更新與驗證資料，並根據您所指定的條件傳送電子郵件通知。 [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] 中的商務規則可用來管理最常見的工作流程案例。 如果您的工作流程需要更複雜的事件處理 (例如多層審核或複雜決策樹)，可以設定 [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] 將資料傳送到您所建立的自訂組件。 若要處理自訂工作流程，您必須在 Web 應用程式電腦上設定並啟動 SQL Server MDS 工作流程整合服務，然後建立一個實作 <xref:Microsoft.MasterDataServices.WorkflowTypeExtender.IWorkflowTypeExtender> 介面的組件。  
  
### <a name="custom-workflow-content"></a>自訂的工作流程內容  
 [建立自訂工作流程 &#40;Master Data Services&#41;](create-a-custom-workflow-master-data-services.md)  
 有關如何建立工作流程處理常式組件、如何設定並啟動 SQL Server MDS 工作流程整合服務，以及如何在 [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] 中建立啟動自訂工作流程之商務規則的指示。  
  
## <a name="web-server-namespaces"></a>Web 伺服器命名空間  
 [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] 會將一組組件安裝在 Web 伺服器電腦上。 這些組件包含可用於進階案例的命名空間，這些案例會自訂 Web 伺服器電腦的行為。 下表描述這些命名空間。  
  
|命名空間|描述|  
|---------------|-----------------|  
|<xref:Microsoft.MasterDataServices.Deployment>|包含的類別可用來從模型建立部署封裝以及將封裝部署到 [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] 資料庫。|  
|<xref:Microsoft.MasterDataServices.Services>|包含的類別可接收和處理透過 [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] Web 應用程式對 Web 伺服器電腦所做的 Web 服務作業。|  
|<xref:Microsoft.MasterDataServices.Services.DataContracts>|包含的類別可定義資料如何透過 [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] Web 應用程式從用戶端電腦傳送到 Web 伺服器電腦。|  
|<xref:Microsoft.MasterDataServices.Services.MessageContracts>|包含的類別可定義要求和回應如何透過 [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] Web 應用程式從用戶端電腦傳送到 Web 伺服器電腦。|  
|<xref:Microsoft.MasterDataServices.Services.ServiceContracts>|包含的介面可定義可以透過 [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] Web 服務呼叫的作業。|  
  
  
