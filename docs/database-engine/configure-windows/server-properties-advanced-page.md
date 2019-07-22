---
title: 伺服器屬性 (進階頁面) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: high-availability
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
f1_keywords:
- sql13.swb.serverproperties.advanced.f1
ms.assetid: cc5e65c2-448e-4f37-9ad4-2dfb1cc84ebe
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 1672b245f061f521c9114bca71f723fe75553c96
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/15/2019
ms.locfileid: "68025587"
---
# <a name="server-properties---advanced-page"></a>伺服器屬性 - 進階頁面
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  使用此頁面來檢視或修改進階的伺服器設定。  
  
 **若要檢視伺服器屬性頁面**  
  
-   [檢視或變更伺服器屬性 &#40;SQL Server&#41;](../../database-engine/configure-windows/view-or-change-server-properties-sql-server.md)  
  
## <a name="containment"></a>Containment  
 啟用自主資料庫  
 指出這個 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體是否允許自主資料庫。 當為 **True**時，可以建立、還原或附加自主資料庫。 當為 **False**時，自主資料庫無法建立、還原或附加至這個 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]執行個體。 變更自主屬性會影響資料庫的安全性。 啟用自主資料庫可讓資料庫擁有者授與這個 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]的存取權。 停用自主資料庫會阻止使用者連接。 若要了解內含項目屬性的影響，請參閱 [自主資料庫](../../relational-databases/databases/contained-databases.md) 和 [自主資料庫的安全性最佳做法](../../relational-databases/databases/security-best-practices-with-contained-databases.md)。  
  
## <a name="filestream"></a>FILESTREAM  
 **FILESTREAM 存取層級**  
 顯示 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]執行個體上目前 FILESTREAM 支援的層級。 若要變更存取層級，請選取下列其中一個值：  
  
 **已停用**  
 二進位大型物件 (BLOB) 資料不能儲存在檔案系統上。 這是預設值。  
  
 **已啟用 Transact-SQL 存取**  
 FILESTREAM 資料可使用 [!INCLUDE[tsql](../../includes/tsql-md.md)]來存取，但不能透過檔案系統來存取。  
  
 **已啟用完整存取**  
 FILESTREAM 資料可使用 [!INCLUDE[tsql](../../includes/tsql-md.md)] 來存取，也可以透過檔案系統存取。  
  
 當您初次啟用 FILESTREAM 時，您可能必須重新啟動電腦，才能設定驅動程式。  
  
 **FILESTREAM 共用名稱**  
 顯示在安裝期間選取之 FILESTREAM 共用的唯讀名稱。 如需詳細資訊，請參閱 [FILESTREAM &#40;SQL Server&#41;](../../relational-databases/blob/filestream-sql-server.md)。  
  
## <a name="miscellaneous"></a>其他  
 **允許觸發程序引發其他觸發程序**  
 允許觸發程序引發其他觸發程序。 觸發程序的巢狀結構，最多可達 32 層。 如需詳細資訊，請參閱 [CREATE TRIGGER &#40;Transact-SQL&#41;](../../t-sql/statements/create-trigger-transact-sql.md) 中的＜巢狀觸發程序＞一節。  
  
 **Blocked Process Threshold**  
 產生已封鎖的處理序報表的臨界值 (以秒為單位)。 此臨界值可設定為 0 到 86,400 的值。 預設不會針對已封鎖的處理序產生任何報告。 如需詳細資訊，請參閱 [已封鎖的處理序臨界值伺服器組態選項](../../database-engine/configure-windows/blocked-process-threshold-server-configuration-option.md)。  
  
 **資料指標臨界值**  
 指定資料指標集內的資料列數目，亦即非同步產生資料指標索引鍵集的數目。 當資料指標為結果集產生索引鍵集時，查詢最佳化工具會估計將在該結果集傳回的資料列數。 如果查詢最佳化工具估計將傳回的列數會大於這個臨界值，就會以非同步方式產生資料指標，讓使用者在資料指標繼續擴展的同時，可以從資料指標擷取資料列。 否則，會以同步的方式產生資料指標，使查詢等到所有資料列都傳回為止。  
  
 如果將資料指標臨界值設定為 -1，就會以同步的方式產生所有索引鍵集，這有益於小型的資料指標集。 如果將資料指標臨界值設定為 0，就會以非同步的方式產生所有資料指標索引鍵集。 若設定為其他的值，查詢最佳化工具就會用來比較資料指標集內預期的列數，如果預期的列數會超過設定的數字，就會以非同步的方式建立索引鍵集。 如需詳細資訊，請參閱 [設定 cursor threshold 伺服器組態選項](../../database-engine/configure-windows/configure-the-cursor-threshold-server-configuration-option.md)。  
  
 **預設全文檢索語言**  
 指定全文檢索索引資料行的預設語言。 全文檢索索引資料的語言分析相依於資料所用的語言。 這個選項的預設值是伺服器使用的語言。 如需所顯示設定的對應語言，請參閱 [sys.fulltext_languages &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-fulltext-languages-transact-sql.md)。  
  
 **預設語言**  
 所有新登入的預設語言，除非另有指定。  
  
 **全文檢索升級選項**  
 控制將資料庫從 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]升級時，要如何移轉全文檢索索引。 這個屬性適用於以下方式的升級：附加資料庫、還原資料庫備份、還原檔案備份，或是使用複製資料庫精靈複製資料庫。  
  
 替代方案如下所示：  
  
 **匯入**  
 匯入全文檢索目錄。 這項作業會明顯地比 **重建**快。 不過，匯入的全文檢索目錄並不會使用 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]中引進的新增強斷詞工具。 因此，最後您仍可能想要重建全文檢索目錄。  
  
 如果無法使用全文檢索目錄，將會重建關聯的全文檢索索引。 只有針對 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 資料庫才可以使用此選項。  
  
 **Rebuild**  
 全文檢索目錄會使用新的增強斷詞工具重建。 重建索引可能要花一些時間，而且在升級之後可能需要相當多的 CPU 和記憶體。  
  
 **重設**  
 重設全文檢索目錄。 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 全文檢索目錄檔案會遭到移除，但是全文檢索目錄和全文檢索索引的中繼資料則會保留。 在升級之後，所有的全文檢索索引都會停用變更追蹤，而且不會自動啟動搜耙。 當您在升級完成之後手動發出完整母體擴展之前，此目錄將會維持空白狀態。  
  
 如需如何選擇全文檢索升級選項的詳細資訊，請參閱 [升級全文檢索搜尋](../../relational-databases/search/upgrade-full-text-search.md)。  
  
