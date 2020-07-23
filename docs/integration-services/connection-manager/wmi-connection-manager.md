---
title: WMI 連線管理員 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.dts.designer.wmiconnection.f1
helpviewer_keywords:
- connections [Integration Services], WMI
- connection managers [Integration Services], WMI
- WMI connection manager [Integration Services]
ms.assetid: fbfa4ba7-3d0d-4d6b-94ad-50741a88d03d
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 0efcca67f53415d34cd8522fa4a59a4ddd2dab79
ms.sourcegitcommit: c8e1553ff3fdf295e8dc6ce30d1c454d6fde8088
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/22/2020
ms.locfileid: "86918235"
---
# <a name="wmi-connection-manager"></a>WMI 連接管理員

[!INCLUDE[sqlserver-ssis](../../includes/applies-to-version/sqlserver-ssis.md)]


  WMI 連接管理員可讓封裝利用 Windows Management Instrumentation (WMI)，來管理企業環境中的資訊。 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 包含的「Web 服務」工作會使用 WMI 連線管理員。  
  
 當您將 WMI 連線管理員新增至套件時，[!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 會建立在執行階段解析為 WMI 連線的連線管理員、設定連線管理員屬性，並將連線管理員新增至套件上的 **Connections** 集合。 連線管理員的 **ConnectionManagerType** 屬性會設為 **WMI**。  
  
## <a name="configuration-of-the-wmi-connection-manager"></a>設定 WMI 連接管理員  
 您可以利用下列方式設定 WMI 連接管理員：  
  
-   指定伺服器的名稱。  
  
-   指定伺服器上的命名空間。  
  
-   選取驗證模式以連接到伺服器。  
  
 您可以透過 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 設計師或以程式設計方式設定屬性。  
  
 如需可在 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 設計師中設定之屬性的相關資訊，請參閱 [WMI 連線管理員編輯器](../../integration-services/connection-manager/wmi-connection-manager-editor.md)。  
  
 如需以程式設計方式設定連線管理員的資訊，請參閱 <xref:Microsoft.SqlServer.Dts.Runtime.ConnectionManager> 和 [以程式設計方式加入連接](../../integration-services/building-packages-programmatically/adding-connections-programmatically.md)。  
  
## <a name="wmi-connection-manager-editor"></a>WMI 連接管理員編輯器
  使用 [WMI 連線管理員]  對話方塊，以指定 Microsoft Windows Management Instrumentation (WMI) 與伺服器的連線。  
  
 若要深入了解 WMI 連接管理員，請參閱＜ [WMI Connection Manager](../../integration-services/connection-manager/wmi-connection-manager.md)＞。  
  
### <a name="options"></a>選項。  
 **名稱**  
 提供唯一的名稱給連接管理員。  
  
 **說明**  
 描述連接管理員。 最佳作法是以其用途描述連接管理員，使封裝可以自我記錄並易於維護。  
  
 **伺服器名稱**  
 提供您要 WMI 連接的伺服器名稱。  
  
 **Namespace**  
 指定 WMI 命名空間。  
  
 **使用 Windows 驗證**  
 選取以使用 Windows 驗證。 如果您使用 Windows 驗證，就不需要提供連接的使用者名稱或密碼。  
  
 **使用者名稱**  
 如果您並未使用 Windows 驗證，則必須提供連接的使用者名稱。  
  
 **密碼**  
 如果您並未使用 Windows 驗證，則必須提供連接的密碼。  
  
 **Test**  
 測試連接管理員設定。  
  
## <a name="see-also"></a>另請參閱  
 [Web 服務工作](../../integration-services/control-flow/web-service-task.md)   
 [Integration Services &#40;SSIS&#41; 連接](../../integration-services/connection-manager/integration-services-ssis-connections.md)  
