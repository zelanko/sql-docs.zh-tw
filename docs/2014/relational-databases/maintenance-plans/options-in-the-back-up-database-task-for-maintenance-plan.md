---
title: 備份資料庫工作 (維護計畫) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
f1_keywords:
- sql12.swb.maint.backup.f1
- sql12.swb.maint.maintplanproperties.logbackup.f1
helpviewer_keywords:
- Back Up Database Task dialog box
ms.assetid: ed1ef012-fa14-4ba5-bafe-d1527ba065b3
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 4a31052bb0633d370098e328741432f6b854d65e
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "68205955"
---
# <a name="back-up-database-task-maintenance-plan"></a>備份資料庫工作 (維護計畫)
  使用 [**備份資料庫**工作] 對話方塊，即可將備份工作加入維護計畫。 萬一因為發生系統或硬體失敗 (或使用者錯誤) 而導致資料庫在某方面發生損毀，因此需要還原已備份副本時，備份資料庫就相當重要。 此工作讓您能夠執行完整、差異、檔案和檔案群組，以及交易記錄的備份。  
  
 **建立備份資料庫工作**  
  
-   [建立維護計畫](create-a-maintenance-plan.md)  
  
## <a name="options"></a>選項。  
 **[連接]**  
 選取執行此工作時要使用的伺服器連接。  
  
 **新增**  
 建立新的伺服器連接，以便執行此工作時使用。 下面會描述 **[新增連接]** 對話方塊。  
  
 **資料庫**  
 指定受此工作影響的資料庫。 選取之後，下拉式清單就會提供下列選項： **All databases**、 **All system databases**、 **All user databases**、 **These specific databases**。  
  
 **所有資料庫**  
 產生維護計畫，以便針對所有 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料庫執行維護工作。  
  
 **所有系統資料庫（master、msdb、model）**  
 產生維護計畫，針對每個 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 系統資料庫執行維護工作。 不會針對使用者建立的資料庫執行維護工作。  
  
 **所有使用者資料庫（不包括 master、model、msdb、tempdb）**  
 產生維護計畫，針對所有使用者建立的資料庫執行維護工作。 不會對 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 系統資料庫執行任何維護工作。  
  
 **這些資料庫**  
 產生維護計畫，只針對選取的資料庫執行維護工作。 如果選擇此選項，則必須在清單中至少選取一個資料庫。  
  
 **備份類型**  
 顯示要執行的備份類型。  
  
 **備份元件**  
 選取 [資料庫]****，即可備份整個資料庫。 選取 **[檔案與檔案群組]** ，即可僅備份資料庫的一部分。 如果已選取，請提供檔案或檔案群組名稱。 在 **[資料庫]** 方塊中選取多個資料庫時，僅能指定 **[備份元件]** 的 **[資料庫]**。 若要執行檔案或檔案群組備份，請為每個資料庫建立工作。  
  
 **備份組即將到期**  
 指定備份組何時可由其他備份組覆寫。  
  
 **備份至**  
 將資料庫備份至檔案或至磁帶。 唯有安裝在包含資料庫之電腦的磁帶裝置可以使用。  
  
 **跨一或多個檔案備份資料庫**  
 按一下 [新增]****，即可開啟 [選取備份目的地]**** 對話方塊，並提供一或多個磁碟位置，或磁帶裝置。  
  
 **如果備份檔案存在**  
 選取 [附加]**** 將此備份加入檔案的結尾。 選取 [覆寫]**** 即可移除檔案中所有舊的備份，並以此新備份取代。  
  
 **為每個資料庫建立備份檔案**  
 在資料夾方塊裡所指定的位置中，建立備份檔案， 會為選取的每個資料庫建立一個檔案。  
  
 **為每個資料庫建立一個子目錄**  
 選取即可在子資料夾中放入每個資料庫。  
  
> [!IMPORTANT]  
>  雖然維護計畫可以建立子目錄，但是維護工作無法刪除子目錄。 這項功能可降低利用「維護清除」工作刪除檔案這類惡意攻擊的可能性。  
  
