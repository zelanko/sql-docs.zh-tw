---
title: "查閱轉換 |Microsoft 文件"
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
- sql13.dts.designer.lookuptrans.f1
- sql13.dts.designer.lookuptransformation.general.f1
- sql13.dts.designer.lookuptransformation.referencetable.f1
- sql13.dts.designer.lookuptransformation.columns.f1
- sql13.dts.designer.lookuptransformation.advanced.f1
helpviewer_keywords:
- Lookup transformation
- joining columns [Integration Services]
- cache [Integration Services]
- match exactly [Integration Services]
- lookups [Integration Services]
- exact matches [Integration Services]
ms.assetid: de1cc8de-e7af-4727-b5a5-a1f0a739aa09
caps.latest.revision: 106
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 4b557efa62075f7b88e6b70cf5950546444b95d8
ms.openlocfilehash: ee0c7e667e933c98bdbc228244a9dea1cf2c9bdd
ms.contentlocale: zh-tw
ms.lasthandoff: 09/28/2017

---
# <a name="lookup-transformation"></a>查閱轉換
  「查閱」轉換會藉由聯結輸入資料行中的資料與參考資料集中的資料行來執行查閱。 您可以使用查閱在相關資料表中存取以通用資料行中的值為基礎的其他資訊。  
  
 參考資料集可以是快取檔案、現有的資料表或檢視、新資料表或 SQL 查詢的結果。 「查閱」轉換會使用 OLE DB 連接管理員或快取連接管理員來連接到參考資料集。 如需詳細資訊，請參閱 [OLE DB 連線管理員](../../../integration-services/connection-manager/ole-db-connection-manager.md) 和 [快取連線管理員](../../../integration-services/data-flow/transformations/cache-connection-manager.md)  
  
 您可以利用下列方式設定「查閱」轉換：  
  
-   選取您要使用的連接管理員。 如果想要連接到資料庫，請選取 OLE DB 連接管理員。 如果想要連接到快取檔案，請選取快取連接管理員。  
  
-   指定包含參考資料集的資料表或檢視。  
  
-   藉由指定 SQL 陳述式產生參考資料集。  
  
-   指定輸入與參考資料集之間的聯結。  
  
-   從參考資料集將資料行加入至「查閱」轉換輸出。  
  
-   設定快取選項。  
  
 「查閱」轉換支援下列 OLE DB 連接管理員的資料提供者：  
  
-   [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]  
  
-   Oracle  
  
-   DB2  
  
 「查閱」轉換會嘗試在轉換輸入的值與參考資料集的值之間執行等聯結 (Equi-Join)  (等聯結表示轉換輸入中的各資料列，必須至少符合參考資料集中的某個資料列)。如果無法執行等聯結，則「查閱」轉換會執行下列其中一項動作：  
  
-   如果參考資料集中沒有相符的項目，則不會發生聯結。 根據預設，「查閱」轉換會將沒有相符項目的資料列視為錯誤； 不過，您可以設定「查閱」轉換，以將這些資料列重新導向至無相符結果輸出。  
  
