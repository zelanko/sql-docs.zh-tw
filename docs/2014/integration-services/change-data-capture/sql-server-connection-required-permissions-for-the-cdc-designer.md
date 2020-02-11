---
title: SQL Server 連線所需的 CDC 設計工具權限 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: 80334de2-17c1-43c9-951e-21a9f864e9cb
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 567ee5d4c6f57d4b4eb08cbd4ecac7aef999aa55
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "62835414"
---
# <a name="sql-server-connection-required-permissions-for-the-cdc-designer"></a>SQL Server 連接所需的 CDC 設計工具權限
  CDC 設計工具主控台需要與 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 之間的連接資訊，才能執行工作。 本主題描述可以在 **[連接到 SQL Server]** 對話方塊中提供的資訊，以便設定與 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]的連接。  
  
 必要時會開啟 **[連接到 SQL Server]** 對話方塊，例如當 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 連接資訊無法取得時，或是當資訊存在但是連接沒有必要的權限時。  
  
 下表描述需要連接 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的各種工作以及 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 登入/使用者的必要權限。  
  
|Task|最低權限|  
|----------|-------------------------|  
|使用關聯的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體檢視 CDC 服務和執行個體的清單。|`db_datareader` 角色|  
|啟動/停止 CDC 執行個體|`db_datareader` 和 `db_datawriter` 角色|  
|檢視 CDC 執行個體狀態。|`db_owner` 角色|  
|建立新的 Oracle CDC 執行個體資料庫。|`dbcreator` 固定伺服器角色|  
|建立新的 Oracle CDC 執行個體。|`db_datareader` 角色<br /><br /> `db_owner` 角色。|  
|取得部署指令碼。|`db_datareader` 和 `db_datawriter` 角色<br /><br /> `db_owner` 角色|  
|變更組態及加入/移除擷取執行個體。|`db_datareader` 和 `db_datawriter` 角色<br /><br /> `db_owner` 角色|  
  
## <a name="see-also"></a>另請參閱  
 [存取 CDC 設計工具主控台](access-the-cdc-designer-console.md)   
 [用來建立執行個體的 SQL Server 連接](sql-server-connection-for-instance-creation.md)  
  
  
