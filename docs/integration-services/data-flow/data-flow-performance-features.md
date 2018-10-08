---
title: 資料流程效能功能 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- Aggregate transformation [Integration Services]
- Integration Services packages, performance
- performance [Integration Services]
- data flow [Integration Services], troubleshooting
- SQL Server Integration Services packages, performance
- loading data
- control flow [Integration Services], troubleshooting
- SSIS packages, performance
- packages [Integration Services], performance
- queries [Integration Services], troubleshooting
- sorting data [Integration Services]
- aggregations [Integration Services]
ms.assetid: c4bbefa6-172b-4547-99a1-a0b38e3e2b05
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: bb243fa126fc53282bd310d3bd5d47029e2f4aba
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47605828"
---
# <a name="data-flow-performance-features"></a>資料流程效能的功能
  本主題提供有關如何設計 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 封裝以避免常見效能問題的建議。 本主題同時也提供有關您可以用於疑難排解封裝效能之功能與工具的資訊。  
  
## <a name="configuring-the-data-flow"></a>設定資料流程  
 若要設定「資料流程」工作以獲得更好的效能，您可以設定工作的屬性、調整緩衝區大小，以及設定平行執行的封裝。  
  
### <a name="configure-the-properties-of-the-data-flow-task"></a>設定資料流程工作的屬性  
  
> [!NOTE]  
>  您必須針對封裝中的每一個「資料流程」工作，個別設定本節中所討論的屬性。  
  
 您可以設定下列會影響效能的資料流程工作的屬性：  
  
-   指定緩衝區資料的暫時儲存位置 (BufferTempStoragePath 屬性)，以及指定包含二進位大型物件 (BLOB) 資料之資料行的暫時儲存位置 (BLOBTempStoragePath 屬性)。 根據預設，這些屬性包含 TEMP 和 TMP 環境變數的值。 您可能需要指定其他資料夾，以便將暫存檔放在不同或更快的硬碟上，或是將暫存檔分散到多個磁碟機。 您可以使用分號分隔目錄名稱，以指定多個目錄。  
  
-   定義工作所使用之緩衝區的預設大小 (設定 DefaultBufferSize 屬性)，以及定義每個緩衝區中資料列的最大數目 (設定 DefaultBufferMaxRows 屬性)。 設定 AutoAdjustBufferSize 屬性，指出緩衝區的預設大小是否會從 DefaultBufferMaxRows 屬性的值自動計算。 預設緩衝區大小是 10 MB，最大緩衝區大小是 2^31-1 位元組。 預設最大資料列數目是 10,000。  
  
-   設定執行期間工作可以使用的執行緒數目 (設定 EngineThreads 屬性)。 這個屬性為資料流程引擎提供可使用之執行緒數目的建議， 預設值為 10，且最小值為 3。 不過，無論這個屬性的值為何，引擎都不會使用超出它所需的執行緒數目。 如果有需要，引擎也可能會使用超過這個屬性所指定的執行緒數目，以避免發生並行的問題。  
  
-   指示資料流程工作是否以最佳化模式執行 (RunInOptimizedMode 屬性)。 最佳化模式可藉由從資料流程中移除未使用的資料行、輸出和元件，來提升效能。  
  
    > [!NOTE]  
    >  您可以在 RunInOptimizedMode 中的專案層級，設定具有相同名稱的屬性 ( [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] )，以指示資料流程工作在偵錯期間以最佳化模式執行。 這個專案屬性會覆寫資料流程工作在設計階段的 RunInOptimizedMode 屬性。  
  
### <a name="adjust-the-sizing-of-buffers"></a>調整緩衝區大小  
 資料流程引擎是經由計算單一資料列的估計大小，開始設定緩衝區大小的工作， 接著它會將資料列的估計大小乘以 DefaultBufferMaxRows 的值，以獲得初步可行的緩衝區大小值。  
  
-   如果 AutoAdjustBufferSize 設為 true，引擎資料流程引擎會使用導出的值作為緩衝區大小，並且會忽略 DefaultBufferSize 的值。  
  
