---
title: SMO 連線管理員 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- connections [Integration Services], SMO
- SMO connection manager
- connection managers [Integration Services], SMO
ms.assetid: d273f1fb-a6a8-4f2f-a5ff-55c2e3de4723
caps.latest.revision: 21
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 85639e416be3870a52a9d44284534f080c62a1a9
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/02/2018
ms.locfileid: "37292898"
---
# <a name="smo-connection-manager"></a>SMO 連線管理員
  SMO 連接管理員可讓封裝連接到 SQL Management Object (SMO) 伺服器。  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 包含的傳送工作會使用 SMO 連線管理員。 例如，傳送 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 登入的「傳送登入」工作便使用 SMO 連線管理員。  
  
 當您將 SMO 連接管理員加入封裝時，[!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]建立連接管理員會解析為 SMO 連接，在執行階段、 設定連接管理員屬性，並將連接管理員加入`Connections`集合封裝。 `ConnectionManagerType`連接管理員屬性設定為`SMOServer`。  
  
 您可以利用下列方式設定 SMO 連接管理員：  
  
-   指定已安裝 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 之伺服器的名稱。  
  
-   選取驗證模式以連接到伺服器。  
  
## <a name="configuration-of-the-smo-connection-manager"></a>設定 SMO 連接管理員  
 您可以透過 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 設計師或以程式設計方式設定屬性。  
  
 如需可在 [ [!INCLUDE[ssIS](../../includes/ssis-md.md)] 設計師] 中設定之屬性的詳細資訊，請參閱 [SMO 連線管理員編輯器](../smo-connection-manager-editor.md)。  
  
 以程式設計方式設定連接管理員的相關資訊，請參閱<xref:Microsoft.SqlServer.Dts.Runtime.ConnectionManager>並[連線以程式設計方式加入](../building-packages-programmatically/adding-connections-programmatically.md)。  
  
## <a name="see-also"></a>另請參閱  
 [Integration Services &#40;SSIS&#41;連線](integration-services-ssis-connections.md)  
  
  
