---
title: affinity mask 伺服器組態選項
description: 了解 SQL Server 中的 [親和性遮罩] 選項。 檢視使用此選項以將處理器繫結至特定執行緒的範例。
ms.prod: sql
ms.prod_service: high-availability
ms.technology: configuration
ms.topic: conceptual
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
author: markingmyname
ms.author: maghan
ms.reviewer: mikeray
ms.custom: ''
ms.date: 06/11/2020
ms.openlocfilehash: 94f8406af013bc0720bc16063d1a9881eda94c5a
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/01/2020
ms.locfileid: "85715591"
---
# <a name="affinity-mask-server-configuration-option"></a>affinity mask 伺服器組態選項

 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

> [!NOTE]
> [!INCLUDE[ssNoteDepFutureDontUse](../../includes/ssnotedepfuturedontuse-md.md)] 請改用 [ALTER SERVER CONFIGURATION &#40;Transact-SQL&#41;](../../t-sql/statements/alter-server-configuration-transact-sql.md)。

為了執行多工作業， [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows 有時會在不同的處理器之間移動處理序執行緒。 雖然從作業系統的觀點來看很有效率，但是在繁重的系統負載下，此活動可能會降低 SQL Server 效能，因為每個處理器快取都會重複地重新載入資料。 將處理器指派給特定的執行緒，可藉由消除處理器重新載入，並減少處理器之間的執行緒移轉 (可減少環境切換)，在這些狀況下增進效能。 執行緒與處理器之間的這種關聯，稱為處理器親和性。

SQL Server 透過兩個親和性遮罩選項來支援處理器親和性：親和性遮罩 (也稱為 **CPU 親和性遮罩**) 與親和性 I/O 遮罩。 如需 [親和性 I/O 遮罩] 選項的詳細資訊，請參閱 [affinity Input-Output mask 伺服器組態選項](../../database-engine/configure-windows/affinity-input-output-mask-server-configuration-option.md)。 擁有 33 到 64 個處理器的 CPU 與 I/O 相似性支援需要分別另外使用 [affinity64 mask 伺服器組態選項](../../database-engine/configure-windows/affinity64-mask-server-configuration-option.md) 與 [affinity64 Input-Output mask 伺服器組態選項](../../database-engine/configure-windows/affinity64-input-output-mask-server-configuration-option.md)。

> [!NOTE]  
> 擁有 33 到 64 個處理器之伺服器的相似性支援只能在 64 位元的作業系統上使用。

[親和性遮罩] 選項存在於較早的 SQL Server 版本中，可動態控制 CPU 親和性。

在 SQL Server 中，不需要重新啟動 SQL Server 執行個體，即可設定 [親和性遮罩] 選項。 使用 sp_configure 時，您必須在設定組態選項之後，執行 RECONFIGURE 或 RECONFIGURE WITH OVERRIDE。 當您使用 [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)] 時，變更 [親和性遮罩] 選項需要重新啟動。

對親和性遮罩的變更會動態發生，允許視需要啟動或關閉 SQL Server 中繫結處理序執行緒的 CPU 排程器。 這會因伺服器上的條件變更而發生。 例如，若要將 SQL Server 的新執行個體新增至伺服器，可能必須對 [親和性遮罩] 選項進行調整，以便重新散發處理器負載。

對親和性位元遮罩的修改，需要 SQL Server 啟用新的 CPU 排程器，並停用現有的 CPU 排程器。 然後，新批次可在新的或剩餘的排程器上加以處理。

為了啟動新的 CPU 排程器，SQL Server 會建立新的排程器，並新增至其標準排程器的清單。 新的排程器只能用於新內送的批次。 目前批次會繼續在相同的排程器上執行。 工作者會在釋出時或建立新工作者時，合併到新的排程器。

排程器上所有的批次都完成活動並結束，才能關閉排程器。 必須關閉的排程器會標示為離線，如此就不會在此排程器上排定新批次。

不論新增或移除新的排程器，只要伺服器保持運作，永久性系統工作就會繼續在排程器上執行，例如，鎖定監視、檢查點、系統工作執行緒 (處理 DTC) 及訊號處理序。 這些永久性系統工作不會動態地移轉。 若要將這些系統工作的處理器負載重新散發到不同排程器上，必須重新啟動 SQL Server 執行個體。 如果 SQL Server 嘗試關閉與永久性系統工作相關聯的排程器，該工作就會繼續在離線的排程器上執行 (沒有移轉)。 此排程器會繫結到已修改之親和性遮罩中的處理器，而且不會在其於變更之前已繫結的處理器上放置任何負載。 具有多餘的離線排程器，應該不會對系統負載造成顯著影響。 如果是這樣，則需要將資料庫伺服器重新開機，才能在使用已修改之親和性遮罩所提供的排程器上重新設定這些工作。

請勿將 SQL Server 的 [親和性遮罩] 和 [親和性 I/O 遮罩] 組態值設定為使用相同的 CPU。 如果您選擇繫結處理器來進行 SQL Server 背景工作執行緒排程和 I/O 處理，效能可能就會受到影響。 因此，請確定並未針對相同的處理器設定組態值。 相同的建議適用於 'affinity64 mask' 和 'affinity64 I/O mask'。  為了確定親和性遮罩不會與親和性 I/O 遮罩重疊，[RECONFIGURE](../../t-sql/language-elements/reconfigure-transact-sql.md) 命令會驗證一般的 CPU 和 I/O 親和性是否互斥。 如果不會，即會向用戶端工作階段和 SQL Server 錯誤記錄檔回報錯誤訊息，指出不建議這樣的設定。

```sql
 Msg 5834, Level 16, State 1, Line 1
 The affinity mask specified conflicts with the IO affinity mask specified. Use the override option to force this configuration
```

執行 RECONFIGURE WITH OVERRIDE 選項，允許 CPU 和 I/O 親和性重疊且不會互斥。  

I/O 親和性遮罩會直接影響 I/O 親和性工作 (例如，延遲寫入器與記錄寫入器)。 如果延遲寫入器與記錄寫入器工作並未繫結，其會遵循針對其他永久性工作 (例如，鎖定監視或檢查點) 所定義的相同規則。
如果您指定嘗試對應到不存在 CPU 的親和性遮罩，RECONFIGURE 命令就會將錯誤訊息回報至用戶端工作階段和 SQL Server 錯誤記錄檔。 在此情況下，使用 RECONFIGURE WITH OVERRIDE 選項沒有作用，而且會再次回報相同的組態錯誤。

您也可以依 Windows 作業系統，從特定工作負載指派中排除 SQL Server 活動。 如果將代表處理器的位元設為 1，SQL Server 資料庫引擎就會選取該處理器來進行執行緒指派。 當您將 [親和性遮罩] 設為 0 (預設值) 時，Microsoft Windows 排程演算法會設定執行緒的親和性。 當您將 [親和性遮罩] 設為任何非零的值時，SQL Server 親和性會將該值解譯為指定適合選取之處理器的位元遮罩。  

藉由將 SQL Server 執行緒從在特定處理器上執行分離出來，Microsoft Windows 可以更有效地評估 Windows 特定處理序的系統處理。 例如，系統管理員可以在執行兩個 SQL Server 執行個體 (執行個體 A 與 B) 的 8-CPU 伺服器上，使用 [親和性遮罩] 選項來將第一組 4 個 CPU 指派到執行個體 A，並將第二組 4 個 CPU 指派到執行個體 B。若要設定 32 個以上的處理器，請同時設定 [親和性遮罩] 與 affinity64 mask。 **affinity mask** 的值如下所示：

- 在多處理器的電腦中，一個位元組的 **affinity mask** 最多可涵蓋 8 個 CPU。

- 在多處理器的電腦中，二個位元組的 **affinity mask** 最多可涵蓋 16 個 CPU。

- 在多處理器的電腦中，三個位元組的 **affinity mask** 最多可涵蓋 24 個 CPU。

- 在多處理器的電腦中，四個位元組的 **affinity mask** 最多可涵蓋 32 個 CPU。

- 若要處理 32 個以上的 CPU，請針對前 32 個 CPU 設定四個位元組的相似性遮罩，並針對剩餘的 CPU 設定最多四個位元組的 affinity64 遮罩。

因為設定 SQL Server 處理器親和性是特殊作業，建議您只在必要時才使用。 在大部分情況下，Microsoft Windows 的預設親和性可提供最佳效能。 設定親和性遮罩時，請考量其他應用程式的 CPU 需求。 如需詳細資訊，請參閱您的 Windows 作業系統文件集。

> [!NOTE]
> 您可使用「Windows 系統監視器」來檢視和分析個別處理器的使用方式。

指定 [親和性 I/O 遮罩] 選項時，您必須搭配使用 [親和性遮罩] 組態選項。 請勿同時在 [親和性遮罩] 切換開關與 [親和性 I/O 遮罩] 選項中啟用相同的 CPU。 對應到每個 CPU 的位元組狀態應為下列三個的其中一個：

- 在 affinity mask 選項與 affinity I/O mask 選項中皆為 0。

- 在 affinity mask 選項中為 1，而在 affinity I/O mask 選項中為 0。

- 在 affinity mask 選項中為 0，在 affinity I/O mask 選項中為 1。

> [!CAUTION]
> 不要在 Windows 作業系統中設定 CPU 親和性，同時又在 SQL Server 中設定親和性遮罩。 這些設定嘗試達到相同的結果，如果組態不一致，可能會有無法預期的結果。 設定 SQL Server CPU 親和性時，最好使用 SQL Server 中的 sp_configure 選項。

## <a name="example"></a>範例

以設定 [親和性遮罩] 選項為例，如果選取處理器 1、2 與 5 為可用，並將位置 1、2、5 中的位元設為 1，且將位元 0、3、4、6 與 7 設為 0，就必須使用十六進位值 0x26 (或對等的十進位值 38)。 由右至左為位元位置編號。

```sql
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

affinity mask 屬於進階選項。 如果使用 sp_configure 系統預存程序來變更設定，只有當 [顯示進階選項] 設為 1 時，才能變更**親和性遮罩**。 執行 [!INCLUDE[tsql](../../includes/tsql-md.md)] RECONFIGURE 命令之後，新的設定會立即生效，而不需重新啟動 SQL Server 執行個體。  

## <a name="non-uniform-memory-access-numa"></a>非統一記憶體存取 (NUMA)

使用以硬體為基礎的非統一記憶體存取 (NUMA) 且設定了親和性遮罩時，節點中的每個排程器都會繫結至自己的 CPU。 若未設定親和性遮罩，則每個排程器都會繫結至 NUMA 節點內的 CPU 群組，而對應到 NUMA 節點 N1 的排程器可在該節點中的任何 CPU 上排程工作，但不能在與另一個節點相關聯的 CPU 上進行排程。  

在單一 NUMA 節點上執行的任何作業只能使用該節點的緩衝區頁面。 若作業平行執行於多個節點的 CPU 上，則可使用任何相關節點的記憶體。  
  
## <a name="licensing-issues"></a>授權問題

動態相似性受到 CPU 授權的嚴格控制， SQL Server 不允許違反授權原則的任何親和性遮罩選項組態。  

### <a name="startup"></a>啟動

如果指定的親和性遮罩在 SQL Server 啟動期間或在資料庫附加期間違反授權原則，引擎層會完成啟動程序或資料庫附加/還原作業，然後將親和性遮罩的 sp_configure 執行值重設為零，以便向 SQL Server 錯誤記錄檔發出錯誤訊息。  
  
### <a name="reconfigure"></a>重新設定

如果指定的親和性遮罩在執行 [!INCLUDE[tsql](../../includes/tsql-md.md)] RECONFIGURE 命令期間違反授權原則，就會向用戶端工作階段和 SQL Server 錯誤記錄檔回報錯誤訊息，並要求資料庫管理員重新設定親和性遮罩。 在此情況下，不會接受任何 RECONFIGURE WITH OVERRIDE 命令。  

## <a name="next-steps"></a>後續步驟

- [監視資源使用狀況 &#40;System Monitor&#41;](../../relational-databases/performance-monitor/monitor-resource-usage-system-monitor.md)
- [RECONFIGURE &#40;Transact-SQL&#41;](../../t-sql/language-elements/reconfigure-transact-sql.md)
- [伺服器組態選項 &#40;SQL Server&#41;](../../database-engine/configure-windows/server-configuration-options-sql-server.md)
- [sp_configure &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md)
- [ALTER SERVER CONFIGURATION &#40;Transact-SQL&#41;](../../t-sql/statements/alter-server-configuration-transact-sql.md)
