---
title: 向外延展部署（原生模式報表伺服器） |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
f1_keywords:
- SQL12.rsconfigtool.scaleoutdeployment.F1
ms.assetid: 4df38294-6f9d-4b40-9f03-1f01c1f0700c
author: maggiesMSFT
ms.author: maggies
manager: craigg
ms.openlocfilehash: a9fe82102df73ddfa77b4636dd29793ac2694949
ms.sourcegitcommit: ffe2fa1b22e6040cdbd8544fb5a3083eed3be852
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/04/2019
ms.locfileid: "71952423"
---
# <a name="scale-out-deployment-native-mode-report-server"></a>向外延展部署 (原生模式報表伺服器)
  請使用 **組態管理員中的** [向外延展部署] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 頁面檢視向外延展部署的初始化狀態，或將報表伺服器聯結到向外延展部署。 *「向外延展部署」* (Scale-out Deployment) 是指共用單一報表伺服器資料庫的兩個或多個報表伺服器執行個體。  
  
 [!INCLUDE[applies](../../includes/applies-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 原生模式。  
  
 *「已初始化的報表伺服器」* (Initialized Report Server) 會描述可加密和解密儲存在報表伺服器資料庫中之敏感性資料的伺服器 (例如，預存認證和連接字串都是儲存於資料庫中之加密資料的範例)。 報表伺服器初始化是報表伺服器作業的需求。  
  
 *「向外延展部署」* (Scale-out Deployment) 的使用案例如下：  
  
-   這是讓伺服器叢集內的多部報表伺服器負載平衡的必要條件。 在您可以讓多部報表伺服器負載平衡之前，您必須先設定這些伺服器，讓它們共用相同的報表伺服器資料庫。  
  
-   若要在不同的電腦上分割報表伺服器應用程式，則使用一部伺服器來處理互動式報表，並使用另一部伺服器來處理已排程報表。 在此狀況下，每一個伺服器執行個體都會針對共用報表伺服器資料庫內儲存的相同報表伺服器內容來處理不同類型的要求。  
  
 若要設定向外延展部署，請從兩個或多個全都連接到相同報表伺服器資料庫的報表伺服器執行個體開始。 在安裝所有的執行個體之後，您會連接到第一部報表伺服器，然後使用 [向外延展部署] 頁面來加入其他每一個執行個體。 只有已經初始化來使用資料庫的報表伺服器才可以初始化其他節點。  
  
 若要開啟此頁面，請啟動 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 組態管理員，並選取導覽窗格中的 **[向外延展部署]** 。 如需詳細資訊，請參閱 [Reporting Services 組態管理員 &#40;原生模式&#41;](../../../2014/sql-server/install/reporting-services-configuration-manager-native-mode.md)。  
  
## <a name="options"></a>選項。  
 **SQL Server 名稱**  
 指定主控報表伺服器資料庫的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssDE](../../includes/ssde-md.md)] 執行個體名稱。  
  
 **Database Name**  
 指定報表伺服器執行個體目前連接的資料庫名稱。  
  
 **伺服器模式**  
 顯示伺服器模式和資料庫。 伺服器模式為原生模式或 SharePoint 整合模式。 這兩種模式都支援向外延展部署。  
  
 **[伺服器]**  
 顯示報表伺服器名稱。 在大多數情況下，這就是安裝報表伺服器的電腦名稱。  
  
 **執行個體**  
 顯示報表伺服器執行個體名稱。 報表伺服器執行個體是以 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體為基礎。  
  
 **狀態**  
 指示要初始化報表伺服器，還是等候加入向外延展部署：  
  
-   如果是不屬於向外延展部署之一部分的獨立報表伺服器，此頁面會顯示報表伺服器執行個體取決於它的專用報表伺服器資料庫來進行初始化。 狀態設定為 **[已加入]** 。  
  
-   如果是等候加入向外延展部署的報表伺服器，此頁面的 [伺服器]、[執行個體] 和 [狀態] 都會是空的值。 如果您選取了已經由另一個報表伺服器執行個體所使用的現有報表伺服器資料庫，則報表伺服器會等候加入向外延展部署。 此頁面上的訊息會指示您連接到已加入此伺服陣列的報表伺服器。 若要完成此要求，請按一下 **[連接]** ，並選取已初始化來使用報表伺服器資料庫的報表伺服器，再按一下 **[向外延展部署]** ，然後選取 **[正在等候加入]** 的報表伺服器執行個體，再按一下 **[初始化]** 。  
  
-   如果報表伺服器目前是向外延展部署的一部分，此頁面會顯示共用相同報表伺服器資料庫之所有報表伺服器執行個體的初始化狀態。 檢視向外延展部署的狀態時，不論您連接的是哪個伺服器都不會有影響。 向外延展部署中的所有節點都會報告相同的狀態資訊。  
  
     如果報表伺服器已經是向外延展部署的一部分，您可以使用此頁面來加入或移除節點。  
  
 **Initialize**  
 按一下 **[初始化]** ，將報表伺服器加入向外延展部署中。 這個步驟會設定報表伺服器在共用報表伺服器資料庫中使用對稱金鑰。 您可以使用 **[初始化]** 將報表伺服器執行個體加入向外延展部署中，或疑難排解移轉或安裝問題。  
  
 只有在先前已設定共用報表伺服器資料庫的連接時，您才可以使用報表伺服器執行個體。 此外，您必須從已初始化為使用報表伺服器資料庫的報表伺服器中執行初始化。  
  
 **移除**  
 按一下 **[移除]** ，即可從報表伺服器資料庫移除選取之報表伺服器執行個體的加密金鑰。 您可以移除金鑰，以便從向外延展部署中移除報表伺服器，或疑難排解移轉或安裝問題。 如果使用此選項，只會移除指定報表伺服器執行個體的加密金鑰。 報表伺服器資料庫中的加密資料並不會受到影響。  
  
 做為預防措施，在移除對稱金鑰之前，請先為其建立備份副本。 移除清單中最後一個報表伺服器的加密金鑰之後，該資料庫任何後續的報表伺服器初始化將導入新需求。 這項新需求是初始化報表伺服器之後，您必須還原對稱金鑰的備份副本。 如果您要存取目前報表伺服器資料庫中的加密資料，就必須還原對稱金鑰。  
  
 如果您不再需要加密資料，或者如果您沒有金鑰的備份副本，則必須刪除加密資料。 如需詳細資訊，請參閱[加密金鑰&#40;SSRS&#41;原生模式](../../../2014/sql-server/install/encryption-keys-ssrs-native-mode.md)。  
  
## <a name="see-also"></a>另請參閱  
 [初始化報表伺服器 &#40;SSRS 組態管理員&#41;](../../reporting-services/install-windows/ssrs-encryption-keys-initialize-a-report-server.md)   
 [設定和管理加密金鑰 &#40;SSRS 組態管理員&#41;](../../reporting-services/install-windows/ssrs-encryption-keys-manage-encryption-keys.md)   
 [設定原生模式報表伺服器向外延展部署 &#40;SSRS 組態管理員&#41;](../../reporting-services/install-windows/configure-a-native-mode-report-server-scale-out-deployment.md)  
  
  
