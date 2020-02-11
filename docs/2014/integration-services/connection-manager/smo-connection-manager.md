---
title: SMO 連線管理員 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- connections [Integration Services], SMO
- SMO connection manager
- connection managers [Integration Services], SMO
ms.assetid: d273f1fb-a6a8-4f2f-a5ff-55c2e3de4723
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 32710f704e3d51d143e071178d690413735319f5
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "62833098"
---
# <a name="smo-connection-manager"></a>SMO 連線管理員
  SMO 連接管理員可讓封裝連接到 SQL Management Object (SMO) 伺服器。 包含的傳送工作[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]會使用 SMO 連線管理員。 例如，傳送 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 登入的「傳送登入」工作便使用 SMO 連線管理員。  
  
 當您將 SMO 連接管理員加入封裝時，[!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 會建立在執行階段解析為 SMO 連接的連接管理員、設定連接管理員屬性，並將連接管理員加入封裝上的 `Connections` 集合。 連接管理員的 `ConnectionManagerType` 屬性會設為 `SMOServer`。  
  
 您可以利用下列方式設定 SMO 連接管理員：  
  
-   指定已安裝 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 之伺服器的名稱。  
  
-   選取驗證模式以連接到伺服器。  
  
## <a name="configuration-of-the-smo-connection-manager"></a>設定 SMO 連接管理員  
 您可以透過 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 設計師或以程式設計方式設定屬性。  
  
 如需可在 [ [!INCLUDE[ssIS](../../includes/ssis-md.md)] 設計師] 中設定之屬性的詳細資訊，請參閱 [SMO 連線管理員編輯器](../smo-connection-manager-editor.md)。  
  
 如需以程式設計方式設定連線管理員的資訊，請參閱 <xref:Microsoft.SqlServer.Dts.Runtime.ConnectionManager> 和 [以程式設計方式加入連接](../building-packages-programmatically/adding-connections-programmatically.md)。  
  
## <a name="see-also"></a>另請參閱  
 [Integration Services &#40;SSIS&#41; 連接](integration-services-ssis-connections.md)  
  
  
