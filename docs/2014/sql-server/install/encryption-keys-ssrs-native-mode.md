---
title: 加密金鑰 （SSRS 原生模式） |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
f1_keywords:
- SQL12.rsconfigtool.encryptionkeypanel.F1
ms.assetid: cc7e6f84-80e1-4b5e-9409-d0e074edd147
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: 16ac264f89c541f0a864f8b47ed008fa254f181c
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "66095420"
---
# <a name="encryption-keys-ssrs-native-mode"></a>加密金鑰 (SSRS 原生模式)
  使用 [加密金鑰] 頁面，即可管理用來加密和解密報表伺服器中之資料的對稱金鑰。 管理加密金鑰是報表伺服器組態之很重要的一部分。 當您建立報表伺服器資料庫時，就會自動建立並套用對稱金鑰。 請建立對稱金鑰的備份副本，以便執行例行維護作業。 您必須擁有對稱金鑰的有效副本，才能執行下列維護工作：  
  
-   變更報表伺服器服務的服務帳戶。  
  
-   將 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 安裝移轉到不同的電腦。  
  
-   設定新的報表伺服器執行個體，來共用或使用現有的報表伺服器資料庫。  
  
 [!INCLUDE[applies](../../includes/applies-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 原生模式。  
  
> [!IMPORTANT]  
>  定期變更 Reporting Services 加密金鑰是安全性最佳作法。 建議您在進行 Reporting Services 的主要版本升級之後，立即變更金鑰。 在升級之後變更金鑰可將升級循環以外，由變更 Reporting Services 加密金鑰所造成的其他服務中斷減至最少。  
  
 如果您更新了報表伺服器服務的使用者帳戶 (並且使用 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 組態管理員以外的工具來變更帳戶)，或者如果您將報表伺服器安裝移轉至新的伺服器，就必須還原對稱金鑰。  
  
 為了保護對稱金鑰不受未經授權的存取，將會使用報表伺服器服務的私密金鑰來加密對稱金鑰。 只有報表伺服器服務能夠解除鎖定並使用對稱金鑰，以便在報表伺服器資料庫中儲存敏感性資料。 如果您變更報表伺服器服務的識別或者將報表伺服器移轉至新電腦，報表伺服器服務的私密金鑰就無法再解除對稱金鑰的鎖定。 若要還原對稱金鑰的存取，請使用新報表伺服器服務識別的私密金鑰來重新加密對稱金鑰。 重新加密可藉由還原對稱金鑰這個處理序而進行。  
  
 只有在對稱金鑰與目前用來在報表伺服器資料庫中加密和解密資料的金鑰相同時，才應還原對稱金鑰。 如果還原的對稱金鑰無效，您就無法再存取敏感性資料。 在這種情況下，請先刪除金鑰，然後再重新建立。  
  
> [!IMPORTANT]  
>  刪除和重新建立對稱金鑰的動作無法反轉或恢復。 刪除或重新建立金鑰可能會對您目前的安裝造成重大的影響。 如果您刪除金鑰，將會一併刪除對稱金鑰所加密的任何現有資料。 刪除的資料包括外部報表資料來源的連接字串、預存連接字串和一些訂閱資訊。  
  
 若要開啟此頁面，請啟動 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 組態管理員，並在導覽窗格中選取此連結。 如需詳細資訊，請參閱 [Reporting Services 組態管理員 &#40;原生模式&#41;](../../../2014/sql-server/install/reporting-services-configuration-manager-native-mode.md)。  
  
## <a name="options"></a>選項  
 **備份**  
 將對稱金鑰複製到您指定的檔案。 對稱金鑰絕不會以純文字的方式儲存。 您必須輸入密碼來保護該檔案。  
  
 **Restore**  
 將對稱金鑰先前儲存的副本套用到報表伺服器資料庫。 您必須提供密碼來解除鎖定該檔案。  
  
 您目前連接到報表伺服器執行個體之對稱金鑰的先前副本，已用還原的版本加以覆寫。 還原對稱金鑰之後，您必須初始化使用報表伺服器資料庫的所有報表伺服器。 如需有關初始化報表伺服器的詳細資訊，請參閱 <<c0> [ 報表伺服器初始化&#40;SSRS 組態管理員&#41;](../../reporting-services/install-windows/ssrs-encryption-keys-initialize-a-report-server.md)。</c0>  
  
 **變更**  
 重新建立對稱金鑰，並重新加密報表伺服器資料庫中的所有加密值。 請務必在重新建立對稱金鑰之前，先停止報表伺服器服務。  
  
 在向外延展部署中，對稱金鑰的所有副本都已用較新的版本取代。 變更對稱金鑰之前，請確定要檢閱已聯結至向外延展部署之伺服器的清單，來確認唯有有效的報表伺服器執行個體，才能夠存取新的金鑰。 成為向外延展部署之一部分的伺服器會列在 **[向外延展部署]** 頁面中。 重新建立金鑰之前，請先停止部署中每一部報表伺服器上的服務。  
  
 請注意，如果您有許多資料來源和訂閱，重新產生對稱金鑰可能是一個長時間執行的處理序。  
  
 **刪除**  
 刪除對稱金鑰和所有加密的內容，其中包含連接字串和預存認證。 如果您無法還原對稱金鑰，就應只刪除該金鑰。  
  
 刪除對稱金鑰之後，您必須重新輸入遺漏的連接字串和報表中的預存認證，以及不再具有這些值的共用資料來源。 您也必須更新使用儲存加密資料之傳遞延伸模組的所有訂閱。 其中包含檔案共用傳遞延伸模組，以及使用加密值的任何協力廠商傳遞延伸模組。  
  
 沒有自動的方式能更新此資訊。 使用預存認證和連接字串的每個報表、訂閱以及共用資料來源，都必須一次更新一個。  
  
## <a name="see-also"></a>另請參閱  
 [Reporting Services 組態管理員 F1 說明主題&#40;SSRS 原生模式&#41;](../../../2014/sql-server/install/reporting-services-configuration-manager-f1-help-topics-ssrs-native-mode.md)   
 [備份與還原 Reporting Services 加密金鑰](../../reporting-services/install-windows/ssrs-encryption-keys-back-up-and-restore-encryption-keys.md)   
 [刪除和重新建立加密金鑰 &#40;SSRS 組態管理員&#41;](../../reporting-services/install-windows/ssrs-encryption-keys-delete-and-re-create-encryption-keys.md)   
 [將報表伺服器初始化 &#40;SSRS 組態管理員&#41;](../../reporting-services/install-windows/ssrs-encryption-keys-initialize-a-report-server.md)   
 [儲存加密的報表伺服器資料 &#40;SSRS 組態管理員&#41;](../../reporting-services/install-windows/ssrs-encryption-keys-store-encrypted-report-server-data.md)  
  
  