> [!NOTE]  
>  也可以使用 [sp_fulltext_service](../../relational-databases/system-stored-procedures/sp-fulltext-service-transact-sql.md)upgrade_option 動作來設定全文檢索升級選項。  
  
 當您將 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 資料庫附加、還原或複製到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 時，該資料庫會立即可用，然後自動升級。 如果資料庫具有全文檢索索引，升級程序就會根據 [全文檢索目錄升級選項]  伺服器屬性的設定，匯入、重設或重建這些索引。 如果升級選項設定為 [匯入]  或 [重建]  ，則全文檢索索引在升級期間將無法使用。 根據進行索引的資料數量而定，匯入可能需要數個小時，而重建可能需要十倍以上的時間。 此外，請注意，當升級選項設定為 [匯入]  時，如果全文檢索目錄無法使用，系統就會重建相關聯的全文檢索索引。 如需檢視或變更 [全文檢索升級選項]  屬性設定的資訊，請參閱[管理及監視伺服器執行個體的全文檢索搜尋](../../relational-databases/search/manage-and-monitor-full-text-search-for-a-server-instance.md)。  
  
 **文字複寫大小上限**  
 指定在單一 INSERT、UPDATE、WRITETEXT 或 UPDATETEXT 陳述式中，可以加入複寫資料行或擷取資料行中的 **text**、 **ntext**、 **varchar(max)** 、 **nvarchar(max)** 、 **xml**和 **image** 資料的大小上限 (以位元組為單位)。 設定的變更會立即生效。 如需詳細資訊，請參閱 [設定 max text repl size 伺服器組態選項](../../database-engine/configure-windows/configure-the-max-text-repl-size-server-configuration-option.md)。  
  
 **掃描啟動程序**  
 指定在啟動時， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 會掃描是否有預存程序要自動執行。 如果設定為 **True**， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 就會掃描並執行伺服器上定義之所有要自動執行的預存程序。 如果設定為 **False** (預設值)，就不會執行掃描。 如需詳細資訊，請參閱 [設定 scan for startup procs 伺服器組態選項](../../database-engine/configure-windows/configure-the-scan-for-startup-procs-server-configuration-option.md)。  
  
 **兩位數年份的截止**  
 指出可用兩位數年份格式輸入的最大年份數目。 列出的年份以及前 99 年均可用兩位數年份格式輸入。 所有其他的年份都必須用四位數年份輸入。  
  
 例如，2049 的預設設定指出用 '3/14/49' 格式輸入的日期會被解譯為 2049 年 3 月 14 日，而用 '3/14/50' 格式輸入的日期會被解譯為 1950 年 3 月 14 日。 如需詳細資訊，請參閱 [設定 two digit year cutoff 伺服器組態選項](../../database-engine/configure-windows/configure-the-two-digit-year-cutoff-server-configuration-option.md)。  
  