-   如果 AutoAdjustBufferSize 設為 false，引擎資料流程引擎會使用下列規則來決定緩衝區大小。  
  
    -   如果得到的結果超出 DefaultBufferSize 的值，引擎會減少資料列的數目。  
  
    -   如果得到的結果小於內部計算的最小緩衝區大小，引擎會增加資料列的數目。  
  
    -   如果得到的結果介於最小緩衝區大小和 DefaultBufferSize 的值之間，引擎會盡可能將緩衝區的大小設為接近資料列的估計大小乘以 DefaultBufferMaxRows 的值。  
  
 當您開始測試資料流程工作的效能時，請使用 DefaultBufferSize 和 DefaultBufferMaxRows 的預設值。 啟用資料流程工作的記錄功能，並選取 BufferSizeTuning 事件，以查看每一個緩衝區中包含多少個資料列。  
  
 在開始調整緩衝區大小之前，您可以進行的最重要改善就是移除不需要的資料行，以及適當地設定資料類型，以減少每一個資料列的大小。  
  
 若要判斷緩衝區的最佳數目與大小，請使用 DefaultBufferSize 和 DefaultBufferMaxRows 的值進行測試，同時監視效能及 BufferSizeTuning 事件所報告的資訊。  
  
 請勿增加發生分頁至磁碟之起始點的緩衝區大小。 分頁至磁碟所妨礙的效能超過尚未經過最佳化的緩衝區大小。 若要判斷是否發生分頁，請在 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Management Console (MMC) 的效能嵌入式管理單元中監視 "Buffers spooled" 效能計數器。  
  
### <a name="configure-the-package-for-parallel-execution"></a>設定平行執行的封裝  
 平行執行會改善具有多個實體或邏輯處理器之電腦的效能。 為了在封裝中支援平行執行不同的工作， [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 使用兩種屬性： **MaxConcurrentExecutables** 和 **EngineThreads**。  
  
#### <a name="the-maxconcurrentexcecutables-property"></a>MaxConcurrentExcecutables 屬性  
 **MaxConcurrentExecutables** 屬性是封裝本身的屬性。 此屬性會定義可以同時執行多少工作。 預設值為 -1，表示實體或邏輯處理器的數目加上 2。  
  
 若要了解此屬性的運作方式，請考慮具有三個「資料流程」工作的範例封裝。 如果您將 **MaxConcurrentExecutables** 設定為 3，全部三個「資料流程」工作都可以同時執行。 不過，這是假設每個「資料流程」工作都有 10 的來源到目的地的執行樹狀結構。 將 **MaxConcurrentExecutables** 設定為 3 不能確保每個「資料流程」工作內的執行樹狀結構都可以平行執行。  
  
#### <a name="the-enginethreads-property"></a>EngineThreads 屬性  
 **EngineThreads** 屬性是每個「資料流程」工作的屬性。 此屬性會定義資料流程引擎可以平行建立並執行多少執行緒。 **EngineThreads** 屬性同樣適用於資料流程引擎針對來源所建立的來源執行緒，以及該引擎針對轉換和目的地所建立的工作者執行緒。 因此，將 **EngineThreads** 設定為 10 表示引擎最多可以建立 10 個來源執行緒與 10 個工作者執行緒。  
  
 若要了解此屬性的運作方式，請考慮具有三個「資料流程」工作的範例封裝。 每個「資料流程」工作都包含 10 的來源到目的地的執行樹狀結構。 如果您將「資料流程」工作上的 EngineThreads 設定為 10，全部 30 個執行樹狀結構可能會同時執行。  
  
> [!NOTE]  
>  執行緒的討論超出本主題的範圍。 不過，一般規則不會平行執行超過可用處理器數目的執行緒。 執行超過可用處理器數目的執行緒可能會因為在執行緒之間進行經常性的內容切換而妨礙效能。  
  
## <a name="configuring-individual-data-flow-components"></a>設定個別的資料流程元件  
 若要設定個別的資料流程元件以獲得較好的效能，有一些您可以遵循的一般指導方針。 針對每種資料流程元件，也有特定的指導方針：來源、轉換和目的地。  
  
### <a name="general-guidelines"></a>一般指導方針  
 不管資料流程元件為何，都有兩個您應該遵循的一般指導方針來改善效能：最佳化查詢與避免不必要的字串。  
  
#### <a name="optimize-queries"></a>最佳化查詢  
 某些資料流程元件會在從來源擷取資料時或在查閱作業中使用查詢，以建立參考資料表。 預設查詢會使用 SELECT * FROM \<資料表名稱> 語法。 這種類型的查詢會傳回來源資料表中的所有資料行。 讓所有資料行都在設計階段可用，您便可以選擇任何資料行作為查閱、傳遞或來源資料行。 不過，在選擇要使用的資料行後，您應該將查詢修訂為只包含選取的資料行。 移除多餘的資料行可讓封裝中的資料流程更為有效，因為資料行越少，就會建立越小的資料列。 資料列越小，表示有越多的資料列可以納入同一個緩衝區，而且處理資料集中全部資料列所需的工作也就越少。  
  
 若要建構查詢，您可以輸入查詢或使用「查詢產生器」。  
  
> [!NOTE]  
>  當您在 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]中執行封裝時， [!INCLUDE[ssIS](../../includes/ssis-md.md)] 設計師的 [進度] 索引標籤會列出警告。 這些警告包括識別來源提供給資料流程使用，但是在下游資料流程元件後續作業中未使用的任何資料行。 您可以使用 **RunInOptimizedMode** 屬性自動移除這些資料行。  
  
