---
title: "以最低組態啟動 SQL Server | Microsoft Docs"
ms.custom: 
ms.date: 01/20/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- minimal configuration [SQL Server]
- starting SQL Server, minimal configuration
ms.assetid: 4d733c99-28b3-42d8-b7f6-7b943b548173
caps.latest.revision: "27"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: f7d4d86a17896a7b79bc0e920585afa81d462869
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/09/2017
---
# <a name="start-sql-server-with-minimal-configuration"></a>以最低組態啟動 SQL Server
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  如果因組態問題而無法啟動伺服器，您可以使用最低組態啟動選項來啟動 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的執行個體。 此為啟動選項 **-f**。 以最低組態啟動 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的執行個體，會自動將伺服器設定為單一使用者模式。  
  
 以最低組態模式啟動 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體時，請注意下列事項：  
  
-   只有一位使用者可以連接，而且不會執行 `CHECKPOINT` 處理序。  
  
-   會關閉遠端存取與預先讀取 (Read-ahead) 功能。  
  
-   不會執行啟動預存程序。  

-   `tempdb` 已設定最小可能大小。
  
 在伺服器以最低組態啟動後，您應該變更適當的伺服器選項值，然後將伺服器停止，再重新啟動。  
  
> [!IMPORTANT]  
>  使用 **sqlcmd** 公用程式與專用管理員連接 (DAC) 連接到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。 如果您使用一般連接，請先停止 SQL Server Agent 服務，再以最低組態模式連接到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的執行個體。 否則，SQL Server Agent 服務會使用連接，從而將其封鎖。  
  
## <a name="see-also"></a>另請參閱  
 [啟動、停止或暫停 SQL Server Agent 服務](http://msdn.microsoft.com/library/c95a9759-dd30-4ab6-9ab0-087bb3bfb97c)   
 [資料庫管理員的診斷連接](../../database-engine/configure-windows/diagnostic-connection-for-database-administrators.md)   
 [sqlcmd 公用程式](../../tools/sqlcmd-utility.md)   
 [伺服器組態選項 &#40;SQL Server&#41;](../../database-engine/configure-windows/server-configuration-options-sql-server.md)   
 [sp_configure &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md)   
 [資料庫引擎服務啟動選項](../../database-engine/configure-windows/database-engine-service-startup-options.md)  
  
  
