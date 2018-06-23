---
title: 建立資料庫鏡像端點的 AlwaysOn 可用性群組 (SQL Server PowerShell) |Microsoft 文件
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- dbe-high-availability
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- Availability Groups [SQL Server], server instance
- Availability Groups [SQL Server], deploying
- Availability Groups [SQL Server], endpoint
ms.assetid: 6197bbe7-67d4-446d-ba5f-cabfa5df77f1
caps.latest.revision: 7
author: MikeRayMSFT
ms.author: mikeray
manager: jhubbard
ms.openlocfilehash: c9c2bba0d4a950e8db0159292947b629475df187
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36033954"
---
# <a name="create-a-database-mirroring-endpoint-for-alwayson-availability-groups-sql-server-powershell"></a>Create a Database Mirroring Endpoint for AlwaysOn Availability Groups (SQL Server PowerShell)
  此主題描述如何使用 PowerShell，在 [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] 中建立 [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] 所用的資料庫鏡像端點。  
  
 **本主題內容**  
  
-   **開始之前**  [安全性](#Security)  
  
-   **若要使用下列項目建立資料庫鏡像端點：**  [PowerShell](#PowerShellProcedure)  
  
## <a name="before-you-begin"></a>開始之前  
  
###  <a name="Security"></a> 安全性  
  
> [!IMPORTANT]  
>  RC4 演算法已被取代。 [!INCLUDE[ssNoteDepFutureDontUse](../../../includes/ssnotedepfuturedontuse-md.md)] 我們建議您改用 AES。  
  
####  <a name="Permissions"></a> 權限  
 需要 CREATE ENDPOINT 權限或系統管理員 (sysadmin) 固定伺服器角色的成員資格。 如需詳細資訊，請參閱 [GRANT 端點權限和 &#40;Transact-SQL&#41;](/sql/t-sql/statements/grant-endpoint-permissions-transact-sql)。  
  
##  <a name="PowerShellProcedure"></a> 使用 PowerShell  
 **若要建立資料庫鏡像端點**  
  
1.  將目錄切換到 (`cd`) 您要建立資料庫鏡像端點的伺服器執行個體。  
  
2.  使用 `New-SqlHadrEndpoint` 指令程式建立端點，然後使用 `Set-SqlHadrEndpoint` 啟動端點。  
  
###  <a name="PShellExample"></a> 範例 (PowerShell)  
 下列 PowerShell 命令會在 SQL Server 執行個體 (機器\\執行個體) 上建立資料庫鏡像端點。 此端點使用通訊埠 5022。  
  
> [!IMPORTANT]  
>  這個範例只適用於目前缺少資料庫鏡像端點的伺服器執行個體。  
  
```  
# Create the endpoint.  
$endpoint = New-SqlHadrEndpoint MyMirroringEndpoint -Port 5022 -Path SQLSERVER:\SQL\Machine\Instance  
  
# Start the endpoint  
Set-SqlHadrEndpoint -InputObject $endpoint -State "Started"  
  
```  
  
##  <a name="RelatedTasks"></a> 相關工作  
 **若要設定資料庫鏡像端點**  
  
-   [建立 Windows 驗證的資料庫鏡像端點 &#40;Transact-SQL&#41;](../../database-mirroring/create-a-database-mirroring-endpoint-for-windows-authentication-transact-sql.md)  
  
-   [使用資料庫鏡像端點憑證 &#40;Transact-SQL&#41;](../../database-mirroring/use-certificates-for-a-database-mirroring-endpoint-transact-sql.md)  
  
    -   [允許資料庫鏡像端點使用輸出連線的憑證 &#40;Transact-SQL&#41;](../../database-mirroring/database-mirroring-use-certificates-for-outbound-connections.md)  
  
    -   [允許資料庫鏡像端點使用輸入連線的憑證 &#40;Transact-SQL&#41;](../../database-mirroring/database-mirroring-use-certificates-for-inbound-connections.md)  
  
-   [指定伺服器網路位址 &#40;資料庫鏡像&#41;](../../database-mirroring/specify-a-server-network-address-database-mirroring.md)  
  
-   [在加入或修改可用性複本時指定端點 URL &#40;Transact-SQL&#41;](specify-endpoint-url-adding-or-modifying-availability-replica.md)  
  
 **若要檢視有關資料庫鏡像端點的資訊**  
  
-   [sys.database_mirroring_endpoints &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-database-mirroring-endpoints-transact-sql)  
  
## <a name="see-also"></a>另請參閱  
 [建立可用性群組 &#40;Transact-SQL&#41;](create-an-availability-group-transact-sql.md)   
 [AlwaysOn 可用性群組概觀&#40;SQL Server&#41;](overview-of-always-on-availability-groups-sql-server.md)  
  
  
