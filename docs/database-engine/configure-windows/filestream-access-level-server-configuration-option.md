---
title: Filestream 存取層級伺服器組態選項 | Microsoft Docs
description: 熟悉 "filestream_access_level" 選項。 了解此選項變更 SQL Server 執行個體 FILESTREAM 存取層級的方式。
ms.custom: ''
ms.date: 03/02/2017
ms.prod: sql
ms.prod_service: high-availability
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
helpviewer_keywords:
- FILESTREAM [SQL Server], access level
- filestream access level
ms.assetid: b88f6ff2-795e-4730-bfb8-dbc6a958f2ad
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 04205ee05e3c26cc807a3a6aa828152c20e4c3c7
ms.sourcegitcommit: 2f868a77903c1f1c4cecf4ea1c181deee12d5b15
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/02/2020
ms.locfileid: "91670949"
---
# <a name="filestream-access-level-server-configuration-option"></a>檔案資料流存取層級伺服器組態選項
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  您可以使用 filestream_access_level 選項來變更這個 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]執行個體的 FILESTREAM 存取層級。  
  
> [!NOTE]  
>  您必須先針對 FILESTREAM 啟用 Windows 管理設定，然後這個選項才會生效。 當您安裝 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 或使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 組態管理員時，可以啟用這些設定。  
  
|值|定義|  
|-----------|----------------|  
|0|針對這個執行個體停用 FILESTREAM 支援。|  
|1|針對 [!INCLUDE[tsql](../../includes/tsql-md.md)] 存取啟用 FILESTREAM。|  
|2|針對 [!INCLUDE[tsql](../../includes/tsql-md.md)] 和 Win32 資料流存取啟用 FILESTREAM。|  
  
## <a name="see-also"></a>另請參閱  
 [Database Engine 組態 - Filestream](../install-windows/install-sql-server.md)   
 [啟用及設定 FILESTREAM](../../relational-databases/blob/enable-and-configure-filestream.md)  
  