> [!IMPORTANT]  
>  子目錄會繼承上層目錄的權限。 限制權限以避免未經授權的存取。  
  
 **資料夾**  
 指定包含自動建立的資料庫檔案的資料夾。  
  
 **備份檔案延伸模組**  
 指定備份檔案所用的副檔名。 預設為 **.bak**。  
  
 **確認備份完整性**  
 確認備份組是完整的，且所有磁碟區都可以讀取。  
  
 **備份記錄檔的結尾，並讓資料庫保持在還原狀態**  
 在還原資料庫之前，執行記錄備份做為最後一個步驟。 如需詳細資訊，請參閱[結尾記錄備份 &#40;SQL Server&#41;](../backup-restore/tail-log-backups-sql-server.md)。  
  
 **設定備份壓縮**  
 在 [!INCLUDE[ssEnterpriseEd10](../../includes/ssenterpriseed10-md.md)] (或更新的版本) 中，選取下列其中一個 [備份壓縮](../backup-restore/backup-compression-sql-server.md) 值：  
  
|||  
|-|-|  
|**使用預設伺服器設定**|按一下即可使用伺服器層級的預設值。<br /><br /> 此預設值是由 [備份壓縮預設]**** 伺服器組態選項所設定。 有關如何檢視這個選項目前之設定的詳細資訊，請參閱 [檢視或設定備份壓縮伺服器組態選項](../../database-engine/configure-windows/view-or-configure-the-backup-compression-default-server-configuration-option.md)。|  
|**壓縮備份**|不論目前的伺服器層級預設值為何，按一下即可壓縮備份。<br /><br /> ** \* \*重要\*事項**根據預設，壓縮會大幅增加 CPU 使用量，而且壓縮程式所耗用的額外 CPU 可能會對並行作業造成不良的影響。 因此，您可能會想要在由[資源管理員](../resource-governor/resource-governor.md)所限制之 CPU 使用量的工作階段中建立低優先權的壓縮備份。 如需詳細資訊，請參閱本主題稍後介紹的＜ [使用資源管理員進行備份壓縮，以限制 CPU 使用率 &#40;Transact-SQL&#41;](../backup-restore/use-resource-governor-to-limit-cpu-usage-by-backup-compression-transact-sql.md)限制的工作階段中，建立低優先權的壓縮備份。|  
|**不要壓縮備份**|不論目前的伺服器層級預設值為何，按一下即可建立未壓縮備份。|  
  
 **View T-sql**  
 根據選取的選項，檢視此工作在伺服器上執行的 [!INCLUDE[tsql](../../includes/tsql-md.md)] 陳述式。  
  
> [!NOTE]  
>  受影響的物件數目較為大量時，會多花一些時間才會顯示。  
  
## <a name="new-connection-dialog-box"></a>新增連接對話方塊  
 **連接名稱**  
 輸入新連接的名稱。  
  
 **選取或輸入伺服器名稱**  
 選取執行此工作時要連接的伺服器。  
  
 **[重新整理]**  
 重新整理可用的伺服器清單。  
  
 **輸入資訊以登入伺服器**  
 指定如何對伺服器進行驗證。  
  
 **使用 Windows 整合式安全性**  
 使用 Windows 驗證連接到的[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssDE](../../includes/ssde-md.md)]實例。  
  
 **使用特定的使用者名稱和密碼**  
 使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssDE](../../includes/ssde-md.md)] 驗證，連接到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的執行個體。 無法使用此選項。  
  
 **使用者名稱**  
 提供驗證時要使用的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 登入。 無法使用此選項。  
  
 **密碼**  
 提供驗證時要使用的密碼。 無法使用此選項。  
  
## <a name="see-also"></a>另請參閱  
 [BACKUP &#40;Transact-SQL&#41;](/sql/t-sql/statements/backup-transact-sql)  
  
  
