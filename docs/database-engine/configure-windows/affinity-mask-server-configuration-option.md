---
title: "affinity mask 伺服器組態選項 | Microsoft Docs"
ms.custom: 
ms.date: 03/02/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- default affinity mask option
- reloading processor cache
- processor cache [SQL Server]
- CPU [SQL Server], licensing
- deferred process call
- affinity mask option
- processor affinity [SQL Server]
- SMP
- DPC
ms.assetid: 5823ba29-a75d-4b3e-ba7b-421c07ab3ac1
caps.latest.revision: "52"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: fa9d428d9565c0ac41b36869cff6ba122b516626
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/09/2017
---
# <a name="affinity-mask-server-configuration-option"></a>affinity mask 伺服器組態選項
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

    
> [!NOTE]  
>  [!INCLUDE[ssNoteDepFutureDontUse](../../includes/ssnotedepfuturedontuse-md.md)] 請改用 [ALTER SERVER CONFIGURATION &#40;Transact-SQL&#41;](../../t-sql/statements/alter-server-configuration-transact-sql.md)。  
  
 為了執行多工作業， [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows 有時會在不同的處理器之間移動處理序執行緒。 雖然從作業系統的觀點來看很有效率，但是在繁重的系統負載下，這項活動可能會降低 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的效能，因為每個處理器快取會重複地重新載入資料。 在這些情況中，將特定執行緒指定給處理器，可降低處理器重新載入的情形並減少跨處理器移轉執行緒的問題 (藉此減少內容切換)，進而提升效能，而執行緒與處理器之間的關聯則稱為處理器相似性。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 透過兩個相似性遮罩選項支援處理器相似性：affinity mask (也稱為 **CPU affinity mask**) 與 affinity I/O mask。 如需 affinity I/O mask 選項的詳細資訊，請參閱 [affinity Input-Output mask 伺服器組態選項](../../database-engine/configure-windows/affinity-input-output-mask-server-configuration-option.md)。 擁有 33 到 64 個處理器的 CPU 與 I/O 相似性支援需要分別另外使用 [affinity64 mask 伺服器組態選項](../../database-engine/configure-windows/affinity64-mask-server-configuration-option.md) 與 [affinity64 Input-Output mask 伺服器組態選項](../../database-engine/configure-windows/affinity64-input-output-mask-server-configuration-option.md)。  
  
> [!NOTE]  
>  擁有 33 到 64 個處理器之伺服器的相似性支援只能在 64 位元的作業系統上使用。  
  
 affinity mask 選項存在於較早的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]版本中，可動態控制 CPU 相似性。  
  
 在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]中，不需要重新啟動 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]執行個體，即可設定 affinity mask 選項。 使用 sp_configure 時，您必須在設定組態選項之後，執行 RECONFIGURE 或 RECONFIGURE WITH OVERRIDE。 當您使用 [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)]時，變更 affinity mask 選項後需要重新啟動。  
  
 對 affinity mask 的變更會動態發生，允許視需要啟動或關閉 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]中繫結處理序執行緒的 CPU 排程器。 這會因伺服器上的條件變更而發生。 例如，若將 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的新執行個體加入伺服器，則可能必須對 affinity mask 選項進行調整，以便分散處理器負載。  
  
 對相似性位元遮罩的修改需要 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 啟用新的 CPU 排程器並停用現有的 CPU 排程器。 然後，新批次可在新的或剩餘的排程器上加以處理。  
  
 為了啟動新的 CPU 排程器， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 會建立新的排程器，並將它加入其標準排程器的清單中。 新的排程器只能用於新內送的批次。 目前批次會繼續在相同的排程器上執行。 工作者會在釋出時或建立新工作者時，合併到新的排程器。  
  
 排程器上所有的批次都完成活動並結束，才能關閉排程器。 必須關閉的排程器會標示為離線，如此就不會在此排程器上排定新批次。  
  
 不論新增或移除新的排程器，只要伺服器保持運作，永久性系統工作就會繼續在排程器上執行，例如，鎖定監視、檢查點、系統工作執行緒 (處理 DTC) 及訊號處理序。 這些永久性系統工作不會動態地移轉。 若要將這些系統工作的處理器負載分散到不同排程器上，必須重新啟動 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體。 如果 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 嘗試關閉與永久性系統工作關聯的排程器，工作會繼續在離線的排程器上執行 (沒有移轉)。 此排程器已繫結到修改的相似性遮罩中的處理器，且不應在變更之前放置任何負載於此處理器上。 具有多餘的離線排程器並不會明顯影響到系統的負載。 如果不是這樣的狀況，重新設定這些工作需要重新啟動資料庫伺服器。  
  
 I/O affinity mask 會直接影響到 I/O 相似性工作 (例如 lazywriter 與 logwriter)。 如果 lazywriter 與 logwriter 工作並未相似化，則會遵循針對其他永久性工作所定義的相同規則，例如鎖定監視或檢查點。  
  
 為了確定新的相似性遮罩有效，RECONFIGURE 命令會驗證一般的 CPU 和 I/O 相似性是否互斥。 如果不是這樣的狀況，會將錯誤訊息回報至用戶端工作階段和 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 錯誤記錄檔，表示不建議這樣的設定。 執行 RECONFIGURE WITH OVERRIDE 選項可允許未互斥的 CPU 和 I/O 相似性。  
  
 如果您指定嘗試對應到不存在之 CPU 的相似性遮罩，RECONFIGURE 命令會將錯誤訊息回報至用戶端工作階段和 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 錯誤記錄檔。 在此情況下，使用 RECONFIGURE WITH OVERRIDE 選項沒有作用，而且會再次回報相同的組態錯誤。  
  
 您也可以從處理器中排除 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 活動，此為 Windows 2000 或 Windows Server 2003 作業系統所指定的特定工作負載。 如果將某處理器的代表位元設成 1，則表示 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Database Engine 已選取該處理器準備進行執行緒指派。 若將 **affinity mask** 設成 0 (預設值)，Microsoft Windows 2000 或 Windows Server 2003 排程演算法會設定執行緒的相似性。 將 **affinity mask** 設成任何非零的值時， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 相似性會將該值解譯為指定適合選取之處理器的位元遮罩。  
  
 藉由將 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行緒從特定處理器中分離，Microsoft Windows 2000 或 Windows Server 2003 可以更有效地評估 Windows 特定處理序的系統處理。 例如，系統管理員可以在執行兩個 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體 (執行個體 A 與 B) 的 8-CPU 伺服器上，使用 affinity mask 選項將第一組 4 個 CPU 指派到執行個體 A，並將第二組 4 個 CPU 指派到執行個體 B。若要設定 32 個以上的處理器，請同時設定 affinity mask 與 affinity64 mask。 **affinity mask** 的值如下所示：  
  
