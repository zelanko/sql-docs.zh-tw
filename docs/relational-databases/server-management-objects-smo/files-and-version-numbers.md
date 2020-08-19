---
description: 檔案和版本號碼
title: 檔案和版本號碼 |Microsoft Docs
ms.custom: ''
ms.date: 08/06/2017
ms.prod: sql
ms.prod_service: database-engine
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
author: markingmyname
ms.author: maghan
monikerRange: =azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 850268d303106e8c07a19915f9284b6c4dc3f7d2
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88420272"
---
# <a name="files-and-version-numbers"></a>檔案和版本號碼
[!INCLUDE [SQL Server ASDB, ASDBMI, ASDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asa.md)]

  所有必要的 SQL Server 管理物件 (SMO) 元件都包含在 SqlManagementObjects NuGet 套件中。 SMO 是實作於數個 Managed 組件中。 您可以在用戶端或伺服器上開發 SMO 應用程式。  

> > [!Important]
> > SMO 元件的檔案版本會顯示為 [主要]。**0**。Build. 修訂。 但是內嵌的元件版本是主要的。**100**。Build. 修訂。 這樣做的目的是要讓每個應用程式中使用的 SMO 版本保持分開，如此一來，更新就不會影響任何其他應用程式。
> > 
> > 因此，您 **不** 應該將這些版本的元件安裝到全域組件快取 (GAC) 。 這樣做可能會導致其他應用程式（例如 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Management Studio）中斷。 
  
|檔案|描述|  
|-----------|-----------------|  
|Microsoft.SqlServer.ConnectionInfo.dll|包含與 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體進行連接的支援。|  
|Microsoft.SqlServer.ServiceBrokerEnum.dll|包含 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Service Broker 程式設計的支援。 只有在存取 Service Broker 的程式中才需要此檔案。|  
|Microsoft.SqlServer.Smo.dll|包含大部分的 SMO 類別。|  
|Microsoft.SqlServer.SmoExtended.dll<br /><br /> Microsoft.SqlServer.Management.Sdk.Sfc.dll<br /><br /> Microsoft.SqlServer.SqlEnum.dll|包含 SMO 類別的支援。|  
|Microsoft.SqlServer.WmiEnum.dll|包含 Windows Management Instrumentation (WMI) 提供者類別。 這只有在使用 WMI 提供者類別的程式中才需要此檔案。|  
|Microsoft.SqlServer.RegSvrEnum.dll|包含已註冊的伺服器的類別。 這只有在使用已註冊伺服器類別的程式中才需要此檔案。|  
  
  
