---
title: 計劃和測試資料庫引擎升級計畫 | Microsoft Docs
ms.custom: ''
ms.date: 07/20/2016
ms.prod: sql
ms.prod_service: install
ms.reviewer: ''
ms.suite: sql
ms.technology:
- server-general
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 19c5b725-7400-4881-af8f-fd232ca28234
caps.latest.revision: 16
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: ccdef1d662006900a6d1338acbb24db907bc9192
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="plan-and-test-the-database-engine-upgrade-plan"></a>計劃和測試資料庫引擎升級計畫

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]
  
 若要成功執行 [!INCLUDE[ssnoversion](../../includes/ssnoversion-md.md)] 升級，不論使用何種方法，都需要適當規劃。  
  
## <a name="release-notes-and-known-upgrade-issues"></a>版本資訊與已知升級問題  
 升級 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 之前，請檢閱：

- [SQL Server 2017 版本資訊](../../sql-server/sql-server-2017-release-notes.md) 
- [SQL Server 2016 版本資訊](../../sql-server/sql-server-2016-release-notes.md) 
- [SQL Server 資料庫引擎回溯相容性](../../database-engine/sql-server-database-engine-backward-compatibility.md)一文。  
  
## <a name="pre-upgrade-planning-checklist"></a>升級前的計劃檢查清單  
 升級 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 之前，請檢閱下列檢查清單及相關文章。 這些文章適用於所有升級，不論使用何種升級方法，都能協助您從輪流升級、新安裝升級或就地升級當中，決定最適當的升級方法。 例如，您可能無法執行就地升級或輪流升級 (若您要升級作業系統)、從 SQL Server 2005 升級，或是從 32 位元版本的 SQL Server 升級。 對於決策樹，請參閱 [Choose a Database Engine Upgrade Method](../../database-engine/install-windows/choose-a-database-engine-upgrade-method.md)。  
  
-   **硬體與軟體需求：** 檢閱安裝 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]的硬體與軟體需求。 您可在以下頁面找到這些需求：[安裝 SQL Server 的硬體和軟體需求](../../sql-server/install/hardware-and-software-requirements-for-installing-sql-server.md)。 在任何升級規劃的週期當中，都會涉及升級硬體 (較新的硬體較快，且可能由於處理器較少或資料庫與伺服器的合併而減少授權) 和升級作業系統的考量。 這類的硬體和軟體變更會影響您所選擇之升級方法的類型。  
  
