---
title: 檔案和版本號碼 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: reference
helpviewer_keywords:
- SQL Server Management Objects, versions
- components [SMO]
- files [SMO], components
- SMO [SQL Server], versions
- versions [SMO]
ms.assetid: 510907b6-e7a9-41bd-b892-d6d99a5118e1
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 0a1b0b28afbb83028af8d71644af08ca660a0b36
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/26/2020
ms.locfileid: "62753410"
---
# <a name="files-and-version-numbers"></a>檔案和版本號碼
  所有必要[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]的管理物件（SMO）元件都會安裝為[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]用戶端或伺服器實例的一部分。 SMO 是實作於數個 Managed 組件中。 您可以在用戶端或伺服器上開發 SMO 應用程式。  
  
|目錄|檔案|描述|  
|---------------|----------|-----------------|  
|[!INCLUDE[ssSampPathSDK](../../includes/sssamppathsdk-md.md)]|Microsoft.SqlServer.ConnectionInfo.dll|包含與 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體進行連接的支援。|  
|[!INCLUDE[ssSampPathSDK](../../includes/sssamppathsdk-md.md)]|Microsoft.SqlServer.ServiceBrokerEnum.dll|包含 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Service Broker 程式設計的支援。 只有在存取 Service Broker 的程式中才需要此檔案。|  
|[!INCLUDE[ssSampPathSDK](../../includes/sssamppathsdk-md.md)]|Microsoft.SqlServer.Smo.dll|包含大部分的 SMO 類別。|  
|[!INCLUDE[ssSampPathSDK](../../includes/sssamppathsdk-md.md)]|Microsoft.SqlServer.SmoExtended.dll<br /><br /> Microsoft.SqlServer.Management.Sdk.Sfc.dll<br /><br /> Microsoft.SqlServer.SqlEnum.dll|包含 SMO 類別的支援。|  
|[!INCLUDE[ssSampPathSDK](../../includes/sssamppathsdk-md.md)]|Microsoft.SqlServer.WmiEnum.dll|包含 Windows Management Instrumentation (WMI) 提供者類別。 這只有在使用 WMI 提供者類別的程式中才需要此檔案。|  
|[!INCLUDE[ssSampPathSDK](../../includes/sssamppathsdk-md.md)]|Microsoft.SqlServer.RegSvrEnum.dll|包含已註冊的伺服器的類別。 這只有在使用已註冊伺服器類別的程式中才需要此檔案。|  
  
  
