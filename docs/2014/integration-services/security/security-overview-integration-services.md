---
title: 安全性概觀 (Integration Services) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- integration-services
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
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 6ee84e7cd1e8d652283eb758af7396257fecf7b4
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/02/2018
ms.locfileid: "48228578"
---
# <a name="security-overview-integration-services"></a>安全性概觀 (Integration Services)
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 中的安全性包含幾層，提供了豐富且具彈性的安全性環境。 這些安全性階層包括使用數位簽章、封裝屬性、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料庫角色，以及作業系統權限。 這些安全性功能中，絕大部分都屬於識別與存取控制的類別。  
  
## <a name="identity-features"></a>識別功能  
 您可以透過在封裝中實作識別功能，藉以達到下列目標：  
  
 **確定您只會開啟和執行來自信任來源的封裝**。  
  
 為確保您只開啟和執行來自信任來源的封裝，您必須先識別封裝的來源。 您可以使用憑證簽署封裝，藉以識別來源。 接著，當您開啟或執行封裝時，可以讓 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 檢查數位簽章是否存在及其有效性。 如需詳細資訊，請參閱 [Identify the Source of Packages with Digital Signatures](identify-the-source-of-packages-with-digital-signatures.md)(使用數位簽章識別封裝來源)。  
  
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
  
 如需詳細資訊，請參閱 [Access Control for Sensitive Data in Packages](access-control-for-sensitive-data-in-packages.md)。  
  
### <a name="controlling-access-to-packages"></a>控制封裝的存取  
 您可以將 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 封裝儲存到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]執行個體中的 msdb 資料庫，或將其儲存為檔案系統中的 XML 檔案，且其副檔名為 .dtsx。 如需詳細資訊，請參閱 [Save Packages](../save-packages.md)(儲存封裝)。  
  
#### <a name="saving-packages-to-the-msdb-database"></a>將封裝儲存到 msdb 資料庫  
 將封裝儲存至 msdb 資料庫有助於提供伺服器、資料庫和資料表層級的安全性。 在 msdb 資料庫中， [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 封裝是儲存在 sysssispackages 資料表中。 由於這些封裝會分別儲存到 msdb 資料庫中的 sysssispackages 和 sysdtspackages 資料表中，因此，當您備份 msdb 資料庫時，也會自動備份這些封裝。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 套用 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 資料庫層級角色還可以保護儲存在 msdb 資料庫的封裝。 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 包含以下三個固定資料庫層級角色：db_ssisadmin、db_ssisltduser 和 db_ssisoperator，可用於控制封裝的存取權。 讀取器和寫入器角色可以與每個封裝相關聯。 您也可以定義要在 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 封裝中使用的自訂資料庫層級角色。 這些角色只能在儲存至 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體中 msdb 資料庫的封裝上實作。 如需詳細資訊，請參閱 [Integration Services 角色 &#40;SSIS 服務&#41;](integration-services-roles-ssis-service.md)。  
  
#### <a name="saving-packages-to-the-file-system"></a>將封裝儲存至檔案系統  
 如果您將封裝儲存到檔案系統，而非 msdb 資料庫中，請務必保護封裝檔案和包含封裝檔案的資料夾。  
  
### <a name="controlling-access-to-files-used-by-packages"></a>控制封裝所使用之檔案的存取  
 已設定為使用組態、檢查點和記錄的封裝會產生儲存在封裝之外的資訊。 此資訊可能是機密資訊，應該對其進行保護。 檢查點檔案只能儲存至檔案系統，但組態和記錄檔可以儲存至檔案系統或 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料庫中的資料表。 儲存至 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的組態和記錄檔受到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 安全性保護，但寫入檔案系統的資訊需要額外的安全性。  
  
 如需詳細資訊，請參閱 [Access to Files Used by Packages](../access-to-files-used-by-packages.md)(存取封裝所使用的檔案)。  
  
#### <a name="storing-package-configurations-securely"></a>安全地儲存封裝組態  
 封裝組態可以儲存至 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料庫中的資料表或儲存至檔案系統。  
  
 組態可以儲存至任何 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料庫，而不只是儲存至 msdb 資料庫。 因此，您可以指定哪些資料庫要當做封裝組態的儲存機制。 您還可以指定要包含組態的資料表名稱，而 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 會自動使用正確的結構建立資料表。 將組態儲存至資料表可以提供伺服器、資料庫和資料表層級的安全性。 另外，儲存至 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的組態會在您備份資料庫時自動備份。  
  
 如果您將組態儲存在檔案系統，而非 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]中，請務必保護包含封裝組態檔的資料夾。  
  
 如需有關組態的詳細資訊，請參閱＜ [Package Configurations](../package-configurations.md)＞。  
  
### <a name="controlling-access-to-the-integration-services-service"></a>控制 Integration Services 服務的存取  
 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 會使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 服務列出已儲存的封裝。 為防止未經授權的使用者檢視本機與遠端電腦上儲存之封裝的資訊，並藉以得知私人資訊，請限制對執行 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 服務之電腦的存取。  
  
 如需詳細資訊，請參閱 [授予 Integration Services 服務的權限](../access-to-the-integration-services-service.md)。  
  
## <a name="related-tasks"></a>相關工作  
 下列清單所含的主題連結，將說明如何執行安全性相關特定工作。  
  
-   [建立使用者定義角色](../create-a-user-defined-role.md)  
  
-   [指派讀取器和寫入器角色給套件](../assign-a-reader-and-writer-role-to-a-package.md)  
  
-   [透過設定登錄值實作簽署原則](../implement-a-signing-policy-by-setting-a-registry-value.md)  
  
-   [使用數位憑證來簽署封裝](../sign-a-package-by-using-a-digital-certificate.md)  
  
-   [設定或變更套件的保護等級](../set-or-change-the-protection-level-of-packages.md)  
  
## <a name="see-also"></a>另請參閱  
 [SQL Server Integration Services](../sql-server-integration-services.md)  
  
  
