---
title: 安全性概觀 (Integration Services) | Microsoft Docs
ms.custom: security
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- SSIS packages, security
- Integration Services, security
- security [Integration Services], about security
- passwords [Integration Services]
- packages [Integration Services], security
- SQL Server Integration Services, security
- SSIS, security
- Integration Services packages, security
- SQL Server Integration Services packages, security
ms.assetid: 01aa0b88-d477-4581-9a3b-2efc3de2b133
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 67f27f17df5bf41f0b2b88265d0eb91df824a57c
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "65718119"
---
# <a name="security-overview-integration-services"></a>安全性概觀 (Integration Services)

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 中的安全性包含幾層，提供了豐富且具彈性的安全性環境。 這些安全性階層包括使用數位簽章、封裝屬性、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料庫角色，以及作業系統權限。 這些安全性功能中，絕大部分都屬於識別與存取控制的類別。  

## <a name="threat-and-vulnerability-mitigation"></a>威脅和弱點安全防護
  雖然 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 包含各種安全性機制，但是封裝以及封裝所建立或使用的檔案可能會遭到惡意使用者的利用。  
  
 下表將描述這些風險，以及您可採取來降低風險的主動式步驟。  
  
|威脅或弱點|定義|降低|  
|-----------------------------|----------------|----------------|  
|封裝來源|封裝的來源是指建立此封裝的個人或組織。 執行來自未知或不受信任來源的封裝可能會有風險。|使用數位簽章來識別封裝的來源，並且只執行來自已知且信任來源的封裝。 如需詳細資訊，請參閱 [使用數位簽章來識別封裝的來源](../../integration-services/security/identify-the-source-of-packages-with-digital-signatures.md)。|  
|封裝內容|封裝內容包括封裝中的元素及其屬性。 這些屬性可能會包含機密資料，例如密碼或連接字串。 SQL 陳述式等封裝元素可能會顯示資料庫的結構。|進行下列步驟來控制封裝及內容的存取權：<br /><br /> 1) 若要控制封裝本身的存取權，請將 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 安全性功能套用至儲存在 **執行個體之** msdb [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]資料庫中的封裝。 對於儲存在檔案系統中的封裝，請套用檔案系統安全性功能，例如存取控制清單 (ACL)。<br /><br /> 2) 若要控制封裝內容的存取權，請設定封裝的保護等級。<br /><br /> 如需詳細資訊，請參閱[安全性概觀 &#40;Integration Services&#41;](../../integration-services/security/security-overview-integration-services.md) 和[封裝中的敏感性資料存取控制](../../integration-services/security/access-control-for-sensitive-data-in-packages.md)。|  
|封裝輸出|當您將封裝設定成使用組態、檢查點和記錄時，此封裝就會在封裝外部儲存這項資訊。 儲存在封裝外部的資訊可能會包含機密資料。|若要保護封裝儲存至 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料庫資料表的組態和記錄，請使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 安全性功能。<br /><br /> 若要控制檔案的存取權，請使用檔案系統所提供的存取控制清單 (ACL)。<br /><br /> 如需詳細資訊，請參閱 [Access to Files Used by Packages](#files)|  
  
## <a name="identity-features"></a>識別功能  
 您可以透過在封裝中實作識別功能，藉以達到下列目標：  
  
 **確定您只會開啟和執行來自信任來源的封裝**。  
  
 為確保您只開啟和執行來自信任來源的封裝，您必須先識別封裝的來源。 您可以使用憑證簽署封裝，藉以識別來源。 接著，當您開啟或執行封裝時，可以讓 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 檢查數位簽章是否存在及其有效性。 如需詳細資訊，請參閱 [Identify the Source of Packages with Digital Signatures](../../integration-services/security/identify-the-source-of-packages-with-digital-signatures.md)(使用數位簽章識別封裝來源)。  
  
## <a name="access-control-features"></a>存取控制功能  
 您可以透過在封裝中實作識別功能，藉以達到下列目標：  
  
 **確定只有授權的使用者會開啟和執行封裝**。  
  
 為確保只有授權的使用者會開啟和執行封裝，您必須控制下列資訊的存取：  
  
-   控制封裝內容的存取，特別是敏感性資料。  
  
-   控制儲存在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]中之封裝和封裝組態的存取。  
  
-   控制封裝及相關檔案的存取，例如，儲存在檔案系統中的組態、記錄以及檢查點檔案。  
  
-   針對服務顯示在 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 中的封裝，控制 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]服務與相關資訊的存取。  
  