-   **目前環境︰** 研究您的目前環境，以了解正在使用的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 元件和連線到您環境的用戶端。  
  
    -   **用戶端提供者︰** 雖然升級時您不需要更新每個用戶端的提供者，但您也可以選擇更新。 如果您要從 [!INCLUDE[sql14](../../includes/sssql14-md.md)] 或更舊版本升級，下列 [!INCLUDE[sql15](../../includes/sssql15-md.md)] 功能將需要每個用戶端的已更新提供者，或提供額外功能的已更新提供者：  
  
       -   [永遠加密 &#40;Database Engine&#41;](../../relational-databases/security/encryption/always-encrypted-database-engine.md)  
  
       -   [Stretch Database](../../sql-server/stretch-database/stretch-database.md)  
  
       -   [可用性群組接聽程式、用戶端連線及應用程式容錯移轉 &#40;SQL Server&#41;](../../database-engine/availability-groups/windows/listeners-client-connectivity-application-failover.md)  
  
       -   SSL 安全性更新  

   >[!NOTE]
   >前面的清單也適用於 [!INCLUDE[sscurrent](../../includes/sscurrent-md.md)]。
  
-   **協力廠商元件︰**判斷協力廠商元件的相容性，例如整合式備份。  
  
-   **目標環境︰** 確認您的目標環境符合硬體和軟體需求，且能夠支援原始系統的需求。 例如，您的升級可能包含多個 SQL Server 執行個體對單一執行個體的調節、新的 [!INCLUDE[ssnoversion](../../includes/ssnoversion-md.md)] 執行個體，或是將 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 環境虛擬化至私人或公用雲端。  
  
-   **版本︰** 判斷適當的 [!INCLUDE[ssCurrent](../../includes/ssnoversion-md.md)] 升級版本，並判斷升級的有效升級路徑。 如需詳細資訊，請參閱＜ [Supported Version and Edition Upgrades](../../database-engine/install-windows/supported-version-and-edition-upgrades.md)＞。 從 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的一個版本升級到另一個版本之前，請確認您目前使用的功能在您想要升級後的版本中有受到支援。  
  
    > [!NOTE]  
    >  當您從舊版 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Enterprise Edition 升級 [!INCLUDE[ssCurrent](../../includes/ssnoversion-md.md)] 時，請選擇 [Enterprise Edition: 核心授權] 和 [Enterprise Edition]。 這些 Enterprise Edition 只有在授權模式方面不同。 如需詳細資訊，請參閱 [Compute Capacity Limits by Edition of SQL Server](../../sql-server/compute-capacity-limits-by-edition-of-sql-server.md)。  
  
-   **回溯相容性︰**請檢閱 [!INCLUDE[ssCurrent](../../includes/ssnoversion-md.md)] 資料庫引擎回溯相容性文章，以檢閱 [!INCLUDE[ssCurrent](../../includes/ssnoversion-md.md)] 與您要升級的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 版本之間的行為變更。 請參閱 [SQL Server Database Engine Backward Compatibility](../../database-engine/sql-server-database-engine-backward-compatibility.md)。  
  
-   **升級建議程式：**  執行 [!INCLUDE[ssCurrent](../../includes/ssnoversion-md.md)] 升級建議程式來協助診斷可能封鎖升級程序，或現有指令碼或應用程式因重大變更而需要修改等原因造成的問題。 [!INCLUDE[ssCurrent](../../includes/ssnoversion-md.md)] 包含新版的升級建議程式，以協助客戶為現有的系統備妥升級。  此工具也能夠檢查現有資料庫，以查看其升級後是否能夠利用新功能 (如延伸資料表)。   
    您可以在 [!INCLUDE[ssCurrent](../../includes/ssnoversion-md.md)]這裡  [下載](https://www.microsoft.com/en-us/download/details.aspx?id=48119)升級建議程式。  
  
-   **System Configuration Checker：**  在您實際排定升級之前，先執行 [!INCLUDE[ssCurrent](../../includes/ssnoversion-md.md)] System Configuration Checker (SCC) 來判斷 SQL Server 安裝程式是否偵測到封鎖問題。 如需詳細資訊，請參閱 [Check Parameters for the System Configuration Checker](../../database-engine/install-windows/check-parameters-for-the-system-configuration-checker.md)。  
  
-   **升級記憶體最佳化資料表：** 將包含記憶體最佳化資料表的 SQL Server 2014 資料庫執行個體升級到 SQL Server 2016 時，升級程序將需要額外的時間來將記憶體最佳化資料表轉換成磁碟上格式 (執行這些步驟時資料庫將會離線)。   時間長短是根據記憶體最佳化資料表的大小及 I/O 子系統的速度而定。 針對就地和新安裝升級，升級需要三種大小的資料作業 (輪流升級不需要步驟 1，但需要步驟 2 和 3)：  
  
    1.  以舊的磁碟上格式執行資料庫復原 (這包含從磁碟機將所有記憶體最佳化資料表中的資料載入記憶體)  
  
    2.  將資料以新的磁碟上格式序列化  
  
    3.  以新的格式執行資料庫復原 (包含從磁碟機將所有記憶體最佳化資料表中的資料載入記憶體)  
  
     此外，若執行此程序期間磁碟機空間不足，將會造成復原失敗。 請確定磁碟機的空間足夠儲存現有資料庫，並擁有等同資料庫內 MEMORY_OPTIMIZED_DATA 檔案群組中容器之大小的額外儲存空間，以執行就地升級或將 SQL Server 2014 資料庫附加到 SQL Server 2016 執行個體。使用以下查詢來判斷目前 MEMORY_OPTIMIZED_DATA 檔案群組所需的磁碟空間，以及完成升級所需的可用磁碟空間：  
  
    ```  
    select cast(sum(size) as float)*8/1024/1024 'size in GB'   
    from sys.database_files  
    where data_space_id in (select data_space_id from sys.filegroups where type=N'FX')  
    ```  
  
## <a name="develop-and-test-the-upgrade-plan"></a>開發和測試升級計畫  
 最好的方法是將升級視為如同其他 IT 專案。 您應該組織一個具備資料庫系統管理員、網路、擷取、轉換與載入 (ETL)，以及其他升級所需之技能的升級小組。 該小組需要：  
  
-   **選擇升級方法：** 請參閱 [選擇 Database Engine 升級方法](../../database-engine/install-windows/choose-a-database-engine-upgrade-method.md)。  
  
-   **開發復原計劃︰**。 如果需要復原，執行此計劃就能還原為原始的環境。  
  
-   **決定驗收準則：** 將使用者切換到升級的環境之前，您需要知道升級是否成功。  
  
-   **測試升級計劃︰** 使用 Microsoft SQL Server Distributed Replay 公用程式，來以您的實際工作負載測試效能。 此公用程式可使用多部電腦重新執行追蹤資料，並模擬關鍵任務的工作負載。 在 SQL Server 升級前後於測試伺服器上進行重新執行作業，可讓您衡量效能差異，並找出應用程式在升級後可能會發生的不相容情況。 如需詳細資訊，請參閱 [SQL Server Distributed Replay](../../tools/distributed-replay/sql-server-distributed-replay.md) 和[管理工具命令列選項 &#40;Distributed Replay Utility&#41;](../../tools/distributed-replay/administration-tool-command-line-options-distributed-replay-utility.md)。  
  
## <a name="next-steps"></a>後續步驟  
 [升級 Database Engine](../../database-engine/install-windows/upgrade-database-engine.md)  
  
  
