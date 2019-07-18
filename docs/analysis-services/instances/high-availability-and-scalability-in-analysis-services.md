---
title: Analysis Services 的高可用性與延展性 |Microsoft Docs
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: ''
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 09fc0a9d9814a399d679b1391678fb5e11ad8a3f
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "68181520"
---
# <a name="high-availability-and-scalability-in-analysis-services"></a>Analysis Services 的高可用性與延展性
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  本文說明提高 Analysis Services 資料庫高度可用且可擴充的最常用的技術。 雖然您可以個別達成每個目標，但實際上這兩個目標經常相互關聯︰可針對大型查詢或處理工作負載擴充的部署通常預期要有高可用性。  
  
 不過反之則不一定。 當任務關鍵性但中等的查詢工作負載有嚴格的服務等級協定時，可以將不含延展性的高可用性當做唯一的目標。  
  
 所有伺服器模式 (多維度、表格式和 SharePoint 整合模式) 通常都會使用相同的技術來提高 Analysis Services 可用性與延展性。 除非另有明確指示，否則您應該假設本文中的資訊適用於所有模式。  
  
## <a name="key-points"></a>重點  
 因為可用性與延展性的技術與關聯式資料庫引擎的技術不同，簡短的重點摘要可有效地介紹搭配 Analysis Services 使用的技術︰  
  
-   Analysis Services 利用內建於 Windows Server 平台的高可用性與延展性機制︰網路負載平衡 (NLB) 及 (或) Window Server 容錯移轉叢集 (WSFC)。  
  
    > [!NOTE]  
    >  關聯式資料庫引擎的 AlwaysOn 功能無法擴充至 Analysis Services。  您無法設定 Analysis Services 執行個體在 AlwaysOn 可用性群組中執行。  
    >   
    >  雖然 Analysis Services 不會在 AlwaysOn 可用性群組中執行，但是它可以從 AlwaysOn 關聯式資料庫擷取及處理資料。 如需如何設定高度可用的關聯式資料庫以供 Analysis Services 使用的指示，請參閱 [Analysis Services 與 AlwaysOn 可用性群組](../../database-engine/availability-groups/windows/analysis-services-with-always-on-availability-groups.md)。  
  
-   高可用性作為唯一的目標時，可透過容錯移轉叢集中的伺服器備援達成。取代節點會假設與作用中節點具有完全相同的硬體及軟體組態。  單獨使用時，WSFC 會為您提供高可用性，但無法調整大小。  
  
-   延展性 (不論是否包含可用性) 可透過唯讀資料庫上的 NLB 來達成。  當查詢量很大或可能突然增加時，通常會考慮延展性。  
  
     負載平衡結合多部唯讀資料庫可同時提供您延展性與高可用性，因為所有節點都在作用中，而且當伺服器關閉時，要求會自動重新分配到其餘節點。 若您同時需要延展性與可用性，NLB 叢集會是適當的選擇。  
  
 進行處理時，高可用性與延展性目標則較不重要，因為您可以控制作業的時間與範圍。 您可以針對模型的各部分進行部分及累加處理，不過有時您需要在單一伺服器上處理整個模型，以確保所有索引和彙總之間的資料一致性。 強固且可擴充的架構有賴於能因應任何速度要求進行完整處理的硬體。 針對大型方案，這項工作會結構化為獨立作業，並具有自己的硬體資源。  
  
##  <a name="bkmk_serverconfig"></a> 單一和多伺服器組態  
 在一般的單一伺服器部署中，處理和查詢工作負載會同時執行 (假設系統資源足夠這兩個活動使用)。 Analysis Services 會保留現有的資料結構不變以支援查詢，同時在背景處理更新的版本。 所有伺服器模式都要求硬體具有足以處理暫存資料結構的記憶體和磁碟空間，不過每個模式對於系統資源還有不同的需求，並且具有不同的 NUMA 感知層級。  
  
 **單一伺服器和延展性**  
  
 單一高階、多核心伺服器本身可能會提供足夠的規模。 在具有大量核心、RAM 和磁碟空間的高階系統上，您可以在單一系統內相應增加。  
  
 針對多維度資料庫，您可以調整伺服器組態屬性，以建立處理序和處理器之間的相似性。 如需相關資訊，請參閱 [Thread Pool Properties](../../analysis-services/server-properties/thread-pool-properties.md) 。  
  
 **多伺服器部署**  
  
 有時作業需求會指定使用多部伺服器。 例如，容錯移轉叢集根據定義是多伺服器，其每個節點會在完全相同的硬體和軟體組態上執行。  
  
 同樣地，迫切需要高可用性的查詢工作負載通常需要有多部伺服器。 在此情況下，Analysis Services 的建議組態是混合使用在專用硬體的個別 Analysis Services 執行個體上執行的唯讀和讀寫資料庫。 唯讀資料庫處理查詢要求。 讀寫資料庫用於處理。 下一節將提供此常用技術的進一步說明。  
  
 **虛擬機器和高可用性**  
  
 達成高可用性需求的另一個策略可能會用到虛擬機器。 若可用性的滿足條件是在幾小時內 (而不是在幾分鐘內) 有取代伺服器，您可以使用虛擬機器，在需要時才啟動，並載入從中央位置擷取的已更新資料庫。  
  