-   如果參考資料表中有多個相符項目，「查閱」轉換將只傳回查閱查詢所傳回的第一個相符項目。 如果找到多個相符項目，則「查閱」轉換只會在已設定為將所有參考資料集載入至快取時才產生錯誤或警告。 在這種情況下，「查閱」轉換會在轉換填滿快取時偵測到多個相符項目時產生警告。  
  
 聯結可以是複合聯結，表示您可以將轉換輸入中的多個資料行聯結至參考資料集中的資料行。 轉換支援聯結任何資料類型的資料行，但 DT_R4、DT_R8、DT_TEXT、DT_NTEXT 或 DT_IMAG 除外。 如需詳細資訊，請參閱＜ [Integration Services Data Types](../../../integration-services/data-flow/integration-services-data-types.md)＞。  
  
 通常參考資料集的值會加入至轉換輸出。 例如，「查閱」轉換可從使用輸出資料行之值的資料表擷取產品名稱，然後將產品名稱加入至轉換輸出。 參考資料表的值可取代資料行的值，或者可加入至新的資料行。  
  
 「查閱」轉換執行的查閱區分大小寫。 若要避免由於資料中的大小寫不同而造成查閱失敗，請先使用「字元對應」轉換將資料轉換成大寫或小寫， 然後在產生參考資料表的 SQL 陳述式中包含 UPPER 或 LOWER 函數。 如需詳細資訊，請參閱[字元對應轉換](../../../integration-services/data-flow/transformations/character-map-transformation.md)、[UPPER &#40;Transact-SQL&#41;](../../../t-sql/functions/upper-transact-sql.md) 和 [LOWER &#40;Transact-SQL&#41;](../../../t-sql/functions/lower-transact-sql.md)。  
  
 「查閱」轉換具有下列的輸入和輸出：  
  
-   輸入。  
  
-   相符結果輸出。 相符結果輸出會處理轉換輸入中，至少符合參考資料集中一個項目的資料列。  
  
-   無相符結果輸出。 無相符結果輸出會處理輸入中沒有至少符合參考資料集中一個項目的資料列。 如果將「查閱」轉換設定為把沒有相符項目的資料列視為錯誤，則這些資料列會重新導向至錯誤輸出； 否則，轉換會將這些資料列重新導向至無相符結果輸出。  
  
-   錯誤輸出。  
  
## <a name="caching-the-reference-dataset"></a>快取參考資料集  
 記憶體中的快取會儲存參考資料集，並儲存編列資料索引的雜湊資料表。 在完成封裝的執行之前，快取都會保留在記憶體中。 您可以將快取保存至快取檔案 (.caw)。  
  
 將快取保存至檔案後，系統就可以更快地載入快取。 如此可改善「查閱」轉換和封裝的效能。 請記住，當您使用快取檔案時，所使用的資料並不如資料庫中的資料新。  
  
 下列是將快取保存至檔案的其他優點：  
  
-   ***在多個封裝間共用快取檔案。如需詳細資訊，請參閱***  [使用快取連線管理員以完整快取模式實作查閱轉換](../../../integration-services/data-flow/transformations/lookup-transformation-full-cache-mode-cache-connection-manager.md)  ***。***  
  
-   使用封裝部署快取檔案， ***接著就可以在多部電腦上使用資料。*** 如需詳細資訊，請參閱 [針對查閱轉換來建立及部署快取](../../../integration-services/data-flow/transformations/create-and-deploy-a-cache-for-the-lookup-transformation.md)。  
  
-   使用「原始檔案」來源從快取檔案讀取資料， 接著就可以使用其他的資料流程元件來轉換或移動資料。 如需相關資訊，請參閱 [Raw File Source](../../../integration-services/data-flow/raw-file-source.md)。  
  
    > [!NOTE]  
    >  快取連接管理員不支援使用「原始檔案」目的地所建立或修改的快取檔案。  
  
-   使用「檔案系統」工作在快取檔案上執行作業和設定屬性。 如需詳細資訊，請參閱 [檔案系統工作](../../../integration-services/control-flow/file-system-task.md)。  
  
 下列是快取選項：  
  
-   參考資料集是藉由執行「查閱」轉換之前使用資料表、檢視或 SQL 查詢而產生並載入快取。 您可以使用 OLE DB 連接管理員來存取資料集。  
  
     此快取選項與 [!INCLUDE[ssISversion2005](../../../includes/ssisversion2005-md.md)]中用於「查閱」轉換的完整快取選項相容。  
  
-   參考資料集是從資料流程中已連接的資料來源或從快取檔案產生，然後在「查閱」轉換執行之前載入至快取。 您可以使用快取連接管理員或是快取轉換來存取資料集。 如需詳細資訊，請參閱 [快取連線管理員](../../../integration-services/data-flow/transformations/cache-connection-manager.md) 和 [快取轉換](../../../integration-services/data-flow/transformations/cache-transform.md)。  
  
-   參考資料集是藉由在執行「查閱」轉換期間使用資料表、檢視或 SQL 查詢而產生。 在參考資料集中具有相符項目的資料列，以及在資料集中沒有相符項目的資料列，都可以載入至快取。  
  
     超過快取的記憶體大小時，查閱轉換會自動從快取中移除最不常用的資料列。  
  
     此快取選項與 [!INCLUDE[ssISversion2005](../../../includes/ssisversion2005-md.md)]中用於「查閱」轉換的部分快取選項相容。  
  
-   參考資料集是藉由在執行「查閱」轉換期間使用資料表、檢視或 SQL 查詢而產生。 不會將任何資料存入快取。  
  
     此快取選項與 [!INCLUDE[ssISversion2005](../../../includes/ssisversion2005-md.md)]中用於「查閱」轉換的無快取選項相容。  
  
 [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] 和 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 的差異在於比較字串的方式。 如果「查閱」轉換是設定為在執行之前將參考資料集載入至快取，則 [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] 會在快取中進行查閱比較。 否則，查閱作業會使用參數化的 SQL 陳述式而由 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 進行查閱比較。 這表示「查閱」轉換可能會根據快取類型，從相同的查閱資料表傳回不同數目的相符項目。  
  
## <a name="related-tasks"></a>相關工作  
 您可以透過「 [!INCLUDE[ssIS](../../../includes/ssis-md.md)] 設計師」或以程式設計方式設定屬性。 如需進一步詳細資訊，請參閱下列主題。  
  
-   [以沒有快取或部分快取模式實作查閱](../../../integration-services/data-flow/transformations/implement-a-lookup-in-no-cache-or-partial-cache-mode.md)  
  
-   [使用快取連線管理員以完整快取模式來實作查閱轉換](../../../integration-services/data-flow/transformations/lookup-transformation-full-cache-mode-cache-connection-manager.md)  
  
-   [使用 OLE DB 連接管理員，以完整快取模式來實作查閱轉換](../../../integration-services/data-flow/transformations/lookup-transformation-full-cache-mode-ole-db-connection-manager.md)  
  
-   [設定資料流程元件的屬性](../../../integration-services/data-flow/set-the-properties-of-a-data-flow-component.md)  
  
## <a name="related-content"></a>相關內容  
  
-   位於 msdn.microsoft.com 的影片： [如何：在完整快取模式中實作查閱轉換 (SQL Server 影片)](http://go.microsoft.com/fwlink/?LinkId=131031)  
  
-   位於 blogs.msdn.com 的部落格項目： [Best Practices for Using the Lookup Transformation Cache Modes](http://go.microsoft.com/fwlink/?LinkId=146623)(使用查閱轉換快取模式的最佳做法)  
  
-   位於 blogs.msdn.com 的部落格項目： [Lookup Pattern: Case Insensitive](http://go.microsoft.com/fwlink/?LinkId=157782)(查閱模式：不區分案例)  
  
-   位於 msftisprodsamples.codeplex.com 上的範例： [Lookup Transformation](http://go.microsoft.com/fwlink/?LinkId=267528)(查閱轉換)。  
  
     如需安裝 [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] 產品範例和範例資料庫的資訊，請參閱 [SQL Server Integration Services Product Samples](http://go.microsoft.com/fwlink/?LinkId=267527)(SQL Server Integration Services 產品範例)。  
  
## <a name="lookup-transformation-editor-general-page"></a>查閱轉換編輯器 (一般頁面)
  使用 [查閱轉換編輯器] 對話方塊的 **[一般]** 頁面來選取快取模式、選取連接類型，及指定如何處理無相符項目的資料列。  
  
### <a name="options"></a>選項。  
 **完整快取**  
 在查閱轉換執行之前產生參考資料集並將其載入快取。  
  
 **部分快取**  
 在查閱轉換執行期間產生參考資料集。 將參考資料集中具有相符項目的資料列，以及在資料集中沒有相符項目的資料列載入到快取。  
  
 **沒有快取**  
 在查閱轉換執行期間產生參考資料集。 沒有資料會載入到快取。  
  
 **快取連接管理員**  
 將查閱轉換設定為使用快取連接管理員。 只有在選取 [完整快取] 選項時，才能使用這個選項。  
  
 **OLE DB 連接管理員**  
 將查閱轉換設定為使用 OLE DB 連接管理員。  
  
 **指定如何處理無相符項目的資料列**  
 選取選項以處理沒有至少符合參考資料集中一個項目的資料列。  
  
 當您選取 **[將資料列重新導向無相符結果輸出]**時，資料列會重新導向無相符結果輸出，且不當做錯誤處理。 無法使用 **[查閱轉換編輯器]** 對話方塊的 **[錯誤輸出]** 頁面上的 **[錯誤]** 選項。  
  
 從 **[指定如何處理無相符項目的資料列]** 清單方塊中選取任何其他選項時，會將資料列當做錯誤處理。 可以使用 **[錯誤輸出]** 頁面上的 **[錯誤]** 選項。  
  
### <a name="external-resources"></a>外部資源  
 blogs.msdn.com 上的部落格文章： [查閱快取模式](http://go.microsoft.com/fwlink/?LinkId=219518)   
  
## <a name="lookup-transformation-editor-connection-page"></a>查閱轉換編輯器 (連接頁面)
  使用 **[查閱轉換編輯器]** 對話方塊的 **[連接]** 頁面，來選取連接管理員。 如果您選取 OLE DB 連接管理員，也可以選取查詢、資料表或檢視來產生參考資料集。  
  
### <a name="options"></a>選項。  
 當您在 **[查閱轉換編輯器]** 對話方塊的 [一般] 頁面上選取 **[完整快取]** 和 **[快取連接管理員]** 時，可使用下列選項：  
  
 **[完整快取]**  
 從清單中選取現有的快取連線管理員，或按一下 [新增] 來建立新的連線。  
  
 **新增**  
 使用 [快取連線管理員編輯器] 對話方塊來建立新的連線。  
  
 當您在 **[查閱轉換編輯器]**對話方塊的 [一般] 頁面上選取 **[完整快取]**、 **[部分快取]**或 **[無快取]**以及 **[OLE DB 連接管理員]** 時，可以使用下列選項。  
  
 **[無快取]**  
 從清單中選取現有的 OLE DB 連線管理員，或按一下 [新增] 來建立新連線。  
  
 **新增**  
 使用 [設定 OLE DB 連線管理員] 對話方塊來建立新的連線。  
  
 **使用資料表或檢視**  
 從清單中選取現有的資料表或檢視，或按一下 [新增] 來建立新的資料表。  
  
> [!NOTE]  
>  如果在 **[查閱轉換編輯器]** 的 **[進階]**頁面上指定 SQL 陳述式，則該 SQL 陳述式會覆寫並取代此處所選取的資料表名稱。 如需詳細資訊，請參閱 [查閱轉換編輯器 &#40;進階頁面&#41;](../../../integration-services/data-flow/transformations/lookup-transformation-editor-advanced-page.md)＞。  
  
 **新增**  
 使用 [建立資料表] 對話方塊建立新的資料表。  
  
 **使用 SQL 查詢的結果**  
 選擇此選項以瀏覽至預先存在的查詢、建立新查詢、檢查查詢語法，以及預覽查詢結果。  
  
 **建立查詢**  
 使用 [查詢產生器] (用來以瀏覽資料的方式建立查詢的圖形化工具)，來建立要執行的 Transact-SQL 陳述式。  
  
 **瀏覽**  
 使用此選項即可瀏覽至預先存在且已儲存為檔案的查詢。  
  
 **剖析查詢**  
 檢查查詢的語法。  
  
 **預覽**  
 使用 [預覽查詢結果] 對話方塊來預覽結果。 此選項最多可顯示 200 個資料列。  
  
### <a name="external-resources"></a>外部資源  
 blogs.msdn.com 上的部落格文章： [查閱快取模式](http://go.microsoft.com/fwlink/?LinkId=219518)   
  
## <a name="lookup-transformation-editor-columns-page"></a>查閱轉換編輯器 (資料行頁面)
  使用 **[查閱轉換編輯器]** 對話方塊的 **[資料行]** 頁面，即可指定來源資料表和參考資料表之間的聯結，以及從參考資料表中選取查閱資料行。  
  
### <a name="options"></a>選項。  
 **可用的輸入資料行**  
 檢視可用的輸入資料行清單。 輸入資料行是連接來源的資料流程中的資料行。 輸入資料行和查閱資料行必須有相符的資料類型。  
  
 使用拖放作業，即可將可用的輸入資料行對應到查閱資料行。  
  
 您也可以藉由在 **[可用的輸入資料行]** 資料表中反白顯示資料行，按下應用程式鍵，然後按一下 **[編輯對應]**，使用鍵盤將輸入資料行對應到查閱資料行。  
  
 **可用的查閱資料行**  
 檢視查閱資料行清單。 查閱資料行是參考資料表中的資料行，您可在其中查閱符合輸入資料行的值。  
  
 使用拖放作業，即可將可用的查閱資料行對應到輸入資料行。  
  
 使用核取方塊即可在參考資料表中，選取要執行查閱作業的查閱資料行。  
  
 您也可以藉由在 **[可用的查閱資料行]** 資料表中反白顯示資料行，按下應用程式鍵，然後按一下 **[編輯對應]**，使用鍵盤將查閱資料行對應到輸入資料行。  
  
 **查閱資料行**  
 檢視選取的查閱資料行。 您的選擇會反映在 **[可用的查閱資料行]** 資料表的核取方塊選擇中。  
  
 **查閱作業**  
 從清單中選取要在查閱資料行上執行的查閱作業。  
  
 **輸出別名**  
 輸入每個查閱資料行之輸出的別名。 預設是查閱資料行的名稱；但是，您可以選取任何唯一的描述性名稱。  
  
## <a name="lookup-transformation-editor-advanced-page"></a>查閱轉換編輯器 (進階頁面)
  使用 [查閱轉換編輯器] 對話方塊的 [進階] 頁面，即可設定部分快取並修改查閱轉換的 SQL 陳述式。  
  
### <a name="options"></a>選項。  
 **快取大小 (32 位元)**  
 調整 32 位元電腦的快取大小 (以 MB 為單位)。 預設值是 5 MB。  
  
 **快取大小 (64 位元)**  
 調整 64 位元電腦的快取大小 (以 MB 為單位)。 預設值是 5 MB。  
  
 **針對無相符項目的資料列啟用快取**  
 將參考資料集中沒有相符項目的資料列存入快取。  
  
 **來自快取的配置**  
 指定針對在資料集中沒有相符項目的資料列所配置的快取百分比。  
  
 **修改 SQL 陳述式**  
 修改用來產生參考資料集的 SQL 陳述式。  
  
> [!NOTE]  
>  在此頁面上所指定的選擇性 SQL 陳述式會覆寫並取代在 [查閱轉換編輯器] 的 [連接] 頁面上所指定的資料表名稱。 如需詳細資訊，請參閱 [查閱轉換編輯器 &#40;連接頁面&#41;](../../../integration-services/data-flow/transformations/lookup-transformation-editor-connection-page.md)＞。  
  
 **設定參數**  
 使用 [設定查詢參數] 對話方塊，即可將輸入資料行對應至參數。  
  
### <a name="external-resources"></a>外部資源  
 blogs.msdn.com 上的部落格文章： [查閱快取模式](http://go.microsoft.com/fwlink/?LinkId=219518)   
  
## <a name="see-also"></a>另請參閱  
 [模糊查閱轉換](../../../integration-services/data-flow/transformations/fuzzy-lookup-transformation.md)   
 [詞彙查閱轉換](../../../integration-services/data-flow/transformations/term-lookup-transformation.md)   
 [資料流程](../../../integration-services/data-flow/data-flow.md)   
 [Integration Services 轉換](../../../integration-services/data-flow/transformations/integration-services-transformations.md)  
  
  
