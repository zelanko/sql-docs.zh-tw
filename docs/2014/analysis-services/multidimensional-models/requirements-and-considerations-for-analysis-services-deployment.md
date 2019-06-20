---
title: 需求和考量的 Analysis Services 部署 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- memory [Analysis Services]
- scalability [Analysis Services]
- space [Analysis Services]
- Analysis Services deployments, requirements
- deploying [Analysis Services], requirements
- disk space [Analysis Services]
- requirements [Analysis Services]
- processors [Analysis Services]
- system requirements [Analysis Services]
- availability [Analysis Services]
ms.assetid: ef1387a5-5137-4ef4-b731-fec347e5f5ed
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: d41f61233bbbcb6c49d4980a3265726280627860
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "66073166"
---
# <a name="requirements-and-considerations-for-analysis-services-deployment"></a>Analysis Services 部署的需求和考量
  方案的效能和可用性取決於許多因素，包括基礎硬體的功能、伺服器部署的拓撲、方案的特性 (例如，具有跨多部伺服器分散的資料分割，或使用需要直接存取關聯式引擎的 ROLAP 儲存)、伺服器等級協定，以及資料模型的複雜性。  
  
## <a name="memory-and-processor-requirements"></a>記憶體和處理器需求  
 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 需要較多的記憶體和處理器資源：  
  
-   處理大型或複雜的 Cube 時。 這些需要比處理小型或簡單的 Cube 更多的記憶體和處理器資源。  
  
-   當單一資料庫內的 Cube 數目增加時。  
  
-   當 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 的單一執行個體內的資料庫數目增加時。  
  
-   當單一電腦上的 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 執行個體數目增加時。  
  