-   在多處理器的電腦中，一個位元組的 **affinity mask** 最多可涵蓋 8 個 CPU。  
  
-   在多處理器的電腦中，二個位元組的 **affinity mask** 最多可涵蓋 16 個 CPU。  
  
-   在多處理器的電腦中，三個位元組的 **affinity mask** 最多可涵蓋 24 個 CPU。  
  
-   在多處理器的電腦中，四個位元組的 **affinity mask** 最多可涵蓋 32 個 CPU。  
  
-   若要處理 32 個以上的 CPU，請針對前 32 個 CPU 設定四個位元組的相似性遮罩，並針對剩餘的 CPU 設定最多四個位元組的 affinity64 遮罩。  
  
 因為設定 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 處理器相似性是專門的作業，建議您只在必要時才使用。 在大部分情況下，Microsoft Windows 2000 或 Windows Server 2003 的預設相似性可提供最佳效能。 您也應該在設定相似性遮罩時，考量其他應用程式的 CPU 需求。 如需詳細資訊，請參閱您的 Windows 作業系統文件集。  
  
> [!NOTE]  
>  您可使用「Windows 系統監視器」來檢視和分析個別處理器的使用方式。  
  
 在指定 affinity I/O mask 選項時，您必須與 affinity mask 組態選項連接使用。 請勿同時在 **affinity mask** 參數與 affinity I/O mask 選項中啟用相同的 CPU。 對應到每個 CPU 的位元組狀態應為下列三個的其中一個：  
  
-   在 affinity mask 選項與 affinity I/O mask 選項中皆為 0。  
  
-   在 affinity mask 選項中為 1，而在 affinity I/O mask 選項中為 0。  
  
-   在 affinity mask 選項中為 0，在 affinity I/O mask 選項中為 1。  
  
