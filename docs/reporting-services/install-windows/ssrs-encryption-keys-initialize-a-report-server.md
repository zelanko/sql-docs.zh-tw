---
title: "初始化報表伺服器 （SSRS 組態管理員） |Microsoft 文件"
ms.custom: 
ms.date: 05/31/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- report servers [Reporting Services], initializing
- initialization process [Reporting Services]
- checking report server initializations
- scale-out deployments [Reporting Services]
- initializing report servers [Reporting Services]
- verifying report server initializations
ms.assetid: 861d4ec4-1085-412c-9a82-68869a77bd55
caps.latest.revision: 10
author: guyinacube
ms.author: asaxton
manager: erikre
ms.translationtype: Machine Translation
ms.sourcegitcommit: 0eb007a5207ceb0b023952d5d9ef6d95986092ac
ms.openlocfilehash: cca3d552a0e1ffb7fdfc09e98a334f8f4d196d84
ms.contentlocale: zh-tw
ms.lasthandoff: 06/22/2017

---
# <a name="ssrs-encryption-keys---initialize-a-report-server"></a>將報表伺服器的 SSRS 加密金鑰-初始化
  在 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]中，初始化的伺服器是可以在報表伺服器資料庫中加密和解密資料的伺服器。 初始化是報表伺服器作業的需求。 報表伺服器服務第一次啟動時，會進行初始化。 在您將報表伺服器聯結至現有的部署時，或者您在復原處理中手動重新建立金鑰時，也會進行初始化。 如需如何和為什麼使用加密金鑰的詳細資訊，請參閱[設定和管理加密金鑰 &#40;SSRS 組態管理員&#41;](../../reporting-services/install-windows/ssrs-encryption-keys-manage-encryption-keys.md) 和[儲存加密的報表伺服器資料 &#40;SSRS 組態管理員&#41;](../../reporting-services/install-windows/ssrs-encryption-keys-store-encrypted-report-server-data.md)。  
  
 加密金鑰有一部分是以報表伺服器服務的設定檔資訊為根據。 如果您變更用來執行報表伺服器服務的使用者識別，就必須隨之更新金鑰。 如果您是使用 Reporting Services 組態工具來變更識別，則會自動幫您處理這個步驟。  
  
 如果初始化因故失敗，報表伺服器就會傳回 **RSReportServerNotActivated** 錯誤，以回應使用者和服務要求。 在此情況下，您可能需要進行系統或伺服器組態的疑難排解。 如需詳細資訊，請參閱 Technet Wiki 中的 [SSRS: Troubleshoot Issues and Errors with Reporting Services](http://social.technet.microsoft.com/wiki/contents/articles/1633.aspx) (SSRS：疑難排解 Reporting Services 的問題和錯誤) (http://social.technet.microsoft.com/wiki/contents/articles/1633.aspx)。  
  
## <a name="overview-of-the-initialization-process"></a>初始化處理的概觀  
 初始化處理會建立和儲存用於加密的對稱金鑰。 對稱金鑰是由 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows 密碼編譯服務所建立，而報表伺服器服務隨後使用它來將資料加密和解密。 對稱金鑰本身是使用非對稱金鑰來加密。  
  
 下列步驟描述初始化處理：  
  
1.  初始啟動時，報表伺服器服務會讀取 RSReportServer.config 檔案，以取得安裝識別碼和資料庫連接資訊。  
  
2.  報表伺服器服務會從密碼編譯服務要求公開金鑰。 Windows 會建立一個私密和一個公開金鑰，並將公開金鑰傳送至報表伺服器服務。  
  
3.  報表伺服器服務會連接到報表伺服器資料庫，並且儲存安裝識別碼和公開金鑰值。  
  
4.  報表伺服器服務會再次呼叫密碼編譯服務，這次是要求對稱金鑰。 Windows 會建立對稱金鑰。  
  
5.  報表伺服器服務會再次連接到報表伺服器資料庫，並將對稱金鑰加入步驟 3 所儲存的公開金鑰和安裝識別碼值。 在儲存之前，報表伺服器服務會使用它的公開金鑰來加密對稱金鑰。 一旦對稱金鑰儲存之後，報表伺服器就視為已初始化，並且可供使用。  
  
## <a name="initializing-a-report-server-for-scale-out-deployment"></a>針對向外延展部署初始化報表伺服器  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 支援向外延展部署模型，這種模型會在多個報表伺服器執行個體中共用單一報表伺服器資料庫。 若要聯結向外延展部署，報表伺服器必須在共用資料庫中建立並儲存其對稱金鑰的副本。 雖然使用資料庫的所有伺服器會使用單一對稱金鑰，不過每個報表伺服器有其自己的金鑰副本。 每個複本都使用其擁有的公開金鑰唯一加密，因此各有不同。  
  
 針對向外延展部署初始化報表伺服器的第一組步驟，和針對單一伺服器與資料庫組合初始化的前三個步驟相同。  
  
 向外延展部署之初始化處理的不同之處在於報表伺服器取得對稱金鑰的方式。 第一個伺服器初始化後，會從 Windows 取得對稱金鑰。 第二部伺服器在向外延展部署的組態過程中初始化後，會從已經初始化的報表伺服器服務取得對稱金鑰。 第一個報表伺服器執行個體使用第二個執行個體的公開金鑰，來建立第二個報表伺服器執行個體之對稱金鑰的加密副本。 在此過程中的任何時候，對稱金鑰絕不會以純文字的形式公開。  
  
## <a name="how-to-initialize-a-report-server"></a>如何將報表伺服器初始化  
  
-   若要將報表伺服器初始化，請使用 Reporting Services 組態工具。 您建立和設定報表伺服器資料庫時，會自動進行初始化。 如需詳細資訊，請參閱[設定報表伺服器資料庫連接 &#40;SSRS 組態管理員&#41;](../../reporting-services/install-windows/configure-a-report-server-database-connection-ssrs-configuration-manager.md)。  
  
-   若要針對向外延展部署將報表伺服器初始化，您可以使用 Reporting Services 組態工具中的 [初始化] 頁面，或 **RSKeymgmt** 公用程式。 若要遵循逐步指示，請參閱[設定原生模式報表伺服器向外延展部署 &#40;SSRS 組態管理員&#41;](../../reporting-services/install-windows/configure-a-native-mode-report-server-scale-out-deployment.md)。  
  
> [!NOTE]  
>  **RSKeymgmt** 是一個主控台應用程式，您可以從主控屬於向外延展部署之報表伺服器執行個體之電腦上的命令列執行。 您執行公用程式時，要指定引數來選取您要初始化的遠端報表伺服器執行個體。  
  
 唯有安裝識別碼與公開金鑰之間有配對時，報表伺服器才會初始化。 如果配對成功，就會建立允許可回覆加密的對稱金鑰。 如果配對失敗，則會停用報表伺服器，這時系統應會要求您套用備份金鑰，或者刪除加密資料 (如果備份金鑰無法使用或無效)。 如需報表伺服器所使用之加密金鑰的詳細資訊，請參閱[設定和管理加密金鑰 &#40;SSRS 組態管理員&#41;](../../reporting-services/install-windows/ssrs-encryption-keys-manage-encryption-keys.md)。  
  
> [!NOTE]  
>  您也可以使用 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] Windows Management Instrumentation (WMI) 提供者，以程式設計方式將報表伺服器初始化。 如需詳細資訊，請參閱《 [線上叢書》中的](../../reporting-services/tools/access-the-reporting-services-wmi-provider.md) 存取 Reporting Services WMI 提供者 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 。  
  
## <a name="how-to-confirm-a-report-server-initialization"></a>如何確認報表伺服器初始化  
 若要確認報表伺服器初始化，請輸入 ping 報表伺服器 Web 服務**http://\<伺服器名稱 > / reportserver**命令視窗中。 如果發生 **RSReportServerNotActivated** 錯誤，初始化就會失敗。  
  
## <a name="see-also"></a>另請參閱
[設定和管理加密金鑰 (SSRS 組態管理員)](../../reporting-services/install-windows/ssrs-encryption-keys-manage-encryption-keys.md)
  
  

