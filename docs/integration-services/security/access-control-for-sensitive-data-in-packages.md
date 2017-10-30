---
title: "在封裝中的機密資料的存取控制 |Microsoft 文件"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.dts.packageprotectionlevel.f1
- sql13.ssis.bids.projectprotectionlevel.f1
- sql13.dts.designer.packagepassword.f1
- sql13.ssis.bids.projectpassword.f1
helpviewer_keywords:
- passwords [Integration Services]
- packages [Integration Services], security
- protection levels for packages [Integration Services]
- configuration files [Integration Services]
- encryption [Integration Services]
- cryptography [Integration Services]
- security [Integration Services], protection levels
ms.assetid: d4b073c4-4238-41fc-a258-4e114216e185
caps.latest.revision: 44
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: f5acdf3ae4f27685fce7aab56aab423044491ee1
ms.openlocfilehash: 51150293cd37e0d9f641bd7ee2ee30f8cce8ed95
ms.contentlocale: zh-tw
ms.lasthandoff: 08/03/2017

---
# <a name="access-control-for-sensitive-data-in-packages"></a>封裝中的敏感性資料存取控制
  若要保護 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 封裝中的資料，您可以設定保護等級，只保護封裝中的機密資料或全部資料。 此外，您可以使用密碼或使用者金鑰將資料加密，或是藉由資料庫來加密資料。 也請注意，用於封裝的保護等級不一定是靜態的，而是隨著封裝生命週期有所改變。 通常，您會在開發階段設定一個保護等級，然後在部署封裝時設定另一個保護等級。  
  
> [!NOTE]  
>  除了本主題所描述的保護等級之外，您也可以使用固定的資料庫層級角色來保護儲存到 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 伺服器的封裝。  
  
## <a name="definition-of-sensitive-information"></a>機密資訊的定義  
 在 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 封裝中，下列資訊定義為「機密」：  
  
-   連接字串的密碼部份。 不過，如果您選取加密所有項目的選項，則會將整個連接字串視為機密資料。  
  
-   標記為機密資料之工作產生的 XML 節點。 XML 節點的標記由 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 控制，使用者無法變更。  
  
-   標記為機密資訊的任何變數。 變數的標記由 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]控制。  
  
 對於 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 是否將屬性視為機密，取決於 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 元件 (例如，連接管理員或工作) 的開發人員是否將該屬性指定為機密。 使用者無法將屬性加入到視為機密之屬性的清單中，也無法從中移除屬性。  
  
## <a name="encryption"></a>加密  
 封裝保護等級所使用的加密是使用「 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 資料保護 API (DPAPI)」(「加密 API (CryptoAPI)」的一部分) 來執行的。  
  
 使用密碼加密封裝的封裝保護等級也需要您提供密碼。 如果您將保護等級從不使用密碼變更為使用密碼的等級，則會提示您輸入密碼。  
  
 此外，對於使用密碼的保護等級， [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 會使用「 [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] 類別庫 (FCL)」中，金鑰長度為 192 位元的「三重 DES」加密演算法。  
  
## <a name="protection-levels"></a>保護等級  
 下表描述 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 提供的保護等級。 括弧中的值是 <xref:Microsoft.SqlServer.Dts.Runtime.DTSProtectionLevel> 列舉的值。 這些值會顯示在 [屬性] 視窗中，當您在 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]中處理封裝時，可以使用該視窗設定封裝的屬性。  
  
