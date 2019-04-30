---
title: 新增和移除向外延展部署 （SSRS 組態管理員） 的加密金鑰 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: conceptual
helpviewer_keywords:
- encryption keys [Reporting Services]
- deleting encryption keys
- removing encryption keys
- adding encryption keys
- rskeymgmt utility
- scale-out deployments [Reporting Services]
ms.assetid: 2da86fb3-4b4d-407f-9825-74dcc42486f5
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 52ecac095d34882d8f65cdafaa83784aef86e2fc
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "63261553"
---
# <a name="add-and-remove-encryption-keys-for-scale-out-deployment-ssrs-configuration-manager"></a>加入和移除向外延展部署的加密金鑰 (SSRS 組態管理員)
  您可以設定多部報表伺服器來使用共用報表伺服器資料庫，以便在向外延展部署模型中執行 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]。 向外延展部署的成員資格，會依報表伺服器是否在報表伺服器資料庫中儲存加密金鑰而定。 您可以加入和移除特定報表伺服器執行個體的加密金鑰，來控制向外延展部署成員資格。 如果您要從部署中移除節點，您可以依照任何順序來移除它們。 如果您要將節點加入部署中，您必須從已屬於部署的報表伺服器聯結任何新的執行個體。  
  
## <a name="using-the-reporting-services-configuration-tool-to-configure-scale-out-deployment"></a>使用 Reporting Services 組態工具設定向外延展部署  
 設定向外延展部署的最容易的方式，是使用 Reporting Services 組態工具。 如需詳細資訊和逐步指示，請參閱[設定原生模式報表伺服器向外延展部署 &#40;SSRS 設定管理員&#41;](configure-a-native-mode-report-server-scale-out-deployment.md)。  
  
## <a name="using-rskeymgmt-to-configure-scale-out-deployment"></a>使用 Rskeymgmt 設定向外延展部署  
 使用 **rskeymgmt** 公用程式初始化報表伺服器執行個體，以使用共用報表伺服器資料庫。 將報表伺服器加入向外延展部署，需要將報表伺服器初始化。 初始化需要管理員權限。 您必須擁有遠端電腦的管理員認證，且該電腦主控您要聯結至部署的報表伺服器。  
  
#### <a name="how-to-join-a-report-server-to-a-scale-out-deployment-rskeymgmt"></a>如何將報表伺服器聯結至向外延展部署 (rskeymgmt)  
  
1.  在主控已經是報表伺服器向外延展部署成員之報表伺服器的電腦上，於本機執行 **rskeymgmt.exe** 。  
  
2.  使用 `-j` 引數，即可將報表伺服器聯結至報表伺服器資料庫。 使用 `-m` 和 `-n` 引數，即可指定您要加入部署中的遠端報表伺服器執行個體。 使用 `-u` 和 `-v` 引數，即可指定遠端電腦上的管理員帳戶。 如果您要利用相同電腦上的多個報表伺服器執行個體來建立向外延展部署，所用的語法稍有不同。 如需您應使用之語法的詳細資訊，請參閱 [rskeymgmt 公用程式 &#40;SSRS&#41;](../tools/rskeymgmt-utility-ssrs.md)。  
  
     下列範例說明，當您要將遠端報表伺服器聯結至向外延展部署 (如果您有遠端電腦的管理員權限，您可以省略認證) 時，您必須指定哪些引數：  
  
    ```  
    rskeymgmt -j -m <remotecomputer> -n <namedreportserverinstance> -u <administratoraccount> -v <administratorpassword>  
    ```  
  
#### <a name="how-to-remove-a-report-server-from-a-scale-out-deployment-rskeymgmt"></a>如何從向外延展部署移除報表伺服器 (rskeymgmt)  
  
1.  開啟您想要移除之報表伺服器的 rsreportserver.config 檔案，然後尋找安裝識別碼。 根據預設，這個檔案位於 Program Files\Microsoft SQL Server\MSSQL.*n*\Reporting Services\ReportServer)。  
  
     如果您已安裝單一執行個體，電腦上將只有一個 rsreportserver.config 檔。 如果您安裝多個 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 執行個體，請利用 Reporting Services 組態工具中的 [伺服器狀態] 頁面，尋找您要移除之報表伺服器的執行個體識別碼 (例如，MSSQL.2)。 儲存報表伺服器執行個體之程式檔案的資料夾名稱將以執行個體識別碼為基礎 (例如，Program Files\Microsoft SQL Server\MSSQL.2)。  
  
2.  執行 **rskeymgmt.exe**。 您可以在屬於報表伺服器向外延展部署的任何報表伺服器上執行。  
  
3.  使用 `-r` 引數，即可將報表伺服器執行個體從向外延展部署釋放。 下列範例說明您必須指定的引數：  
  
    ```  
    rskeymgmt -r <installation ID>  
    ```  
  
 雖然這些步驟會從向外延展部署中移除報表伺服器，但是它們不會解除安裝報表伺服器上的 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 執行個體。 在您從向外延展部署中移除報表伺服器之後，如果不再需要該伺服器上的 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] ，可以解除安裝該伺服器的 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 。 如需相關資訊，請參閱《[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 線上叢書》的[解除安裝現有的 SQL Server 執行個體 &#40;安裝程式&#41;](../../sql-server/install/uninstall-an-existing-instance-of-sql-server-setup.md)。  
  
## <a name="see-also"></a>另請參閱  
 [設定和管理加密金鑰 &#40;SSRS 組態管理員&#41;](ssrs-encryption-keys-manage-encryption-keys.md)   
 [初始化報表伺服器 &#40;SSRS 組態管理員&#41;](ssrs-encryption-keys-initialize-a-report-server.md)  
  
  