## <a name="scalability-using-read-only-and-read-write-databases"></a>使用唯讀和讀寫資料庫的延展性  
 建議針對很高或節節升高的查詢和處理工作負載平衡其網路負載。 NLB 方案中的 Analysis Services 資料庫會定義為唯讀資料庫，以確保查詢之間的一致性。  
  
 雖然 [Scale-out querying for Analysis Services using read-only databases](https://technet.microsoft.com/library/ff795582\(v=sql.100\).aspx) (使用唯讀資料庫向外延展 Analysis Services 的查詢) 中的指引 (發佈於 2008 年) 已過時，但通常仍然有效。 雖然伺服器作業系統和電腦硬體的改進使得特定平台和 CPU 限制的參考資料過時，但是針對大量查詢使用唯讀和讀寫資料庫的基本技術仍然不變。  
  
 此方法可以摘要如下：  
  
-   使用專用硬體和 Analysis Services 執行個體來處理資料庫。 處理完成之後，將資料庫設成唯讀。 如需相關指示，請參閱＜ [Switch an Analysis Services database between ReadOnly and ReadWrite modes](../../analysis-services/multidimensional-models/switch-an-analysis-services-database-between-readonly-and-readwrite-modes.md) ＞。  
  
-   使用多部完全相同的查詢伺服器，執行同一個唯讀 Analysis Services 資料庫的多個複本。 伺服器會部署到 NLB 叢集中，並透過一個虛擬伺服器名稱 (作為叢集的單一進入點) 進行存取。  
  
-   使用 robocopy 將整個資料目錄從處理伺服器複製到每部查詢伺服器，並將唯讀模式的相同資料庫附加至所有查詢伺服器。 您也可以使用 SAN 快照集、同步處理，或是您用來移動生產資料庫的任何其他工具或方法  
  
## <a name="resource-demands-for-tabular-and-multidimensional-workloads"></a>表格式和多維度工作負載的資源需求  
 下表是 Analysis Services 如何使用系統資源進行查詢及處理的高階摘要，並依伺服器和儲存模式來區隔。 此摘要可協助您了解處理分散式工作負載的多伺服器部署的強調重點。  
  
|||  
|-|-|  
|**伺服器和儲存模式**|**系統資源的影響**|  
|記憶體內部表格式 (預設值)，其中查詢會當做記憶體內部資料結構的資料表掃描來執行。|強調 RAM 和 CPU，並具有很快的時脈速度。|  
|DirectQuery 模式中的表格式，其中查詢會卸載至後端關聯式資料庫伺服器，且處理僅限於建構模型的中繼資料。|專注於關聯式資料庫效能、降低網路延遲，並最大化輸送量。 更快速的 CPU 也會改善 Analysis Services 查詢處理器的效能。|  
|使用 MOLAP 儲存的多維度模型。|選擇平衡的組態，以提供可快速載入資料的磁碟 IO，並具有足夠的 RAM 來處理快取的資料。|  
|使用 ROLAP 儲存的多維度模型。|最大化磁碟 IO，並將網路延遲降至最低。|  
  
## <a name="high-availability-and-redundancy-through-wsfc"></a>高可用性與備援透過 WSFC  
 Analysis Services 可安裝到現有的 Windows Server 容錯移轉叢集 (WSFC) 以取得高可用性，盡可能在最短的時間內還原服務。  
  
 容錯移轉叢集提供資料庫的完整存取權 (讀取和回寫)，但一次只會針對一個節點。 次要資料庫會在叢集中的額外節點上執行，並在第一個節點關閉時作為取代伺服器。  
  
 容錯移轉叢集的主要優點是從服務失敗中快速復原。 此優點有一些限制。 例如，若永不需要容錯移轉，叢集中的專用資源會處於閒置狀態。 其次，若發生容錯移轉，所有連接都會中斷，而對應的未認可工作將會遺失。 大部分的用戶端應用程式應該都能夠處理這個狀況。通常，按下應用程式中的重新整理按鈕就會讓結果恢復。 
 
 在考慮 WSFC 時，請記住下列幾點︰

- 目前不支援主動/主動。 主動/被動 (容錯移轉) 是唯一支援之適用於 Analysis Services 的 WSFC 組態。
- 在對 Analysis Services 進行叢集化時，請確定在叢集中參與之任何節點於相同或非常相似的硬體上執行，且每個節點在作業系統版本和 service pack、Analysis Services 版本和服務套件 (或累計更新)，以及伺服器模式等方面都有相同的操作內容。
- 請避免重新排定為另一個工作負載的作用中節點的被動節點。 如果節點無法處理這兩個工作負載，在實際容錯移轉狀況時會失去任何短期提升電腦使用量的機會。
 
 此白皮書提供深入指示和容錯移轉叢集中部署 Analysis Services 的背景資訊：[如何叢集化 SQL Server Analysis Services](https://msdn.microsoft.com/library/dn736073.aspx)。 雖然本指引是針對 SQL Server 2012 所撰寫，但仍適用於較新版本的 Analysis Services。  
  
## <a name="see-also"></a>另請參閱  
 [同步處理 Analysis Services 資料庫](../../analysis-services/multidimensional-models/synchronize-analysis-services-databases.md)   
 [Forcing NUMA affinity for Analysis Services Tabular Databases (對 Analysis Services 表格式資料庫強制執行 NUMA 相似性)](https://blogs.msdn.microsoft.com/sqlcat/2013/11/05/forcing-numa-node-affinity-for-analysis-services-tabular-databases/)   
 [Analysis Services 案例研究：在大規模商業解決方案中使用表格式模型](https://msdn.microsoft.com/library/dn751533.aspx)  
  
  