|保護等級|說明|  
|----------------------|-----------------|  
|不要儲存機密 (**DontSaveSensitive**)|儲存封裝時，隱藏封裝中的機密屬性值。 此保護等級不加密，但是會防止標記為機密資料的屬性與封裝一起儲存，因此其他使用者無法使用機密資料。 如果其他使用者開啟封裝，則機密資訊會以空白取代，該使用者必須提供機密資訊。<br /><br /> 與 **dtutil** 公用程式 (dtutil.exe) 搭配使用時，這個保護等級會對應至值 0。|  
|以密碼加密全部 (**EncryptAllWithPassword**)|使用密碼加密整個封裝。 封裝是使用建立或匯出封裝時使用者提供的密碼來加密的。 若要在 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 設計師 中開啟封裝，或是使用 **dtexec** 命令提示公用程式來執行封裝，使用者必須提供封裝密碼。 如果沒有密碼，使用者就無法存取或執行封裝。<br /><br /> 與 **dtutil** 公用程式搭配使用時，這個保護等級會對應至值 3。|  
|以使用者金鑰加密全部 (**EncryptAllWithUserKey**)|使用以目前使用者設定檔為基礎的金鑰加密整個封裝。 只有建立或匯出封裝的使用者，才可以在 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 設計師 中開啟封裝，或是使用 **dtexec** 命令提示公用程式來執行封裝。<br /><br /> 與 **dtutil** 公用程式搭配使用時，這個保護等級會對應至值 4。<br /><br /> 注意：對於使用使用者金鑰的保護等級， [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 會使用 DPAPI 標準。 如需 DPAPI 的詳細資訊，請參閱 MSDN Library，其網址為 [http://msdn.microsoft.com/library](http://go.microsoft.com/fwlink/?LinkId=15408)。|  
|以密碼加密機密 (**EncryptSensitiveWithPassword**)|使用密碼僅加密封裝中的機密屬性值。 DPAPI 用於此加密。 機密資料會做為封裝的一部份進行儲存，但該資料會使用建立或匯出封裝時目前使用者所提供的密碼進行加密。 若要在「 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 設計師」中開啟封裝，使用者必須提供封裝密碼。 如果未提供密碼，則會開啟封裝但不提供機密資料，目前的使用者必須為機密資料提供新值。 如果使用者嘗試在未提供密碼的情況下執行封裝，則封裝執行會失敗。 如需密碼和命令列執行的詳細資訊，請參閱 [dtexec 公用程式](../../integration-services/packages/dtexec-utility.md)。<br /><br /> 與 **dtutil** 公用程式搭配使用時，這個保護等級會對應至值 2。|  
|以使用者金鑰加密機密 (**EncryptSensitiveWithUserKey**)|使用以目前使用者設定檔為基礎的金鑰，僅加密封裝中的機密屬性值。 只有使用相同設定檔的相同使用者才可以載入封裝。 如果其他使用者開啟封裝，則機密資訊會以空白取代，且目前的使用者必須為機密資料提供新值。 如果使用者嘗試執行封裝，則封裝執行會失敗。 DPAPI 用於此加密。<br /><br /> 與 **dtutil** 公用程式搭配使用時，這個保護等級會對應至值 1。<br /><br /> 注意：對於使用使用者金鑰的保護等級， [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 會使用 DPAPI 標準。 如需 DPAPI 的詳細資訊，請參閱 MSDN Library，其網址為 [http://msdn.microsoft.com/library](http://go.microsoft.com/fwlink/?LinkId=15408)。|  
|依賴伺服器儲存體進行加密 (**ServerStorage**)|使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料庫角色保護整個封裝。 在將封裝儲存到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] msdb 資料庫時，才支援此選項。 此外，SSISDB 目錄會使用 **ServerStorage** 保護等級<br /><br /> 將封裝從 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]儲存到檔案系統時不支援此選項。|  
  
## <a name="protection-level-setting-and-the-ssisdb-catalog"></a>保護等級設定和 SSISDB 目錄  
 SSISDB 目錄會使用 **ServerStorage** 保護等級。 當您將 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 專案部署至 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 伺服器時，目錄會自動將封裝資料與敏感值加密。 當您擷取時，目錄也會自動解密資料。  
  
 如果您從 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 伺服器將專案 (.ispac 檔) 匯出至檔案系統，系統會自動將保護等級變更為 **EncryptSensitiveWithUserKey**。 如果您使用 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 中的 [Integration Services 匯入專案精靈] 匯入專案，[屬性] 視窗中的 [ProtectionLevel] 屬性會顯示 [EncryptSensitiveWithUserKey] 這個值。  
  
## <a name="protection-level-setting-based-on-package-life-cycle"></a>根據封裝生命週期設定保護等級  
 您會在第一次於 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 中開發 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)][!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 封裝時，設定該封裝的保護等級。 稍後在部署封裝、從 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 中的 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 匯入或匯出封裝，或將封裝從 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 複製到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]、「[!INCLUDE[ssIS](../../includes/ssis-md.md)] 封裝存放區」或檔案系統時，都可以更新封裝保護等級。 例如，如果您在電腦上建立和儲存封裝時，使用其中一個使用者金鑰保護等級選項，則當您將封裝提供給其他使用者時，必須變更保護等級，否則使用者無法開啟封裝。  
  
 一般而言，您需要依照下列步驟變更保護等級：  
  
1.  在開發階段，將封裝的保護等級設定保留為預設值 **EncryptSensitiveWithUserKey**。 這項設定可以協助確保只有開發人員能夠看到封裝中的機密值。 或者，您可以考慮使用 **EncryptAllWithUserKey**或 **DontSaveSensitive**。  
  
2.  到了部署封裝的階段，您必須將保護等級變更為不需要開發人員使用者金鑰的等級。 因此您通常需要選取 **EncryptSensitiveWithPassword**或 **EncryptAllWithPassword**。 指定暫時性的增強式密碼來加密封裝，並且讓生產環境中的作業小組知道該密碼。  
  
3.  將封裝部署到生產環境之後，作業小組可以指定只有小組內部知道的增強式密碼來重新加密已部署的封裝。 或者，作業小組也可以選擇 **EncryptSensitiveWithUserKey** 或 **EncryptAllWithUserKey**，然後使用將執行封裝之帳戶的本機認證來加密已部署的封裝。  