> [!CAUTION]  
>  不要在 Windows 作業系統中設定 CPU 相似性，然後又在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]中設定相似性遮罩。 這些設定嘗試達到相同的結果，如果組態不一致，可能會有無法預期的結果。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 設定 CPU 相似性時，最好使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]中的 sp_configure 選項。  
  
## <a name="example"></a>範例  
 以設定 affinity mask 選項為例，如果選取處理器 1、2 與 5 為可用，並將位元 1、2、5 設成 1，位元 0、3、4、6 與 7 設成 0，就會指定十六進位值 0x26 (或相當的十進位值 `38` )。 位元的編號從右算起。 affinity mask 選項會從 0 到 31 開始計算處理器，所以在下列範例中，計數器 `1` 代表伺服器上的第二個處理器。  
  
```  
sp_configure 'show advanced options', 1;  
RECONFIGURE;  
GO  
sp_configure 'affinity mask', 38;  
RECONFIGURE;  
GO  
```  
  
 以下為 8-CPU 系統的 **affinity mask** 值。  
  
|十進位值|二進位位元遮罩|允許 SQL Server 執行緒的處理器數目|  
|-------------------|---------------------|--------------------------------------------|  
|1|00000001|0|  
|3|00000011|0 與 1|  
|7|00000111|0、1 與 2|  
|15|00001111|0、1、2 與 3|  
|31|00011111|0、1、2、3 與 4|  
|63|00111111|0、1、2、3、4 與 5|  
|127|01111111|0、1、2、3、4、5 與 6|  
|255|11111111|0、1、2、3、4、5、6 與 7|  
  
 affinity mask 屬於進階選項。 若使用 sp_configure 系統預存程序來變更設定，只有當 **show advanced options** 設為 1 時，才能變更 **affinity mask** 。 在執行 [!INCLUDE[tsql](../../includes/tsql-md.md)] RECONFIGURE 命令之後，新的設定會立即生效，而不需要重新啟動 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體。  
  
## <a name="non-uniform-memory-access-numa"></a>非統一記憶體存取 (NUMA)  
 當使用以非統一記憶體存取 (NUMA) 為基礎的硬體且設定相似性遮罩時，節點中的每一個排程器將相似於它自己的 CPU。 若未設定相似性遮罩，則每一個排程器會相似於 NUMA 節點內的 CPU 群組，且對應到 NUMA 節點 N1 的排程器可在該節點的任何 CPU 上設定工作排程，但不能在與另一個節點相關聯的 CPU 上設定。  
  
 在單一 NUMA 節點上執行的任何作業只能使用該節點的緩衝區頁面。 若作業平行執行於多個節點的 CPU 上，則可使用任何相關節點的記憶體。  
  
## <a name="licensing-issues"></a>授權問題  
 動態相似性受到 CPU 授權的嚴格控制， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 並不允許違反授權原則的任何相似性遮罩選項組態。  
  
### <a name="startup"></a>啟動  
 如果指定的相似性遮罩在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 啟動期間或資料庫附加期間違反授權原則，則引擎層會完成啟動程序或資料庫附加/還原作業，然後將相似性遮罩的 sp_configure 執行值重設為零，發出錯誤訊息至 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 錯誤記錄檔。  
  
### <a name="reconfigure"></a>重新設定  
 如果指定的相似性遮罩在執行 [!INCLUDE[tsql](../../includes/tsql-md.md)] RECONFIGURE 命令期間違反授權原則，就會將錯誤訊息回報至用戶端工作階段和 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 錯誤記錄檔，並要求資料庫管理員重新設定相似性遮罩。 在此情況下，不會接受任何 RECONFIGURE WITH OVERRIDE 命令。  
  
## <a name="see-also"></a>另請參閱  
 [監視資源使用狀況 &#40;系統監視器&#41;](../../relational-databases/performance-monitor/monitor-resource-usage-system-monitor.md)   
 [RECONFIGURE &#40;Transact-SQL&#41;](../../t-sql/language-elements/reconfigure-transact-sql.md)   
 [伺服器組態選項 &#40;SQL Server&#41;](../../database-engine/configure-windows/server-configuration-options-sql-server.md)   
 [sp_configure &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md)   
 [ALTER SERVER CONFIGURATION &#40;Transact-SQL&#41;](../../t-sql/statements/alter-server-configuration-transact-sql.md)  
  
  