#### <a name="avoid-unnecessary-sorting"></a>避免不必要的排序  
 排序本質上就是很慢的作業，避免不必要的排序可以改善封裝資料流程的效能。  
  
 有時候來源資料在由下游元件使用前，就已經經過排序。 這種預先排序會在 SELECT 查詢使用 ORDER BY 子句時，或在將資料以排序的順序插入來源時發生。 對於這種預先排序的來源資料，您可以提供資料已排序的提示，因而避免使用「排序」轉換來滿足某些下游轉換的排序需求 (例如，「合併」和「合併聯結」轉換需要已排序的輸入)。若要提供資料已排序的提示，您必須執行下列工作：  
  
-   將上游資料流程元件之輸出的 **IsSorted** 屬性設定為 **True**。  
  
-   指定排序資料所依據的排序索引鍵資料行。  
  
 如需詳細資訊，請參閱 [排序合併和合併聯結轉換的資料](../../integration-services/data-flow/transformations/sort-data-for-the-merge-and-merge-join-transformations.md)。  
  
 如果在資料流程中必須排序資料，您可以將資料流程設計為盡可能少使用排序作業，以改進效能。 例如，資料流程使用「多點傳送」轉換來複製資料集。 在「多點傳送」轉換執行前，對資料集進行一次排序，而不應在轉換後排序多個輸出。  
  
 如需詳細資訊，請參閱＜ [Sort Transformation](../../integration-services/data-flow/transformations/sort-transformation.md)＞、＜ [Merge Transformation](../../integration-services/data-flow/transformations/merge-transformation.md)＞、＜ [Merge Join Transformation](../../integration-services/data-flow/transformations/merge-join-transformation.md)＞和＜ [Multicast Transformation](../../integration-services/data-flow/transformations/multicast-transformation.md)＞。  
  
### <a name="sources"></a>來源  
  
#### <a name="ole-db-source"></a>OLE DB 來源  
 當您使用 OLE DB 來源從檢視表中擷取資料時，選取 [SQL 命令] 當做資料存取模式，然後輸入 SELECT 陳述式。 使用 SELECT 陳述式存取資料的效能比選取 [資料表或檢視表] 當做資料存取模式的效能更好。  
  
### <a name="transformations"></a>轉換  
 使用本節中的建議來改善「彙總」、「模糊查閱」、「模糊群組」、「查閱」、「合併聯結」與「緩時變維度」轉換的效能。  
  