## <a name="set_protection"></a> 設定或變更封裝的保護等級
  若要控制封裝內容以及其中包含之機密值 (例如密碼) 的存取權，請設定 **ProtectionLevel** 屬性的值。 包含在專案中的封裝需要有和專案相同的保護層級，才能建立專案。 如果您變更專案上的 **ProtectionLevel** 屬性設定，就需要手動更新封裝的屬性設定。  
  
 如需 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 安全性功能的概觀，請參閱[安全性概觀 &#40;Integration Services&#41;](../../integration-services/security/security-overview-integration-services.md)。  
  
 本主題中的程序說明如何使用 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 或 dtutil 命令提示字元公用程式來變更 **ProtectionLevel** 屬性。  
  
> [!NOTE]  
>  除了本主題中的程序之外，您通常可以在匯入或匯出封裝時，設定或變更封裝的 **ProtectionLevel** 屬性。 您也可以在使用 [ **匯入和匯出精靈] 來儲存封裝時，變更封裝的** ProtectionLevel [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 屬性。  
  
### <a name="to-set-or-change-the-protection-level-of-a-package-in-sql-server-data-tools"></a>若要在 SQL Server 資料工具中設定或變更封裝的保護等級  
  
1.  在 **設定封裝的保護等級** 主題中，檢閱 [ProtectionLevel](#set_protection)屬性可用的值，並判斷適用於您的封裝的值。  
  
2.  在 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]中，開啟包含封裝的 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 專案。  
  
3.  在 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 設計器中，開啟封裝。  
  
4.  如果 [屬性] 視窗並未顯示封裝屬性，請按一下設計介面。  
  
5.  在 [屬性] 視窗的 [安全性] 群組中，為 **ProtectionLevel** 屬性選取適當的值。  
  
     如果您選取了需要密碼的保護等級，請輸入密碼作為 **PackagePassword** 屬性的值。  
  
6.  在 [檔案] 功能表上，選取 [儲存選取項目] 以儲存修改過的封裝。  
  
### <a name="to-set-or-change-the-protection-level-of-packages-at-the-command-prompt"></a>在命令提示字元設定或變更封裝的保護等級  
  
1.  檢閱可用的值**ProtectionLevel**區段中的屬性[設定封裝保護等級](#set_protection)，並判斷您的套件的適當值。  
  
2.  在 **dtutil 公用程式** 主題中，檢閱 [Encrypt](../../integration-services/dtutil-utility.md)選項的對應，並判斷適合當做所選 **ProtectionLevel** 屬性值的整數。  
  
3.  開啟 [命令提示字元] 視窗。  
  
4.  在命令提示字元，導覽至您要設定其 **ProtectionLevel** 屬性之封裝的所在資料夾。  
  
     下列步驟所示的語法範例假設此資料夾為目前的資料夾。  
  
5.  使用類似於下列其中一個範例的命令，設定或變更封裝的保護等級：  
  
    -   下列命令會將檔案系統中個別封裝的 **ProtectionLevel** 屬性設為層級 2「機密資料以密碼加密」，並且將密碼設為 "strongpassword"：  
  
         `dtutil.exe /file "C:\Package.dtsx" /encrypt file;"C:\Package.dtsx";2;strongpassword`  
  
    -   下列命令會將檔案系統中特定資料夾內所有封裝的 **ProtectionLevel** 屬性設為層級 2「機密資料以密碼加密」，並且將密碼設為 "strongpassword"：  
  
         `for %f in (*.dtsx) do dtutil.exe /file %f /encrypt file;%f;2;strongpassword`  
  
         如果您要對批次檔使用類似命令，請將檔案預留位置 "%f" 改輸入為批次檔適用的 "%%f"。  

## <a name="protection_dialog"></a>封裝專案保護等級對話方塊
  使用 **[封裝保護等級]** 對話方塊，即可更新封裝的保護等級。 保護等級會決定保護方法、密碼或使用者金鑰，以及封裝保護的範圍。 保護可包括所有資料或只包括機密資料。  
  
 若要了解封裝安全性選項與需求，您可能會發現若要查看[安全性概觀 &#40; Integration Services &#41;](../../integration-services/security/security-overview-integration-services.md)。  
  
### <a name="options"></a>選項。  
 **Package protection level**  
 從清單中選取保護等級。  
  
 **密碼**  
 如果使用 [機密資料以密碼加密] 或 [所有資料以密碼加密] 保護層級，請輸入密碼。  
  
 **再次輸入密碼**  
 再輸入密碼一次。  

## <a name="password_dialog"></a>封裝密碼 對話方塊
  使用 **[封裝密碼]** 對話方塊，即可為使用密碼加密的封裝提供封裝密碼。 如果封裝使用 **[機密資料以密碼加密]**或 **[所有資料以密碼加密]** 保護等級，則必須提供密碼。  
  
### <a name="options"></a>選項。  
 **密碼**  
 輸入密碼。  
  
## <a name="see-also"></a>另請參閱  
 [Integration Services &#40;SSIS&#41; 封裝](../../integration-services/integration-services-ssis-packages.md)   
 [安全性概觀 &#40; Integration Services &#41;](../../integration-services/security/security-overview-integration-services.md)  
 [dtutil 公用程式](../../integration-services/dtutil-utility.md)  
  

