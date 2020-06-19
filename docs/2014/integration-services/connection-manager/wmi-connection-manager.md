---
title: WMI 連線管理員 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- connections [Integration Services], WMI
- connection managers [Integration Services], WMI
- WMI connection manager [Integration Services]
ms.assetid: fbfa4ba7-3d0d-4d6b-94ad-50741a88d03d
author: janinezhang
ms.author: janinez
ms.openlocfilehash: 29ddc30f89621e9b4875a57c191a81ef3f10784d
ms.sourcegitcommit: 9ee72c507ab447ac69014a7eea4e43523a0a3ec4
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/17/2020
ms.locfileid: "84920233"
---
# <a name="wmi-connection-manager"></a>WMI 連接管理員
  WMI 連接管理員可讓封裝利用 Windows Management Instrumentation (WMI)，來管理企業環境中的資訊。 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 包含的「Web 服務」工作會使用 WMI 連線管理員。  
  
 當您將 WMI 連線管理員加入封裝時， [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 會建立在執行時間解析為 WMI 連接的連線管理員、設定連線管理員屬性，並將連線管理員加入 `Connections` 封裝上的集合。 連接管理員的 `ConnectionManagerType` 屬性會設為 `WMI`。  
  
## <a name="configuration-of-the-wmi-connection-manager"></a>設定 WMI 連接管理員  
 您可以利用下列方式設定 WMI 連接管理員：  
  
-   指定伺服器的名稱。  
  
-   指定伺服器上的命名空間。  
  
-   選取驗證模式以連接到伺服器。  
  
 您可以透過 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 設計師或以程式設計方式設定屬性。  
  
 如需可在 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 設計師中設定之屬性的相關資訊，請參閱 [WMI 連線管理員編輯器](../wmi-connection-manager-editor.md)。  
  
 如需以程式設計方式設定連線管理員的資訊，請參閱 <xref:Microsoft.SqlServer.Dts.Runtime.ConnectionManager> 和 [以程式設計方式加入連接](../building-packages-programmatically/adding-connections-programmatically.md)。  
  
## <a name="see-also"></a>另請參閱  
 [Web 服務工作](../control-flow/web-service-task.md)   
 [Integration Services &#40;SSIS&#41; 連接](integration-services-ssis-connections.md)  
  
  