#### <a name="aggregate-transformation"></a>彙總轉換  
 「彙總」轉換包括 **Keys**、 **KeysScale**、 **CountDistinctKeys**和 **CountDistinctScale** 屬性。 這些屬性會提升效能，其方式是讓轉換針對轉換所快取的資料來預先配置所需的記憶體數量。 如果您知道預期要從 **[群組依據]** 作業產生的精確或大約群組數，請分別設定 **Keys** 和 **KeysScale** 屬性。 如果您知道預期要從 **[相異計數]** 作業產生的精確或大約相異數，請分別設定 **CountDistinctKeys** 和 **CountDistinctScale** 屬性。  
  
 如果必須在資料流程中建立多個彙總，您應考慮使用一個「彙總」轉換來建立多個彙總，而不是建立多個轉換。 當一個彙總就是其他彙總的子集時，這個方法能夠改善效能，因為轉換可以最佳化內部儲存體，並且只會掃描一次傳入的資料。 例如，如果彙總使用 GROUP BY 子句和 AVG 彙總，則將它們組合成一個轉換可以改進效能。 不過，在一個「彙總」轉換內執行多個彙總會序列化彙總作業，因此，當多個彙總必須個別計算時，可能不會改善效能。  
  
#### <a name="fuzzy-lookup-and-fuzzy-grouping-transformations"></a>模糊查閱和模糊群組轉換  
 如需有關最佳化「模糊查閱」和「模糊群組」轉換的詳細資訊，請參閱＜ [SQL Server Integration Services 2005 中的模糊查詢和模糊群組](http://go.microsoft.com/fwlink/?LinkId=96604)＞(英文) 白皮書。  
  
#### <a name="lookup-transformation"></a>查閱轉換  
 輸入僅查閱所需資料行的 SELECT 陳述式可以將記憶體中的參考資料大小最小化。 這個選項的效能比選取會傳回大量不必要資料的整個資料表或檢視表更好。  
  
#### <a name="merge-join-transformation"></a>Merge Join Transformation  
 您再也不必設定 **MaxBuffersPerInput** 屬性的值，因為 Microsoft 已做出變更，降低合併聯結轉換會耗用過多記憶體的風險。 這個問題有時候會發生在合併聯結的多個輸入以不平均的速率產生資料時。  
  
#### <a name="slowly-changing-dimension-transformation"></a>緩時變維度轉換  
 「緩時變維度精靈」和「緩時變維度精靈」轉換都是符合多數使用者需求的一般用途工具。 不過，精靈所產生的資料流程不會針對效能進行最佳化。  
  
 「緩時變維度」轉換中最緩慢的元件通常是一次針對一個單一資料列執行 UPDATE 的「OLE DB 命令」轉換。 因此，改善「緩時變維度」轉換效能最有效的方式就是取代「OLE DB 命令」轉換。 您可以將這些轉換取代為將要更新的所有資料列儲存到臨時資料表的目的地元件。 然後，您可以同時加入針對所有資料列執行以單一資料列集為基礎之 Transact-SQL UPDATE 的「執行 SQL」工作。  
  
 進階使用者可以針對緩時變維度處理，設計針對大維度進行最佳化的自訂資料流程。 如需此方式的討論和範例，請參閱＜ [專案 REAL：Business Intelligence ETL 設計練習](http://go.microsoft.com/fwlink/?LinkId=96602)＞(英文) 白皮書中的「唯一的維度狀況」一節。  
  
### <a name="destinations"></a>目的地  
 為達成較佳的目的地效能，請考慮使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 目的地並測試目的地的效能。  
  
#### <a name="sql-server-destination"></a>SQL Server 目的地  
 當封裝將資料載入相同電腦上的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體時，請使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 目的地。 這個目的地最適合高速大量載入。  
  
#### <a name="testing-the-performance-of-destinations"></a>測試目的地的效能  
 您可能會發現將資料儲存至目的地所花費的時間超出預期。 若要識別速度很慢是否是因為目的地無法夠快地處理資料，您可以暫時使用「資料列計數器」轉換來取代目的地。 如果輸送量顯著提高，則很可能是正在載入資料的目的地導致速度變慢。  
  
### <a name="review-the-information-on-the-progress-tab"></a>檢視進度索引標籤上的資訊  
 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 設計師」會提供在 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]。 **[進度]** 索引標籤會以執行順序列出工作和容器，並包含每個工作和容器 (包括封裝本身) 的開始與完成時間、警告及錯誤訊息。 此外，還會以執行順序列出資料流程元件，並包含有關進度 (以完成百分比顯示) 以及已經處理的資料列數目等資訊。  
  
 若要啟用或停用 **[進度]** 索引標籤上的訊息顯示，請在 **[SSIS]** 功能表上切換 **[偵錯進度報表]** 選項。 停用進度報告有助於在 [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)]中執行複雜封裝時改善效能。  
  
