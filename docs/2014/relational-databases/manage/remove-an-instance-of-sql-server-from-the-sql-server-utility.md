---
title: 從 SQL Server 公用程式移除 SQL Server 執行個體 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- dbe-cross-instance
ms.tgt_pltfrm: ''
ms.topic: conceptual
f1_keywords:
- sql12.swb.utility.remove.f1
ms.assetid: ae1d126a-46d2-47bf-b339-17c743df6491
caps.latest.revision: 7
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: e7b657f69ae221044fcc0fa1211b21954b4ad1d0
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/02/2018
ms.locfileid: "37244618"
---
# <a name="remove-an-instance-of-sql-server-from-the-sql-server-utility"></a>從 SQL Server 公用程式移除 SQL Server 執行個體
  使用下列步驟可從 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 公用程式中移除 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的 Managed 執行個體。 這個程序會從 UCP 清單檢視中移除 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的執行個體，並停止 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 公用程式資料收集。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的執行個體則不會解除安裝。  
  
> [!IMPORTANT]  
>  在您使用這個程序從 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 公用程式中移除 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體之前，請確定 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 和 SQL Server Agent 服務正在要移除的執行個體上執行。  
  
1.  從 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 的公用程式總管上，按一下 [Managed 執行個體]。 在 [公用程式總管] 內容窗格上，觀察 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Managed 執行個體的清單檢視。  
  
2.  在清單檢視的 [SQL Server 執行個體名稱] 資料行中，選取要從 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 公用程式中移除的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體。 以滑鼠右鍵按一下要移除的執行個體，然後選取 [移除 Managed 執行個體]。  
  
3.  針對 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體指定具有系統管理員權限的認證：按一下 [連接]，並確認 [連接到伺服器] 對話方塊中的資訊，然後按一下 [連接]。 您將會在 [移除 Managed 執行個體] 對話方塊中看到登入資訊。  
  
4.  若要確認此作業，請按一下 [確定]。 若要結束此作業，請按一下 [取消]。  
  
## <a name="manually-remove-a-managed-instance-of-sql-server-from-a-sql-server-utility"></a>從 SQL Server 公用程式中手動移除 SQL Server 的 Managed 執行個體  
 這個程序會從 UCP 清單檢視中移除 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的執行個體，並停止 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 公用程式資料收集。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的執行個體則不會解除安裝。  
  
 使用 PowerShell，從 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 公用程式中移除 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的 Managed 執行個體。 此指令碼會執行下列作業：  
  
-   依據伺服器執行個體名稱取得 UCP。  
  
-   從 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 公用程式中移除 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的 Managed 執行個體。  
  
```  
# Get Ucp connection  
$UcpServerInstanceName = "ComputerName\InstanceName";  
$UtilityInstance = new-object –Type Microsoft.SqlServer.Management.Smo.Server $UcpServerInstanceName;  
$UcpConnection = new-object -Type Microsoft.SqlServer.Management.Sdk.Sfc.SqlStoreConnection $UtilityInstance.ConnectionContext.SqlConnectionObject;  
$Utility = [Microsoft.SqlServer.Management.Utility.Utility]::Connect($UcpConnection);  
  
# Now remove the ManagedInstance from the SQL Server Utility  
$ServerInstanceName = "ComputerName\InstanceName";  
$Instance = new-object -Type Microsoft.SqlServer.Management.Smo.Server $ServerInstanceName;  
$InstanceConnection = new-object -Type Microsoft.SqlServer.Management.Sdk.Sfc.SqlStoreConnection $Instance.ConnectionContext.SqlConnectionObject;  
$ManagedInstance = $Utility.ManagedInstances[$ServerInstanceName];  
$ManagedInstance.Remove($InstanceConnection);  
```  
  
 請注意，參考 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體名稱時，必須與儲存在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]中的形式一模一樣。 在區分大小寫的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體中，您必須使用 @@SERVERNAME 傳回的相同大小寫來指定執行個體名稱。 若要取得 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Managed 執行個體的執行個體名稱，請在 Managed 執行個體上執行這個查詢：  
  
```  
select @@SERVERNAME AS instance_name  
```  
  
 此時會從 UCP 中完全移除 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的 Managed 執行個體。 下次當您重新整理 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 公用程式的資料時，它就會從清單檢視中消失。 這個狀態表示使用者順利完成在 SSMS 使用者介面中移除 Managed 執行個體的作業。  
  
## <a name="see-also"></a>另請參閱  
 [使用公用程式總管來管理 SQL Server 公用程式](use-utility-explorer-to-manage-the-sql-server-utility.md)   
 [疑難排解 SQL Server 公用程式](../../database-engine/troubleshoot-the-sql-server-utility.md)  
  
  
