---
title: 備份與還原 Reporting Services 加密金鑰 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- backing up encryption keys [Reporting Services]
- restoring encryption keys [Reporting Services]
- encryption keys [Reporting Services]
- symmetric keys [Reporting Services]
ms.assetid: 6773d5df-03ef-4781-beb7-9f6825bac979
caps.latest.revision: 12
author: markingmyname
ms.author: maghan
manager: jhubbard
ms.openlocfilehash: 26b64626126f331b5ca9dcc893a7ecb73a7bce38
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36147103"
---
# <a name="back-up-and-restore-reporting-services-encryption-keys"></a>備份與還原 Reporting Services 加密金鑰
  在報表伺服器組態中，建立用於加密機密資訊的對稱金鑰備份副本是很重要的一部分。 許多例行作業都需要金鑰的備份副本，這備份副本可以讓您在新安裝中重複使用現有的報表伺服器資料庫。  
  
 **[!INCLUDE[applies](../../includes/applies-md.md)]**  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 原生模式 | [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] SharePoint 模式  
  
 發生下列任何事件時，就必須還原加密金鑰的備份副本。  
  
-   變更報表伺服器 Windows 服務帳戶名稱或重設密碼。 當您使用 Reporting Services 組態管理員時，備份金鑰是服務帳戶名稱變更作業的一部分。  
  
    > [!NOTE]  
    >  重設密碼和變更密碼不同。 密碼重設需要覆寫網域控制站上之帳戶資訊的權限。 您忘記密碼或不知道特定密碼時，會由系統管理員執行密碼重設。 只有密碼重設需要對稱金鑰還原。 定期變更帳戶密碼並不需要重設對稱金鑰。  
  
-   重新命名主控報表伺服器的電腦或執行個體 (報表伺服器執行個體是以 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體名稱為基礎)。  
  
-   移轉報表伺服器安裝或設定報表伺服器，以使用其他報表伺服器資料庫。  
  
-   由於硬體故障而復原報表伺服器安裝。  
  
 您只需要備份對稱金鑰的一個副本。 報表伺服器資料庫與對稱金鑰之間有一對一對應。 雖然您只需要備份一個副本，但是如果您在向外延展部署模型中執行多個報表伺服器，就可能需要多次還原金鑰。 每個報表伺服器執行個體都需要其對稱金鑰的副本，才能鎖定和解除鎖定報表伺服器資料庫中的資料。  
  
  
## <a name="backing-up-the-encryption-keys"></a>備份加密金鑰  
 備份對稱金鑰的程序是將金鑰寫入您指定的檔案，然後使用您提供的密碼將金鑰加密。 對稱金鑰絕不能以未加密的狀態儲存，因此您將金鑰儲存到磁碟時，必須提供密碼將其加密。 檔案建立之後，您必須將其儲存在安全的位置，並 **記住用來解除檔案鎖定的密碼** 。 若要備份對稱金鑰，您可以使用下列工具：  
  
 **原生模式** ：Reporting Services 組態管理員或 **rskeymgmt** 公用程式。  
  
 **SharePoint 模式** ：SharePoint 管理中心頁面或 PowerShell。  
  
####  <a name="bkmk_backup_sharepoint"></a> 備份 SharePoint 模式報表伺服器  
 對於 SharePoint 模式報表伺服器，您可以使用 PowerShell 命令，或使用適用於 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 服務應用程式的管理頁面。 如需詳細資訊，請參閱 [管理 Reporting Services SharePoint 服務應用程式](../manage-a-reporting-services-sharepoint-service-application.md)的＜金鑰管理＞一節  
  
####  <a name="bkmk_backup_configuration_manager"></a> 備份加密金鑰 - Reporting Services 組態管理員 (原生模式)  
  
1.  啟動 Reporting Services 組態管理員，然後連接到您要設定的報表伺服器執行個體。  
  
