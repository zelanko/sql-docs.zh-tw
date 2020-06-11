---
title: 資料庫引擎設定-資料目錄 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
ms.assetid: 9b1fa0fc-623b-479a-afc3-4f13bd850487
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 641656bede6163e1630ef2b39c54ca931d8b6ec4
ms.sourcegitcommit: 18a7c77be31f9af92ad9d0d3ac5eecebe8eec959
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/26/2020
ms.locfileid: "83859723"
---
# <a name="database-engine-configuration---data-directories"></a>Database Engine 組態 - 資料目錄
  請使用此頁面來指定 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)][!INCLUDE[ssDE](../../includes/ssde-md.md)]程式和資料檔案的安裝位置。 根據安裝類型，支援的儲存體可能包括本機磁碟、共用儲存體或 SMB 檔案伺服器。  
  
 若要將 SMB 檔案共用指定為目錄，您必須手動輸入支援的 UNC 路徑。 不支援瀏覽 SMB 檔案共用。 以下是 SMB 檔案共用支援的 UNC 路徑格式： \\\Servername\ShareName\\....  
  
## <a name="stand-alone-instance-of-ssnoversion"></a>[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的獨立執行個體  
 下表列出 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 獨立執行個體支援的儲存類型，以及使用者可以在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 安裝期間設定的預設目錄。  
  
## <a name="ui-element-list"></a>UI 元素清單  
  
