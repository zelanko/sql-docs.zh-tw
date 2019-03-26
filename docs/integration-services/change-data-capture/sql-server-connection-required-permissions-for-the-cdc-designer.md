---
title: SQL Server 連線所需的 CDC 設計工具權限 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: 80334de2-17c1-43c9-951e-21a9f864e9cb
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: b9a95743de7e75620cc1f3b0d07b2d9b42a878f3
ms.sourcegitcommit: 7ccb8f28eafd79a1bddd523f71fe8b61c7634349
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/20/2019
ms.locfileid: "58290046"
---
# <a name="sql-server-connection-required-permissions-for-the-cdc-designer"></a>SQL Server 連接所需的 CDC 設計工具權限
  CDC 設計工具主控台需要與 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 之間的連接資訊，才能執行工作。 本主題描述可以在 **[連接到 SQL Server]** 對話方塊中提供的資訊，以便設定與 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]的連接。  
  
 必要時會開啟 **[連接到 SQL Server]** 對話方塊，例如當 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 連接資訊無法取得時，或是當資訊存在但是連接沒有必要的權限時。  
  
 下表描述需要連接 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的各種工作以及 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 登入/使用者的必要權限。  
  
|工作|最小權限|  
|----------|-------------------------|  
|使用關聯的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體檢視 CDC 服務和執行個體的清單。|`db_datareader` 角色|  
|啟動/停止 CDC 執行個體|`db_datareader` 和 `db_datawriter` 角色|  
|檢視 CDC 執行個體狀態。|`db_owner` 角色|  
|建立新的 Oracle CDC 執行個體資料庫。|`dbcreator` 固定伺服器角色|  
|建立新的 Oracle CDC 執行個體。|`db_datareader` 角色<br /><br /> `db_owner` 角色。|  
|取得部署指令碼。|`db_datareader` 和 `db_datawriter` 角色<br /><br /> `db_owner` 角色|  
|變更組態及加入/移除擷取執行個體。|`db_datareader` 和 `db_datawriter` 角色<br /><br /> `db_owner` 角色|  
  
## <a name="see-also"></a>另請參閱  
 [存取 CDC 設計工具主控台](../../integration-services/change-data-capture/access-the-cdc-designer-console.md)   
 [用來建立執行個體的 SQL Server 連接](../../integration-services/change-data-capture/sql-server-connection-for-instance-creation.md)  
  
  
