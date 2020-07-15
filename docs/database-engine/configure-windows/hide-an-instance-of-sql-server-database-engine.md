---
title: 隱藏 SQL Server 資料庫引擎的執行個體 | Microsoft Docs
description: 了解如何隱藏 SQL Server Database Engine 的執行個體。 用戶端電腦無法使用 SQL Server Browser 服務來尋找隱藏的執行個體。
ms.custom: ''
ms.date: 08/19/2015
ms.prod: sql
ms.prod_service: high-availability
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
helpviewer_keywords:
- Database Engine [SQL Server], hiding instances
- hiding instances of Database Engine
ms.assetid: 392de21a-57fa-4a69-8237-ced8ca86ed1d
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 5be741205c17d32e9a2ddb253574c8dd50e4c4fe
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/01/2020
ms.locfileid: "85772445"
---
# <a name="hide-an-instance-of-sql-server-database-engine"></a>隱藏 SQL Server Database Engine 的執行個體
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  此主題描述如何使用 SQL Server 組態管理員，在 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 中隱藏 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 執行個體。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Browser 服務來列舉電腦上安裝的 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 執行個體。 這可讓用戶端應用程式瀏覽伺服器，並可幫助用戶端區別同一部電腦上的多個 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 執行個體。 您可以使用下列程序防止 SQL Server Browser 服務向嘗試利用 [!INCLUDE[ssDE](../../includes/ssde-md.md)] [瀏覽] **按鈕尋找執行個體的用戶端電腦公開** 執行個體。  
  
##  <a name="using-sql-server-configuration-manager"></a><a name="SSMSProcedure"></a> 使用 SQL Server 組態管理員  
  
#### <a name="to-hide-an-instance-of-the-sql-server-database-engine"></a>若要隱藏 SQL Server Database Engine 的執行個體  
  
1.  在 [SQL Server 組態管理員] 中，展開 [SQL Server 網路組態]，然後以滑鼠右鍵按一下 [通訊協定] *\<server instance>* ，然後選取 [屬性]。  
  
2.  在 **[旗標]** 索引標籤的 **[HideInstance]** 方塊中，選取 **[是]** ，然後按一下 **[確定]** 關閉對話方塊。 此變更在新連接時會立即生效。  
  
## <a name="remarks"></a>備註  
 如果隱藏具名執行個體，將必須於連接字串中提供連接埠號碼，才可連接到隱藏的執行個體 (即使瀏覽器服務正在執行中亦然)。 建議您使用靜態連接埠，而不要使用具名隱藏執行個體的動態連接埠。  
  如需詳細資訊，請參閱[設定伺服器接聽特定 TCP 通訊埠 &#40;SQL Server 組態管理員&#41;](../../database-engine/configure-windows/configure-a-server-to-listen-on-a-specific-tcp-port.md)。  
  
### <a name="clustering"></a>叢集  
 如果隱藏叢集執行個體或可用性群組，則叢集服務可能無法連接到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。 而如此會導致叢集執行個體的 **IsAlive** 檢查失敗，且 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 會離線。 
 
若要避免這種情況，請在叢集執行個體的所有節點或所有本機可用性群組複本中都建立別名，以反映為該執行個體所設定的靜態連接埠。  舉例而言，在含有兩個複本的可用性群組中，針對節點 2 執行個體在節點 1 上建立別名，例如 `node-two\instancename`。 在節點 2 上，建立稱為 `node-one\instancename` 的別名。 這些別名是成功容錯移轉的必要項目。 
 
 如需詳細資訊，請參閱[建立或刪除用戶端使用的伺服器別名 &#40;SQL Server Configuration Manager&#41;](../../database-engine/configure-windows/create-or-delete-a-server-alias-for-use-by-a-client.md)。  
  
 如果隱藏了叢集具名執行個體，而當 **LastConnect** 登錄機碼 (**HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\MSSQLServer\Client\SNI11.0\LastConnect**) 與 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 目前接聽的連接埠有不同的連接埠時，叢集服務可能無法連接到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。 如果叢集服務將無法連接到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，可能會看到類似如下的錯誤：  
**事件識別碼：1001：事件名稱：容錯移轉叢集資源鎖死。**  
  
## <a name="see-also"></a>另請參閱  
 [伺服器網路組態](../../database-engine/configure-windows/server-network-configuration.md)   
 [SQL 虛擬伺服器用戶端連接的描述](https://support.microsoft.com/kb/273673)   
 [如何將靜態連接埠指派給 SQL Server 具名執行個體，並避免常見陷阱](https://blogs.msdn.com/b/arvindsh/archive/2012/09/08/how-to-assign-a-static-port-to-a-sql-server-named-instance-and-avoid-a-common-pitfall.aspx)  
  
  
