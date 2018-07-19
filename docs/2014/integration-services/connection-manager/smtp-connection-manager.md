---
title: SMTP 連線管理員 | Microsoft Docs
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
- connections [Integration Services], SMTP
- SMTP connection manager [Integration Services]
- connection managers [Integration Services], SMTP
ms.assetid: 3795d442-714b-4bbb-9acd-75bf277a468a
caps.latest.revision: 36
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: b05612ac34e4c2e7eb412d59eb9dcf5f28e99c78
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/02/2018
ms.locfileid: "37213478"
---
# <a name="smtp-connection-manager"></a>SMTP 連接管理員
  SMTP 連接管理員可讓封裝連接到 Simple Mail Transfer Protocol (SMTP) 伺服器。  [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 所包含的「傳送郵件」工作會使用 SMTP 連接管理員。  
  
 將 Microsoft Exchange 用作 SMTP 伺服器時，您可能需要設定 SMTP 連接管理員使用「Windows 驗證」。 Exchange 伺服器可以設定成不允許未驗證的 SMTP 連接。  
  
## <a name="configuration-the-smtp-connection-manager"></a>設定 SMTP 連接管理員  
 當您新增 SMTP 連接管理員加入封裝時，[!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]建立連接管理員會解析為 SMTP 連線，在執行階段、 設定連接管理員屬性，並將連接管理員加入`Connections`集合封裝。 `ConnectionManagerType`連接管理員屬性設定為`SMTP`。  
  
 您可以利用下列方式設定 SMTP 連接管理員：  
  
-   提供連接字串。  
  
-   指定 SMTP 伺服器的名稱。  
  
-   指定要使用的驗證方法。  
  
    > [!IMPORTANT]  
    >  SMTP 連接管理員僅支援匿名驗證和 Windows 驗證， 而不支援基本驗證。  
  
-   指定在傳送電子郵件訊息時，是否使用「安全通訊端層 (SSL)」加密通訊。  
  
 您可以透過 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 設計師或以程式設計方式設定屬性。  
  
 如需可在 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 設計師中設定之屬性的詳細資訊，請參閱 [SMTP 連線管理員編輯器](../smtp-connection-manager-editor.md)。  
  
 以程式設計方式設定連接管理員的相關資訊，請參閱<xref:Microsoft.SqlServer.Dts.Runtime.ConnectionManager>並[連線以程式設計方式加入](../building-packages-programmatically/adding-connections-programmatically.md)。  
  
  
