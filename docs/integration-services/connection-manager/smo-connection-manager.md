---
title: "SMO 連接管理員 |Microsoft 文件"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: connection-manager
ms.reviewer: 
ms.suite: sql
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.dts.designer.smoconnection.f1
helpviewer_keywords:
- connections [Integration Services], SMO
- SMO connection manager
- connection managers [Integration Services], SMO
ms.assetid: d273f1fb-a6a8-4f2f-a5ff-55c2e3de4723
caps.latest.revision: 21
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 8397673c7ed9dfe8ae02871f9077ed7286e49863
ms.openlocfilehash: d1f03b27dd5dca9e9a2940abf3731a2f5cefe0af
ms.contentlocale: zh-tw
ms.lasthandoff: 08/09/2017

---
# <a name="smo-connection-manager"></a>SMO 連接管理員
  SMO 連接管理員可讓封裝連接到 SQL Management Object (SMO) 伺服器。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 包含的傳送工作會使用 SMO 連線管理員。 例如，傳送 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 登入的「傳送登入」工作便使用 SMO 連線管理員。  
  
 當您將 SMO 連線管理員加入封裝時， [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 會建立在執行階段解析為 SMO 連接的連線管理員、設定連線管理員屬性，並將連線管理員加入封裝上的 **Connections** 集合。 連線管理員的 **ConnectionManagerType** 屬性會設為 **SMOServer**。  
  
 您可以利用下列方式設定 SMO 連接管理員：  
  
-   指定已安裝 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 之伺服器的名稱。  
  
-   選取驗證模式以連接到伺服器。  
  
## <a name="configuration-of-the-smo-connection-manager"></a>設定 SMO 連接管理員  
 您可以透過「 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 設計師」或以程式設計方式設定屬性。  
  
 如需可在 [ [!INCLUDE[ssIS](../../includes/ssis-md.md)] 設計師] 中設定之屬性的詳細資訊，請參閱 [SMO 連線管理員編輯器](../../integration-services/connection-manager/smo-connection-manager-editor.md)。  
  
 如需以程式設計方式設定連線管理員的相關資訊，請參閱 <xref:Microsoft.SqlServer.Dts.Runtime.ConnectionManager> 和 [以程式設計方式加入連接](../../integration-services/building-packages-programmatically/adding-connections-programmatically.md)。  
  
## <a name="smo-connection-manager-editor"></a>SMO 連接管理員編輯器
  使用 [SMO 連線管理員編輯器] 來設定傳送 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 物件的各種工作所使用的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 連接。  
  
 若要深入了解 SMO 連線管理員，請參閱 [SMO 連線管理員](../../integration-services/connection-manager/smo-connection-manager.md)。  
  
### <a name="options"></a>選項。  
 **伺服器名稱**  
 輸入 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體的名稱，或從清單中選取伺服器名稱。  
  
 **重新整理**  
 重新整理可以在網路上偵測到的可用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體的清單。  
  
 **使用 Windows 驗證**  
 使用 Windows 驗證連接到選取的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體。  
  
 **使用 SQL Server 驗證**  
 使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 驗證連接到選取的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體。  
  
 **使用者名稱**  
 如果您已經選取 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 驗證，請輸入 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 使用者名稱。  
  
 **密碼**  
 如果您已經選取 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 驗證，請輸入密碼。  
  
 **測試連接**  
 以目前的設定測試連接。  
  
## <a name="see-also"></a>另請參閱  
 [Integration Services &#40;SSIS&#41; 連接](../../integration-services/connection-manager/integration-services-ssis-connections.md)  
  
  

