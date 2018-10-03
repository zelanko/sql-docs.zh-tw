---
title: 儲存加密的報表伺服器資料 (SSRS 設定管理員) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: conceptual
helpviewer_keywords:
- report servers [Reporting Services], encryption
- credentials [Reporting Services]
- cryptography [Reporting Services]
- confidential reports [Reporting Services]
- encryption [Reporting Services]
- databases [Reporting Services], encryption
ms.assetid: ac0f4d4d-fc4b-4c62-a693-b86e712e75f2
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: 19434a73f39e0701479f754b5af5dbe9ab4d8030
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/02/2018
ms.locfileid: "48149088"
---
# <a name="store-encrypted-report-server-data-ssrs-configuration-manager"></a>儲存加密的報表伺服器資料 (SSRS 組態管理員)
  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 會在報表伺服器資料庫和組態檔中儲存加密值。 大部份加密值是用於存取將資料提供給報表之外部資料來源的認證。 本主題將描述哪些值會進行加密、 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]中所使用的加密功能，以及您應該知道的其他預存機密資料類型。  
  
## <a name="encrypted-values"></a>加密值  
 下列清單將描述儲存在 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 安裝中的值。  
  
-   連接資訊和認證 - 可供報表伺服器連接到儲存內部伺服器資料的報表伺服器資料庫。  
  
     這些值是在安裝或報表伺服器組態過程中指定與加密。 您可以隨時使用 Reporting Services 組態工具或 **rsconfig** 公用程式，來更新連接資訊。 組態設定的加密，是以所有使用者都能使用之本機電腦的電腦層級金鑰執行。 加密的報表伺服器連接資訊，會儲存在 rsreportserver.config 檔案中 (其他組態檔並未包含加密的設定)。 如需詳細資訊，請參閱[設定報表伺服器資料庫連接 &#40;SSRS 組態管理員&#41;](../../sql-server/install/configure-a-report-server-database-connection-ssrs-configuration-manager.md)。  
  
-   預存認證 - 可供報表伺服器連接到將資料提供給報表的外部資料來源。  
  
     這些值是在您設定報表資料來源資訊時所定義的，然後以加密值的形式儲存在報表伺服器資料庫中。 報表伺服器會使用對稱金鑰，將此資料加密與解密。 如需有關預存認證的詳細資訊，請參閱 <<c0> [ 指定的認證和報表資料來源的連接資訊](../../integration-services/connection-manager/data-sources.md)在[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]線上叢書 》。  
  
-   自動使用者帳戶 - 可供報表伺服器連接到其他電腦，以擷取報表中使用的外部影像檔或外部資料。  
  
     當需要連接到遠端電腦，且無其他認證可用來進行該連接時，則必須使用此帳戶。 此帳戶主要用來支援不使用認證存取資料來源之報表的自動執行報表處理。 如果您是根據存取資料時不需要或不使用認證的資料來源建立報表，您必須將此帳戶設定為可供報表伺服器使用。  
  
     此帳戶在某些情況下需要，而且只能透過 Reporting Services 組態工具或 **rsconfig**建立。 此值也儲存在 rsreportserver.config 檔案中。 您必須手動建立此帳戶。 如需此帳戶和其使用方式的詳細資訊，請參閱[設定自動執行帳戶 &#40;SSRS 設定管理員&#41;](configure-the-unattended-execution-account-ssrs-configuration-manager.md)。  
  
-   用於加密的對稱金鑰。  
  
     此值是在安裝或伺服器組態過程中建立，然後以加密值形式儲存在報表伺服器資料庫中。 報表伺服器 Windows 服務會使用此金鑰，將儲存在報表伺服器資料庫中的資料加密與解密。  
  
## <a name="encryption-functionality-in-reporting-services"></a>Reporting Services 中的加密功能  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 會使用屬於 Windows 作業系統的加密函數。 對稱和非對稱加密均使用。  
  
 報表伺服器資料庫中的資料是利用對稱金鑰來加密。 每個報表伺服器資料庫均有單一對稱金鑰。 此對稱金鑰本身是利用 Windows 產生之非對稱金鑰組的公開金鑰來加密。 私密金鑰由報表伺服器 Windows 服務帳戶持有。  
  
 在報表伺服器向外延展部署中，如果多個報表伺服器執行個體共用相同的報表伺服器資料庫，則所有報表伺服器節點都使用單一對稱金鑰。 每個節點都必須有共用對稱金鑰的副本。 設定向外延展部署時，會自動為每個節點建立對稱金鑰的副本。 每個節點都會利用 Windows 服務帳戶之特定金鑰組的公開金鑰來加密其對稱金鑰副本。 若要深入了解如何為單一執行個體和向外延展部署建立對稱金鑰，請參閱[初始化報表伺服器 &#40;SSRS 設定管理員&#41;](ssrs-encryption-keys-initialize-a-report-server.md)。  
  
> [!NOTE]  
>  當您變更報表伺服器 Windows 服務帳戶時，非對稱金鑰可能會變成無效，因而中斷伺服器作業。 若要避免此問題，請永遠利用 Reporting Services 組態工具來修改服務帳戶設定。 當您使用組態工具時，系統會自動為您更新金鑰。 如需詳細資訊，請參閱[設定報表伺服器服務帳戶 &#40;SSRS 組態管理員&#41;](configure-the-report-server-service-account-ssrs-configuration-manager.md)。  
  
## <a name="other-sources-of-confidential-data"></a>其他機密資料的來源  
 報表伺服器會儲存其他未加密的資料，可能包含您想要保護的機密資訊。 尤其是報表記錄快照集與報表執行快照集所包含的查詢結果，可能包含要供授權使用者使用的資料。 如果您在包含機密資料的報表使用快照集功能，請注意，可以開啟報表伺服器資料庫中之資料表的使用者，就有可能檢查資料表內容來檢視預存報表的部份。  
  
> [!NOTE]  
>  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 不支援使用以使用者安全性識別為基礎之參數的報表的快取或報表記錄。  
  
## <a name="see-also"></a>另請參閱  
 [設定和管理加密金鑰&#40;SSRS 組態管理員&#41;](ssrs-encryption-keys-manage-encryption-keys.md)  
  
  