## <a name="related-tasks"></a>相關工作  
  
-   [排序合併和合併聯結轉換的資料](../../integration-services/data-flow/transformations/sort-data-for-the-merge-and-merge-join-transformations.md)  
  
## <a name="related-content"></a>相關內容  
 **文件和部落格文章**  
  
-   technet.microsoft.com 上的技術文件： [SQL Server 2005 Integration Services：效能策略](http://go.microsoft.com/fwlink/?LinkId=98899)  
  
-   technet.microsoft.com 上的技術文件： [Integration Services：效能微調技術](http://go.microsoft.com/fwlink/?LinkId=98900)  
  
-   sqlcat.com 上的技術文件： [將同步轉換分割為多個工作來增加管線的輸送量](http://sqlcat.com/technicalnotes/archive/2010/08/18/increasing-throughput-of-pipelines-by-splitting-synchronous-transformations-into-multiple-tasks.aspx)  
  
-   msdn.microsoft.com 上的技術文章： [資料載入效能指南](http://go.microsoft.com/fwlink/?LinkId=220816)。  
  
-   msdn.microsoft.com 上的技術文件： [我們使用 SSIS 在短短 30 分鐘內載入了 1TB 的資料，您也可以](http://go.microsoft.com/fwlink/?LinkId=220817)。  
  
-   sqlcat.com 上的技術文件： [10 大 SQL Server Integration Services 的最佳作法](http://go.microsoft.com/fwlink/?LinkId=220818)。  
  
-   sqlcat.com 上的技術文件及範例： [SSIS 的「平衡型資料散發者」](http://go.microsoft.com/fwlink/?LinkId=220822)。  
  
-   blogs.msdn.com 上的部落格文章： [疑難排解 SSIS 封裝效能問題](http://go.microsoft.com/fwlink/?LinkId=238156)  
  
 **視訊**  
  
-   影片系列， [Designing and Tuning for Performance your SSIS packages in the Enterprise (SQL Video Series)](http://go.microsoft.com/fwlink/?LinkId=400878)(設計及微調企業中 SSIS 封裝的效能 (SQL 影片系列))  
  
-   technet.microsoft.com 上的影片： [Tuning Your SSIS Package Data Flow in the Enterprise (SQL Server Video)](http://technet.microsoft.com/sqlserver/ff686901.aspx)(調整企業中的 SSIS 封裝資料流程 (SQL Server 視訊))  
  
-   technet.microsoft.com 上的影片： [Understanding SSIS Data Flow Buffers (SQL Server Video)](http://technet.microsoft.com/sqlserver/ff686905.aspx)(了解 SSIS 資料流程緩衝區 (SQL Server 視訊))  
  
-   channel9.msdn.com 上的影片： [Microsoft SQL Server Integration Services 效能設計模式](http://go.microsoft.com/fwlink/?LinkID=233698&clcid=0x409)。  
  
-   sqlcat.com 上的簡報： [Microsoft IT 如何運用 SQL Server 2008 SSIS 資料流程引擎增強功能](http://go.microsoft.com/fwlink/?LinkId=217660)。  
  
-   technet.microsoft.com 上的影片： [平衡型資料散發者](http://go.microsoft.com/fwlink/?LinkID=226278&clcid=0x409)  
  
## <a name="see-also"></a>另請參閱  
 [疑難排解封裝開發的工具](../../integration-services/troubleshooting/troubleshooting-tools-for-package-development.md)   
 [套件執行的疑難排解工具](../../integration-services/troubleshooting/troubleshooting-tools-for-package-execution.md)  
  
  