-   當同時存取 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 資源的使用者數量增加時。  
  
 可供 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 使用的記憶體和處理器資源數量會因 SQL Server 版本、作業系統、硬體功能以及您是使用虛擬還是實體處理器而異。 如需詳細資訊，請追蹤下列連結：  
  
 [安裝 SQL Server 2014 的硬體與軟體需求](../../sql-server/install/hardware-and-software-requirements-for-installing-sql-server.md)  
  
 [SQL Server 版本的計算容量限制](../../sql-server/compute-capacity-limits-by-edition-of-sql-server.md)  
  
 [SQL Server 2014 各版本所支援的功能](../../getting-started/features-supported-by-the-editions-of-sql-server-2014.md)  
  
 [最大容量規格 &#40;Analysis Services&#41;](olap-physical/maximum-capacity-specifications-analysis-services.md)  
  
## <a name="disk-space-requirements"></a>磁碟空間需求  
 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 安裝的差異以及物件處理工作的差異，會有不同的磁碟空間需求。 下列清單描述這些需求。  
  
 Cube  
 有大型事實資料表的 Cube 所需要的磁碟空間，會比小型事實資料表的 Cube 更多。 同樣地，雖然差異幅度較小，有許多大型維度的 Cube 對於所需要的磁碟空間，會比有較少維度成員的 Cube 更多。 一般而言，您可以預測 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 資料庫所需的磁碟空間，會是基礎關聯式資料庫中所儲存相同資料之空間的 20% 左右。  
  
 Aggregations  
 彙總需要的額外空間來加入的彙總成正比有更多的彙總，則需要更多的空間。 如果您有避免建立不需要的彙總，則彙總需要的額外磁碟空間，通常不會超過基礎關聯式資料庫中所儲存資料大小的 10% 左右。  
  
 資料採礦  
 依預設，採礦結構會將定型資料集快取至磁碟。 若要從磁碟中移除此快取資料，您可以對採礦結構物件使用 **[處理清除結構]** 處理選項。 如需詳細資訊，請參閱[處理需求和考量 &#40;資料採礦&#41;](../data-mining/processing-requirements-and-considerations-data-mining.md)。  
  
 物件處理  
 在處理期間， [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 會將正在處理交易中處理的物件副本儲存到磁碟上，直到處理完成為止。 處理完成時，物件的已處理副本就會取代原始物件。 因此，您必須提供足夠的額外磁碟空間，給要處理的每一個物件的第二個副本。 例如，如果您打算在單一交易中處理整個 Cube，您需要足夠的磁碟空間來儲存整個 Cube 的第二個副本。  
  
##  <a name="BKMK_Availability"></a> 可用性考量  
 在 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 環境中，可能會因為硬體或軟體的失敗，而無法使用 Cube 或採礦模型來進行查詢。 Cube 也可能因為需要進行處理而無法使用。  
  
### <a name="providing-availability-in-the-event-of-hardware-or-software-failures"></a>在硬體或軟體失敗時維持可用性  
 硬體或軟體可能因為不同原因而失敗。 不過，維護 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 安裝的可用性不只需要進行失敗原因的疑難排解，也需要提供替代資源，讓使用者可以在發生失敗時繼續使用系統。 叢集和負載平衡伺服器通常會用於因應硬體或軟體失敗時，當做維護可用性的替代資源。  
  
 若要在發生硬體或軟體失敗時維持可用性，請考慮將 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 部署到容錯移轉叢集。 在容錯移轉叢集中，如果主要節點因任何原因失敗，或必須重開機， [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows Clustering 就會容錯移轉至次要節點。 發生非常快速的容錯移轉之後，當使用者執行查詢時，他們存取的就會是在次要節點上執行的 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 執行個體。 如需有關容錯移轉叢集的詳細資訊，請參閱[Windows Server 技術：容錯移轉叢集](https://technet.microsoft.com/library/cc732488\(v=WS.10\).aspx)。  
  
 可用性問題的另一個解決方案，是將 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 專案部署到兩個以上的實際伺服器。 然後，您就可以使用 Windows 伺服器的 Network Load Balancing (NLB) 功能，將這些實際伺服器結合成單一叢集。 在 NLB 叢集中，如果叢集的伺服器因為硬體或軟體問題而無法使用，NLB 服務就會將使用者查詢引導至仍然可使用的伺服器。  
  
### <a name="providing-availability-while-processing-structural-changes"></a>處理結構化變更時維持可用性  
 Cube 的某些變更會造成 Cube 無法使用，直到處理過為止。 例如，如果您對 Cube 的維度做了結構化變更，即使重新處理維度，每一個使用已修改維度的 Cube 也必須重新處理過。 在您處理那些 Cube 之前，使用者無法查詢它們，也不能查詢以含有修改過維度之 Cube 為基礎的任何採礦模型。  
  
 結構化變更可能會影響 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 專案中的一個或多個 Cube，若要在處理結構化變更時維持可用性，請考慮納入臨時伺服器以及使用同步處理資料庫精靈。 此功能可讓您在臨時伺服器上更新資料和中繼資料，然後在實際伺服器和臨時伺服器之間進行線上同步處理。 如需詳細資訊，請參閱 [Synchronize Analysis Services Databases](synchronize-analysis-services-databases.md)。  
  
 若要直接在背景處理來源資料的累加更新，請啟用主動式快取。 主動式快取會自動以新的來源資料更新 Cube，不需要手動處理且不影響 Cube 的可用性。 如需詳細資訊，請參閱[主動式快取 &#40;資料分割&#41;](../multidimensional-models-olap-logical-cube-objects/partitions-proactive-caching.md)。  
  
##  <a name="BKMK_Scalability"></a> 延展性考量  
 在相同電腦上的 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 和 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 的多個執行個體，可能會造成效能問題。 若要解決這些問題，可增加伺服器上的處理器、記憶體和磁碟資源。 不過，您可能也需要在多部電腦上調整 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 和 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 執行個體的延展。  
  
### <a name="scaling-analysis-services-across-multiple-computers"></a>在多部電腦上調整 Analysis Services 的延展  
 有幾個方法可調整延展至多部電腦上的 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 安裝。 下列清單描述這些選項。  
  
-   如果在單一電腦上有多個 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 執行個體，您可以將一個或多個執行個體移到另一部電腦上。  
  
-   如果在單一電腦上有多個 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 資料庫，您可以將一個或多個資料庫移到另一部電腦上的個別 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 執行個體中。  
  
-   如果有一個或多個提供資料給 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 資料庫的關聯式資料庫，您可以將這些資料庫移到另一部電腦上。 在移動資料庫之前，請考慮 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 資料庫及其基礎資料庫之間的網路速度和頻寬。 如果網路太慢或壅塞，將基礎資料庫移到另一部電腦上會降低處理效能。  
  
-   如果處理會影響查詢效能，但您無法降低的查詢負載中的時間處理，請考慮將處理工作移到預備伺服器，然後再執行 實際執行伺服器，而預備伺服器的線上同步處理。 如需詳細資訊，請參閱 [Synchronize Analysis Services Databases](synchronize-analysis-services-databases.md)。 您也可以使用遠端資料分割，在 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 的多個執行個體上分散處理。 處理遠端資料分割時會使用遠端伺服器上的處理器和記憶體資源，而非本機電腦上的資源。 如需遠端資料分割管理的資訊，請參閱[建立及管理遠端資料分割 &#40;Analysis Services&#41;](create-and-manage-a-remote-partition-analysis-services.md)。  
  
-   如果查詢效能不佳，但您無法在本機伺服器上增加處理器和記憶體資源，請考慮將 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 專案部署到兩個以上的實際伺服器。 然後，您就可以使用 Network Load Balancing (NLB) 將伺服器結合到單一叢集中。 在 NLB 叢集中，查詢會自動分散到 NLB 叢集的所有伺服器上。  
  
  
