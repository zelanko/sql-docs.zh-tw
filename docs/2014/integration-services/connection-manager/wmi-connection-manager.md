---
title: WMI 連線管理員 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- connections [Integration Services], WMI
- connection managers [Integration Services], WMI
- WMI connection manager [Integration Services]
ms.assetid: fbfa4ba7-3d0d-4d6b-94ad-50741a88d03d
caps.latest.revision: 39
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.openlocfilehash: 199cea31baaee58c25b50a8ef0aefed15dfab387
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36146113"
---
# <a name="wmi-connection-manager"></a>WMI 連接管理員
  WMI 連接管理員可讓封裝利用 Windows Management Instrumentation (WMI)，來管理企業環境中的資訊。 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 包含的 Web 服務工作會使用 WMI 連線管理員。  
  
 當您新增 WMI 連接管理員加入封裝時，[!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]建立連線管理員，將會解析為 WMI 連接，在執行階段，設定連接管理員屬性，並將連接管理員加入`Connections`集合封裝。 `ConnectionManagerType`連接管理員的屬性設定為`WMI`。  
  
## <a name="configuration-of-the-wmi-connection-manager"></a>設定 WMI 連接管理員  
 您可以利用下列方式設定 WMI 連接管理員：  
  
-   指定伺服器的名稱。  
  
-   指定伺服器上的命名空間。  
  
-   選取驗證模式以連接到伺服器。  
  
 您可以透過 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 設計師或以程式設計方式設定屬性。  
  
 如需可在 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 設計師中設定之屬性的相關資訊，請參閱 [WMI 連線管理員編輯器](../wmi-connection-manager-editor.md)。  
  
 如需以程式設計方式設定連接管理員資訊，請參閱<xref:Microsoft.SqlServer.Dts.Runtime.ConnectionManager>和[新增連線以程式設計方式](../building-packages-programmatically/adding-connections-programmatically.md)。  
  
## <a name="see-also"></a>另請參閱  
 [Web 服務工作](../control-flow/web-service-task.md)   
 [Integration Services &#40;SSIS&#41;連線](integration-services-ssis-connections.md)  
  
  