2.  按一下 **[加密金鑰]**，然後按一下 **[備份]**。  
  
3.  輸入增強式密碼。  
  
4.  指定要包含儲存之金鑰的檔案。 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 會將 .snk 副檔名附加到這個檔案。 可以考慮將檔案儲存到磁碟上，使其與報表伺服器分開。  
  
5.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
####  <a name="bkmk_backup_rskeymgmt"></a> 備份加密金鑰 – rskeymgmt (原生模式)  
  
1.  在主控報表伺服器的本機電腦上，執行 **[rskeymgmt.exe]** 。 您必須使用 `-e` 擷取引數來複製金鑰、提供檔案名稱，並指定密碼。 下列範例說明您必須指定的引數：  
  
    ```  
    rskeymgmt -e -f d:\rsdbkey.snk -p<password>  
    ```  
  
## <a name="restore-encryption-keys"></a>還原加密金鑰  
 還原對稱金鑰會覆寫儲存在報表伺服器資料庫中的現有對稱金鑰。 還原加密金鑰會以您先前儲存到磁碟的副本，取代無法使用的金鑰。 還原加密金鑰會導致下列動作：  
  
-   從密碼保護的備份檔案開啟對稱金鑰。  
  
-   使用報表伺服器 Windows 服務的公開金鑰，將對稱金鑰加密。  
  
-   將加密的對稱金鑰儲存在報表伺服器資料庫中。  
  
-   刪除先前儲存的對稱金鑰資料 (例如，先前部署中已存在於報表伺服器資料庫中的金鑰資訊)。  
  
 若要還原加密金鑰，檔案上必須有一個加密金鑰的副本。 您也必須知道解除鎖定儲存之副本的密碼。 如果您有金鑰和密碼，就可以執行 Reporting Services 組態工具或 **rskeymgmt** 公用程式來還原金鑰。 對稱金鑰必須和鎖定與解除鎖定目前儲存在報表伺服器資料庫中之加密資料的金鑰相同。 如果您還原無效的副本，報表伺服器將無法存取目前儲存在報表伺服器資料庫中的加密資料。 萬一發生這種情形，如果無法還原有效的金鑰，就必須刪除所有的加密值。 如果因故無法還原加密金鑰 (例如，您若沒有備份副本)，則必須刪除現有的金鑰和加密內容。 如需詳細資訊，請參閱[刪除和重新建立加密金鑰 &#40;SSRS 設定管理員&#41;](ssrs-encryption-keys-delete-and-re-create-encryption-keys.md)。 如需建立對稱金鑰的詳細資訊，請參閱[初始化報表伺服器 &#40;SSRS 組態管理員&#41;](ssrs-encryption-keys-initialize-a-report-server.md)。  
  
####  <a name="bkmk_restore_configuration_manager"></a> 還原加密金鑰 - Reporting Services 組態管理員 (原生模式)  
  
1.  啟動 Reporting Services 組態管理員，然後連接到您要設定的報表伺服器執行個體。  
  
2.  在 [加密金鑰] 頁面上，按一下 **[還原]**。  
  
3.  選取包含備份副本的 .snk 檔案。  
  
4.  輸入解除檔案鎖定的密碼。  
  
5.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
####  <a name="bkmk_restore_rskeymgmt"></a> 還原加密金鑰 – rskeymgmt (原生模式)  
  
1.  在主控報表伺服器的本機電腦上，執行 **[rskeymgmt.exe]** 。 使用`-a`引數還原金鑰。 您必須提供完整的檔案名稱，並指定密碼。 下列範例說明您必須指定的引數：  
  
    ```  
    rskeymgmt -a -f d:\rsdbkey.snk -p<password>  
    ```  
  
## <a name="see-also"></a>另請參閱  
 [設定和管理加密金鑰&#40;SSRS 組態管理員&#41;](ssrs-encryption-keys-manage-encryption-keys.md)  
  
  