## <a name="network"></a>Network  
 **網路封包大小**  
 設定跨越整個網路所用的封包大小 (以位元組為單位)。 預設的封包大小為 4096 個位元組。 如果應用程式進行大量複製作業，或是傳送或接收大量的 **text** 或 **image** 資料，則使用大於預設值的封包有助於改善效能，因為這樣會有較少的網路讀取與寫入。 如果應用程式傳送與接收的資訊量很少，您可以將封包大小設成 512 位元組，這對大部分的資料傳輸而言已經足夠。 如需詳細資訊，請參閱 [設定 network packet size 伺服器組態選項](../../database-engine/configure-windows/configure-the-network-packet-size-server-configuration-option.md)。  
  
> [!NOTE]  
>  除非確信有助於提升效能，否則請勿變更封包大小。 對於大部分應用程式而言，預設封包大小是最適當的大小。  
  
 **遠端登入逾時**  
 指定從失敗的遠端登入動作返回之前， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 要等候的秒數。 此設定會影響異質性查詢針對 OLE DB 提供者的連接。 預設值為 20 秒。 將值設定為 0 即可無限期等候。 如需詳細資訊，請參閱 [設定 remote login timeout 伺服器組態選項](../../database-engine/configure-windows/configure-the-remote-login-timeout-server-configuration-option.md)。  
  
 設定的變更會立即生效。  
  
## <a name="parallelism"></a>平行處理：  
 **平行處理的成本臨界值**  
 指定 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 針對查詢所建立與執行之平行計畫的臨界值。 成本是指在特定硬體組態下，估計執行序列計畫所需的已耗用時間 (以秒為單位)。 只有在使用對稱式多處理器時，才應設定此選項。 如需詳細資訊，請參閱 [設定 cost threshold for parallelism 伺服器組態選項](../../database-engine/configure-windows/configure-the-cost-threshold-for-parallelism-server-configuration-option.md)。  
  
 **鎖定**  
 設定可用鎖定的最大數目，藉此限制 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 用於鎖定的記憶體數量。 預設值是 0，允許 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 根據變更系統需求，動態配置與解除配置鎖定。  
  
 讓 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 動態地使用鎖定，是建議的設定。 如需詳細資訊，請參閱 [設定 locks 伺服器組態選項](../../database-engine/configure-windows/configure-the-locks-server-configuration-option.md)。  
  
 **平行處理原則的最大程度**  
 限制平行計畫執行期間要使用的處理器數目 (最大值為 64)。 預設值是 0，亦即使用所有可以使用的處理器。 將值設定為 1，就會抑制平行計畫的產生。 大於 1 的數目，就會限制單一查詢執行可用的最大處理器數目。 如果指定的數值大於可用的處理器數目，就會使用可用處理器的實際數目。 如需詳細資訊，請參閱 [設定 max degree of parallelism 伺服器組態選項](../../database-engine/configure-windows/configure-the-max-degree-of-parallelism-server-configuration-option.md)。  
  
 **查詢等候**  
 指定查詢在逾時之前，要等候資源的時間 (以秒為單位，從 0 到 2147483647)。如果使用預設值 -1，逾時值就會以估計之查詢成本的 25 倍計算。 如需詳細資訊，請參閱 [設定 query wait 伺服器組態選項](../../database-engine/configure-windows/configure-the-query-wait-server-configuration-option.md)。  
  
## <a name="see-also"></a>另請參閱  
 [伺服器組態選項 &#40;SQL Server&#41;](../../database-engine/configure-windows/server-configuration-options-sql-server.md)  
  
  