|Description|支援的儲存類型|預設目錄|建議|  
|-----------------|----------------------------|-----------------------|---------------------|  
|資料根目錄|本機磁片、SMB 檔案伺服器、共用儲存體<sup>1</sup>|C:\Program Files \\ [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] \| [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 安裝程式將會設定 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 目錄的 acl，並在設定過程中中斷繼承。|  
|使用者資料庫目錄|本機磁片、SMB 檔案伺服器、共用儲存體<sup>1</sup>|C:\Program Files \\ [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] \MSSQL12. \<InstanceID> \MSSQL\Data|使用者資料目錄的最佳作法取決於工作負載和效能需求。|  
|使用者資料庫記錄檔目錄|本機磁片、SMB 檔案伺服器、共用儲存體<sup>1</sup>|C:\Program Files \\ [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] \MSSQL12. \<InstanceID> \MSSQL\Data|請確定記錄檔目錄具有足夠的空間。|  
|暫存資料庫目錄|本機磁片、SMB 檔案伺服器、共用儲存體<sup>1</sup>|C:\Program Files \\ [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] \MSSQL12. \<InstanceID> \MSSQL\Data|暫存目錄的最佳作法取決於工作負載和效能需求。|  
|暫存資料庫記錄檔目錄|本機磁片、SMB 檔案伺服器、共用儲存體<sup>1</sup>|C:\Program Files \\ [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] \MSSQL12. \<InstanceID> \MSSQL\Data|請確定記錄檔目錄具有足夠的空間。|  
|備份目錄|本機磁片、SMB 檔案伺服器、共用儲存體<sup>1</sup>|C:\Program Files \\ [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] \MSSQL12. \<InstanceID> \MSSQL\Backup|請設定適當的權限來防止資料遺失，並且確定 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 服務的使用者帳戶具有足夠的權限，可寫入備份目錄。 不支援針對備份目錄使用對應的磁碟機。|  
  
 <sup>1</sup>雖然支援共用磁片，但並不建議您針對獨立實例使用此方法 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 。  
  
## <a name="failover-cluster-instance-of-ssnoversion"></a>[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 容錯移轉叢集執行個體  
 下表列出 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 容錯移轉叢集執行個體支援的儲存類型，以及使用者可以在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 安裝期間設定的預設目錄。  
  
|Description|支援的儲存類型|預設目錄|建議|  
|-----------------|----------------------------|-----------------------|---------------------|  
|資料根目錄|共用儲存體、SMB 檔案伺服器|\<磁碟機：>\Program Files\\[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]\\<br /><br /> 秘訣：如果在 [叢集磁碟選取] **** 頁面上選取共用磁碟，預設為第一個共用磁碟。 如果在 **[叢集磁碟選取]** 頁面上沒有進行任何選擇，此欄位預設為空白。|進行組態設定時，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 安裝程式將會設定 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 目錄的 ACL 並中斷繼承。|  
|使用者資料庫目錄|共用儲存體、SMB 檔案伺服器|\<磁片磁碟機： >Program Files \\ [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] \MSSQL12. \<InstanceID> \MSSQL\Data<br /><br /> 秘訣：如果在 [叢集磁碟選取] **** 頁面上選取共用磁碟，預設為第一個共用磁碟。 如果在 **[叢集磁碟選取]** 頁面上沒有進行任何選擇，此欄位預設為空白。|使用者資料目錄的最佳作法取決於工作負載和效能需求。|  
|使用者資料庫記錄檔目錄|共用儲存體、SMB 檔案伺服器|\<磁片磁碟機： > \program Files \\ [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] \MSSQL12. \<InstanceID> \MSSQL\Data<br /><br /> 秘訣：如果在 [叢集磁碟選取] **** 頁面上選取共用磁碟，預設為第一個共用磁碟。 如果在 **[叢集磁碟選取]** 頁面上沒有進行任何選擇，此欄位預設為空白。|請確定記錄檔目錄具有足夠的空間。|  
|暫存資料庫目錄|本機磁碟、共用儲存體、SMB 檔案伺服器|\<磁片磁碟機： > \program Files \\ [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] \MSSQL12. \<InstanceID> \MSSQL\Data<br /><br /> 秘訣：如果在 [叢集磁碟選取] **** 頁面上選取共用磁碟，預設為第一個共用磁碟。 如果在 **[叢集磁碟選取]** 頁面上沒有進行任何選擇，此欄位預設為空白。|請確定指定的目錄對所有叢集節點都有效。 在容錯移轉期間，如果容錯移轉目標節點上的 tempdb 目錄無法使用，則 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資源將無法上線。|  
|暫存資料庫記錄檔目錄|本機磁碟、共用儲存體、SMB 檔案伺服器|\<磁片磁碟機： > \program Files \\ [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] \MSSQL12. \<InstanceID> \MSSQL\Data<br /><br /> 秘訣：如果在 [叢集磁碟選取] **** 頁面上選取共用磁碟，預設為第一個共用磁碟。 如果在 **[叢集磁碟選取]** 頁面上沒有進行任何選擇，此欄位預設為空白。|請確定指定的目錄對所有叢集節點都有效。 在容錯移轉期間，如果容錯移轉目標節點上的 tempdb 目錄無法使用，則 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資源將無法上線。|  
|備份目錄|本機磁碟、共用儲存體、SMB 檔案伺服器|\<磁片磁碟機： > \program Files \\ [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] \MSSQL12. \<InstanceID> \MSSQL\Backup<br /><br /> 秘訣：如果在 [叢集磁碟選取] **** 頁面上選取共用磁碟，預設為第一個共用磁碟。 如果在 **[叢集磁碟選取]** 頁面上沒有進行任何選擇，此欄位預設為空白。|請設定適當的權限來防止資料遺失，並且確定 SQL Server 服務的使用者帳戶具有足夠的權限，可寫入備份目錄。 不支援針對備份目錄使用對應的磁碟機。|  
  
## <a name="security-considerations"></a>安全性考量  
 進行組態設定時，安裝程式將會設定 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 目錄的 ACL 並中斷繼承。  
  
 以下建議適用於 SMB 檔案伺服器：  
  
-   如果使用 SMB 檔案伺服器， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 服務帳戶必須是網域帳戶。  
  
-   用於安裝 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的帳戶應該擁有當做資料目錄之 SMB 檔案共用資料夾的 FULL CONTROL NTFS 權限。  
  
-   用於安裝 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的帳戶應該具有 SMB 檔案伺服器的 SeSecurityPrivilege 權限。 若要授與此權限，請使用檔案伺服器上的 [本機安全性原則] 主控台，將 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 安裝程式帳戶新增至 **[管理稽核和安全性記錄檔]** 原則中。 在 **[本機安全性原則]** 主控台中 **[本機原則]** 下的 **[使用者權限指派]** 區段可以找到此設定。  
  
## <a name="notes"></a>注意  
  
-   將功能加入現有的安裝時，您不能變更先前安裝之功能的位置，也不能指定新功能的位置。  
  
-   如果您要指定非預設的安裝目錄，請確定安裝資料夾對於此 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]執行個體是唯一的。 此對話方塊上的任何目錄都不應該與其他 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]執行個體中的目錄共用。 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 執行個體內的 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 和 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 元件也應該安裝在不同的目錄中。  
  
-   程式檔和資料檔案無法安裝在下列位置中：  
  
    -   抽取式磁碟機  
  
    -   使用壓縮的檔案系統  
  
    -   系統檔案所在的目錄  
  
    -   容錯移轉叢集執行個體上的對應網路磁碟機  
  
## <a name="see-also"></a>另請參閱  
 [SQL Server 的預設和具名執行個體的檔案位置](../../../2014/sql-server/install/file-locations-for-default-and-named-instances-of-sql-server.md)   
 [檔案伺服器的共用及 NTSF 權限](https://go.microsoft.com/fwlink/?LinkID=206571)  
  
  
