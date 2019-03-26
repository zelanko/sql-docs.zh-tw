---
title: SQL Server 連線所需的 CDC 服務權限 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: d9e968f9-180c-4fa0-a849-98f2b1942330
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 84037e98c5ff29465e46c247421bee65c4990174
ms.sourcegitcommit: 7ccb8f28eafd79a1bddd523f71fe8b61c7634349
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/20/2019
ms.locfileid: "58276987"
---
# <a name="sql-server-connection-required-permissions-for-the-cdc-service"></a>SQL Server 連接所需的 CDC 服務權限
  CDC 服務組態主控台需要與 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 之間的連接資訊，才能執行其工作。 本主題描述可以在 [連接到 SQL Server] 對話方塊中提供的資訊，以便設定與 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]的連接。  
  
 必要時會開啟 [連接到 SQL Server] 對話方塊，例如當 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 連接資訊無法取得時，或是當資訊存在但是連接沒有必要的權限時。  
  
 下表描述需要連接 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的各種工作以及 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 登入/使用者的必要權限。  
  
|工作|最小權限|  
|----------|-------------------------|  
|準備 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體。|`dbcreator` 固定伺服器角色|  
|建立 Oracle CDC 服務 SQL Server 登入，以供 Oracle CDC 服務使用。|`public` 固定伺服器角色|  
|建立 Oracle CDC 服務登入，以供在 MSXDBCDC 中註冊新服務使用。|`db_datareader` 和 `db_datawriter` 角色|  
|編輯 Oracle CDC 服務登入，以供在 MSXDBCDC 中更新服務註冊使用。|`db_datareader` 和 `db_datawriter` 角色|  
|刪除 Oracle CDC 服務登入，以供在 MSXDBCDC 中更新服務註冊使用。|`db_datareader` 和 `db_datawriter` 角色|  
  
## <a name="see-also"></a>另請參閱  
 [連接到 SQL Server](../../integration-services/change-data-capture/connection-to-sql-server.md)   
 [連接到 SQL Server 進行刪除](../../integration-services/change-data-capture/connection-to-sql-server-for-delete.md)  
  
  
