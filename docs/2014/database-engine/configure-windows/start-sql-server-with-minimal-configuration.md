---
title: 以最低組態啟動 SQL Server | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
helpviewer_keywords:
- minimal configuration [SQL Server]
- starting SQL Server, minimal configuration
ms.assetid: 4d733c99-28b3-42d8-b7f6-7b943b548173
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: cf7065d064e322e45fb95a38aed514b2acfc714a
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "62756215"
---
# <a name="start-sql-server-with-minimal-configuration"></a>以最低組態啟動 SQL Server
  如果您的設定問題導致伺服器無法啟動，您可以使用最小設定啟動選項[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]來啟動的實例。 此為啟動選項 **-f**。 以最低組態啟動 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的執行個體，會自動將伺服器設定為單一使用者模式。  
  
 以最低組態模式啟動 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體時，請注意下列事項：  
  
-   只有一位使用者可以連接，而且不會執行 CHECKPOINT 處理序。  
  
-   會關閉遠端存取與預先讀取 (Read-ahead) 功能。  
  
-   不會執行啟動預存程序。  
  
 在伺服器以最低組態啟動後，您應該變更適當的伺服器選項值，然後將伺服器停止，再重新啟動。  
  
> [!IMPORTANT]  
>  使用 **sqlcmd** 公用程式與專用管理員連接 (DAC) 連接到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。 如果您使用一般連接，請先停止 SQL Server Agent 服務，再以最低組態模式連接到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的執行個體。 否則，SQL Server Agent 服務會使用連接，從而將其封鎖。  
  
## <a name="see-also"></a>另請參閱  
 [啟動、停止或暫停 SQL Server Agent 服務](../../ssms/agent/start-stop-or-pause-the-sql-server-agent-service.md)   
 [資料庫管理員的診斷連接](diagnostic-connection-for-database-administrators.md)   
 [sqlcmd 公用程式](../../tools/sqlcmd-utility.md)   
 [伺服器組態選項 &#40;SQL Server&#41;](server-configuration-options-sql-server.md)   
 [sp_configure &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-configure-transact-sql)   
 [Database Engine 服務啟動選項](database-engine-service-startup-options.md)  
  
  