### <a name="controlling-access-to-the-contents-of-packages"></a>控制封裝內容的存取  
 為協助限制封裝內容的存取，您可以設定封裝的 ProtectionLevel 屬性來加密封裝。 您可以將此屬性設定為封裝所需的保護等級。 例如，在小組開發環境中，您可以使用僅處理封裝之小組成員知道的密碼來加密封裝。  
  
 當您設定封裝的 ProtectionLevel 屬性時， [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 會自動偵測機密屬性，並根據指定的封裝保護層級處理這些屬性。 例如，將封裝的 ProtectionLevel 屬性設定為以密碼加密機密資訊的層級。 對於此封裝， [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 會自動加密所有機密屬性的值，而且如果沒有提供正確的密碼，將不會顯示對應的資料。  
  
 如果屬性包含密碼或連接字串之類的資訊，或者如果屬性對應到變數或工作產生的 XML 節點， [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 通常會將這些屬性視為機密。 對於 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 是否將屬性視為機密，取決於 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 元件 (例如，連接管理員或工作) 的開發人員是否將該屬性指定為機密。 使用者無法將屬性加入到視為機密之屬性的清單，也無法從其中移除屬性。如果撰寫自訂工作、連接管理員或資料流程元件，您可以指定 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 應該將哪些屬性視為機密。  
  
 如需詳細資訊，請參閱 [Access Control for Sensitive Data in Packages](../../integration-services/security/access-control-for-sensitive-data-in-packages.md)。  
  
### <a name="controlling-access-to-packages"></a>控制封裝的存取  
 您可以將 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 封裝儲存到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]執行個體中的 msdb 資料庫，或將其儲存為檔案系統中的 XML 檔案，且其副檔名為 .dtsx。 如需詳細資訊，請參閱 [Save Packages](../../integration-services/save-packages.md)(儲存封裝)。  
  
#### <a name="saving-packages-to-the-msdb-database"></a>將封裝儲存到 msdb 資料庫  
 將封裝儲存至 msdb 資料庫有助於提供伺服器、資料庫和資料表層級的安全性。 在 msdb 資料庫中， [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 封裝是儲存在 sysssispackages 資料表中。 由於這些封裝會分別儲存到 msdb 資料庫中的 sysssispackages 和 sysdtspackages 資料表中，因此，當您備份 msdb 資料庫時，也會自動備份這些封裝。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 套用 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 資料庫層級角色還可以保護儲存在 msdb 資料庫的封裝。 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 包含以下三個固定資料庫層級角色：db_ssisadmin、db_ssisltduser 和 db_ssisoperator，可用於控制封裝的存取權。 讀取器和寫入器角色可以與每個封裝相關聯。 您也可以定義要在 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 封裝中使用的自訂資料庫層級角色。 這些角色只能在儲存至 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體中 msdb 資料庫的封裝上實作。 如需詳細資訊，請參閱 [Integration Services 角色 &#40;SSIS 服務&#41;](../../integration-services/security/integration-services-roles-ssis-service.md)。  
  
#### <a name="saving-packages-to-the-file-system"></a>將封裝儲存至檔案系統  
 如果您將封裝儲存到檔案系統，而非 msdb 資料庫中，請務必保護封裝檔案和包含封裝檔案的資料夾。  
  
### <a name="controlling-access-to-files-used-by-packages"></a>控制封裝所使用之檔案的存取  
 已設定為使用組態、檢查點和記錄的封裝會產生儲存在封裝之外的資訊。 此資訊可能是機密資訊，應該對其進行保護。 檢查點檔案只能儲存至檔案系統，但組態和記錄檔可以儲存至檔案系統或 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料庫中的資料表。 儲存至 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的組態和記錄檔受到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 安全性保護，但寫入檔案系統的資訊需要額外的安全性。  
  
 如需詳細資訊，請參閱 [Access to Files Used by Packages](#files)(存取封裝所使用的檔案)。  
  
#### <a name="storing-package-configurations-securely"></a>安全地儲存封裝組態  
 封裝組態可以儲存至 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料庫中的資料表或儲存至檔案系統。  
  
 組態可以儲存至任何 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料庫，而不只是儲存至 msdb 資料庫。 因此，您可以指定哪些資料庫要當做封裝組態的儲存機制。 您還可以指定要包含組態的資料表名稱，而 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 會自動使用正確的結構建立資料表。 將組態儲存至資料表可以提供伺服器、資料庫和資料表層級的安全性。 另外，儲存至 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的組態會在您備份資料庫時自動備份。  
  
 如果您將組態儲存在檔案系統，而非 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]中，請務必保護包含封裝組態檔的資料夾。  
  
 如需有關組態的詳細資訊，請參閱＜ [Package Configurations](../../integration-services/packages/package-configurations.md)＞。  
  
### <a name="controlling-access-to-the-integration-services-service"></a>控制 Integration Services 服務的存取  
 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 會使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 服務列出已儲存的封裝。 為防止未經授權的使用者檢視本機與遠端電腦上儲存之封裝的資訊，並藉以得知私人資訊，請限制對執行 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 服務之電腦的存取。  
  
 如需詳細資訊，請參閱 [授予 Integration Services 服務的權限](#service)。  

## <a name="files"></a> Access to Files Used by Packages
  封裝保護等級不會保護儲存於封裝之外的檔案。 這些檔案包括下列各項：  
  
-   組態檔  
  
-   檢查點檔案  
  
-   記錄檔  
  
 您必須分開保護這些檔案，尤其是當檔案中包含機密資訊時。  
  
### <a name="configuration-files"></a>組態檔  
 如果組態中含有機密資訊，例如登入和密碼資訊，則應考慮將組態儲存至 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]中，或使用存取控制清單 (ACL) 來限制對儲存檔案之位置或資料夾的存取權，且只允許特定帳戶擁有其存取權。 通常，您可以將存取權授與您允許執行封裝的帳戶，以及負責管理和疑難排解封裝的帳戶，其工作可能包括檢閱組態、檢查點和記錄檔的內容。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 提供更安全的儲存體，因為它可以提供伺服器和資料庫層級的保護。 若要將組態儲存至 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，您可以使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 組態類型。 若要儲存至檔案系統，則可以使用 XML 組態類型。  
  
 如需詳細資訊，請參閱 [封裝組態](../../integration-services/packages/package-configurations.md)、 [建立封裝組態](../../integration-services/packages/create-package-configurations.md)和 [SQL Server 安裝的安全性考量](../../sql-server/install/security-considerations-for-a-sql-server-installation.md)。  
  
### <a name="checkpoint-files"></a>檢查點檔案  
 同樣地，如果封裝使用的檢查點檔案包含機密資訊，應使用存取控制清單 (ACL) 來保護儲存檔案之位置或資料夾的安全。 檢查點檔案儲存有關封裝進度和目前變數值的目前狀態資訊。 例如，封裝可能包括含有電話號碼的自訂變數。 如需詳細資訊，請參閱 [使用檢查點來重新啟動封裝](../../integration-services/packages/restart-packages-by-using-checkpoints.md)。  
  
### <a name="log-files"></a>記錄檔  
 寫入檔案系統的記錄項目也應使用存取控制清單 (ACL) 保護其安全。 記錄項目還可以儲存於 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料表中，由 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 安全性進行保護。 記錄項目可能包含機密資訊，例如，如果封裝包含建構參考電話號碼之 SQL 陳述式的「執行 SQL」工作，SQL 陳述式的記錄項目便會包含電話號碼。 SQL 陳述式可能還顯示有關資料庫中資料表與資料行名稱的私用資訊。 如需詳細資訊，請參閱 [集成服務 &#40;SSIS&#41; 記錄](../../integration-services/performance/integration-services-ssis-logging.md)。  

## <a name="service"></a> 授予 Integration Services 服務的權限
  封裝保護等級可限制已獲允許編輯和執行封裝的人員。 您需要額外的保護措施來限制有誰能夠檢視目前在伺服器上執行的封裝清單，以及有誰能夠停止目前在 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]中執行的封裝。  
  
 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 會使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 服務列出正在執行封裝。 Windows Administrators 群組的成員可以檢視和停止所有目前正在執行封裝。 非 Administrators 群組成員的使用者只能檢視和停止他們所啟動的封裝。  
  
 限制存取執行 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 服務的電腦很重要，特別是可列舉遠端資料夾的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 服務。 任何已驗證的使用者都可以要求列舉封裝。 服務即使找不到該服務，仍會列舉資料夾。 這些資料夾名稱對惡意使用者可能很有用。 如果管理員已設定服務來列舉遠端電腦上的資料夾，則使用者還可查看他們通常無法看到的資料夾名稱。  

## <a name="related-tasks"></a>相關工作  
 下列清單所含的主題連結，將說明如何執行安全性相關特定工作。  
  
-   [建立使用者定義角色](../../integration-services/security/integration-services-roles-ssis-service.md#create)  
  
-   [指派讀取器和寫入器角色給封裝](../../integration-services/security/integration-services-roles-ssis-service.md#assign)  
  
-   [透過設定登錄值實作簽署原則](../../integration-services/security/identify-the-source-of-packages-with-digital-signatures.md#registry)  
  
-   [使用數位憑證來簽署封裝](../../integration-services/security/identify-the-source-of-packages-with-digital-signatures.md#cert)  
  
-   [設定或變更封裝的保護等級](../../integration-services/security/access-control-for-sensitive-data-in-packages.md#set_protection)  
