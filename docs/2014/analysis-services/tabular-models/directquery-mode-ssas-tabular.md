---
title: DirectQuery 模式（SSAS 表格式） |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.bidtoolset.realtime.f1
ms.assetid: 45ad2965-05ec-4fb1-a164-d8060b562ea5
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 9a9c1510030f61896f686b49f4bc134a7dfcb42b
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/26/2020
ms.locfileid: "67284867"
---
# <a name="directquery-mode-ssas-tabular"></a>DirectQuery 模式 (SSAS 表格式)
  Analysis Services 可讓您使用*DirectQuery 模式*直接從關係資料庫系統抓取資料和匯總，從表格式模型中取出資料和建立報表。 此主題介紹僅存在於記憶體中的標準表格式模型和可查詢關聯式資料來源的表格式模型之間的差異，並且說明如何撰寫和部署要在 DirectQuery 模式下使用的模型。  
  
 本主題的章節：  
  
-   [DirectQuery 模式的優點](#bkmk_Benefits)  
  
-   [撰寫要用於 DirectQuery 模式的模型](#bkmk_Design)  
  
    -   [DirectQuery 模型的資料來源](directquery-mode-ssas-tabular.md#bkmk_DataSources)  
  
    -   [DirectQuery 模式的驗證和設計限制](#bkmk_Validation)  
  
    -   [DirectQuery 模型的公式相容性](#bkmk_FormulaCompat)  
  
    -   [DirectQuery 模式的安全性](#bkmk_Security)  
  
    -   [DirectQuery 模式的安全性](#bkmk_Security)  
  
-   [DirectQuery 屬性](#bkmk_PropertyList)  
  
-   [相關主題和工作](#bkmk_related_tasks)  
  
##  <a name="benefits-of-directquery-mode"></a><a name="bkmk_Benefits"></a>DirectQuery 模式的優點  
 根據預設，表格式模型會使用記憶體中快取來儲存和查詢資料。 因為表格式模型使用存在於記憶體中的資料，所以即使是複雜查詢也可以非常快速地執行。 但是，使用快取資料有些缺點：  
  
-   來源資料變更時不會重新整理資料。 您必須處理模型，以便對資料進行更新。  
  
-   在您關閉裝載模型的電腦時，快取將保存到磁碟中，並且在您載入模型或開啟 PowerPivot 檔案時必須重新開啟。 儲存和載入作業可能很耗時。  
  
 反之，DirectQuery 模式使用儲存在 SQL Server 資料庫中的資料。  通常，在您撰寫模型時會將全部資料或少量樣本資料匯入至快取中，並且在您部署模型時指定用於模型查詢的資料來源應該是 SQL Server，而非快取資料。  會將資料的任何 DAX 查詢轉譯為針對指定之關聯式資料來源的對等 SQL 陳述式。  
  
 使用 DirectQuery 模式部署模型有許多優點：  
  
-   以下的資料集可能會有模型：資料集過大而無法納入 Analysis Services 伺服器上的記憶體。  
  
-   資料確保是最新的，並且沒有必須維護另一份資料複本的額外管理負擔。 基礎來源資料的變更可立即反映在對資料模型的查詢中。  
  
-   DirectQuery 可以利用提供者端的查詢加速功能，例如 xVelocity 記憶體最佳化的資料行索引提供的加速功能。  
  
-   後端資料庫強制執行的任何安全性保證會透過資料列層級安全性來強制執行。 反之，如果您使用快取資料，可能很難確保能夠以伺服器上保護資料的相同方式來保護快取的安全。  
  
-   如果模型包含可能需要多個查詢的複雜公式，Analysis Services 可以執行最佳化，以確保對後端資料庫執行之查詢的查詢計畫將盡可能有效率。  
  
##  <a name="authoring-models-for-use-with-directquery-mode"></a><a name="bkmk_Design"></a>撰寫用於 DirectQuery 模式的模型  
 表格式模型是使用模型設計師 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 所撰寫。 模型設計師會在記憶體中建立所有模型，這表示在模型化時，如果資料太大而無法放入記憶體中，您應該只將資料子集匯入至工作空間資料庫使用的快取中。  
  
 在您準備切換至 DirectQuery 模式時，您可以變更啟用 DirectQuery 模式的屬性。 如需詳細資訊，請參閱[啟用 DirectQuery 設計模式 &#40;SSAS 表格式&#41;](enable-directquery-mode-in-ssdt.md)。  
  
 在您執行此作業時，模型設計師會自動將工作空間資料庫設定為以混合模式執行，讓您可以繼續使用快取資料。 模型設計師也會通知您模型中與 DirectQuery 模式不相容的任何功能。 下列清單摘要說明應牢記的主要需求：  
  
-   **資料來源：** DirectQuery 模型只能使用單一 SQL Server 資料來源中的資料。 如果已經為模型啟用 DirectQuery 模式，您將無法在模型設計師中使用任何其他資料類型，包括複製-貼上作業所加入的資料表。 所有其他匯入選項都已停用。 查詢中包含的任何資料表都必須是 SQL Server 資料來源的一部分。 如需詳細資訊，請參閱[DirectQuery 模型的資料來源](directquery-mode-ssas-tabular.md#bkmk_DataSources)。  
  
-   **支援計算結果欄：** DirectQuery 模型不支援計算結果欄。 但是，您可以建立量值和 KPI，以操作資料集。 如需詳細資訊，請參閱[驗證](#bkmk_Validation)一節。  
  
-   **DAX 函數的有限使用：** 某些 DAX 函數不能在 DirectQuery 模式下使用，因此您必須以其他函數取代它們，或使用資料來源中的衍生資料行來建立值。 當您所建立的公式與 DirectQuery 模式不相容時，模型設計師會針對任何引發的錯誤提供設計階段驗證。 如需詳細資訊，請參閱下列各節：[驗證](#bkmk_Validation)。  
  
-   **公式相容性：** 在某些已知情況下，相較于只使用關聯式資料存放區的 DirectQuery 模型，相同的公式可能會在快取或混合式模型中傳回不同的結果。 這些差異是由於 xVelocity 記憶體中分析引擎 (VertiPaq) 和 SQL Server 之間的語意差異所導致。 如需這些差異的詳細資訊，請參閱這一節：[公式相容性](#bkmk_FormulaCompat)。  
  
-   **安全性：** 您可以使用不同的方法來保護模型，視其部署方式而定。 表格式模型的快取資料是使用 Analysis Services 執行個體的安全性模型來確保安全。 您可以使用角色確保 DirectQuery 模型的安全，但是也可以使用關聯式資料存放區中定義的安全性。 您可以設定模型，好讓開啟以僅限 DirectQuery 模型為基礎之報表的使用者只能看到他們在 SQL Server 中的權限下允許看到的資料。 如需詳細資訊，請參閱本節：[安全性](#bkmk_Security)。  
  
-   **用戶端限制：** 當模型處於 DirectQuery 模式時，只能使用 DAX 進行查詢。 不能使用 MDX 來建立查詢。 這表示您不能使用 Excel Pivot Client，因為 Excel 會使用 MDX。  
  
     不過，如果您使用 DAX 資料表查詢當做 XMLA Execute [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]語句的一部分，您可以在中針對 DirectQuery 模型建立查詢。如需詳細資訊，請參閱 [Dax 查詢語法參考] （/dax/dax-syntax-reference
  
 在您解決了所有設計問題並且測試模型之後，就可以進行部署。 此時，您可以設定回應模型查詢的慣用方法。 您希望使用者有存取快取的權限，還是永遠只使用關聯式資料來源？  
  
 如果您在*混合式模式*中部署模型，則快取仍然可供使用，而且可用於查詢。 混合模式為您提供許多選項：  
  
-   在快取和關聯式資料來源都可用時，您可以設定慣用連接方法，但最終還是由用戶端控制所使用的資料來源 (利用 DirectQueryMode 連接字串屬性)。  
  
-   您還可以在快取上設定資料分割，以便永遠不處理用於 DirectQuery 模式的主要資料分割，並且主要資料分割必須永遠參考關聯式資料來源。 有許多方法可以使用資料分割來最佳化模型設計和報表體驗。 如需詳細資訊，請參閱[&#40;SSAS 表格式&#41;的資料分割和 DirectQuery 模式](define-partitions-in-directquery-models-ssas-tabular.md)。  
  
-   部署模型之後，您可以變更慣用連接方法。 例如，您可以使用混合模式來進行測試，並且只在全面測試了使用該模型的所有報表或查詢後，才將模型切換到 **[僅限 DirectQuery]** 模式。 如需詳細資訊，請參閱 [設定或變更 DirectQuery 的慣用連接方法](../set-or-change-the-preferred-connection-method-for-directquery.md)。  
  
###  <a name="data-sources-for-directquery-models"></a><a name="bkmk_DataSources"></a>DirectQuery 模型的資料來源  
 當您將設計環境變更為啟用 DirectQuery 模式之後，系統會立即對工作空間資料庫的資料來源進行驗證，以確保它們來自單一 SQL Server 資料來源。 DirectQuery 模型中不允許來自其他資料來源的資料，包括複製-貼上的資料。  
  
 如果您想要在 DirectQuery 模式下使用模型，則必須確保報表所需的所有資料都儲存在指定的 SQL Server 資料庫中。 如果該來源中未提供模型化所需的資料，請考慮使用 Integration Services 或其他資料倉儲工具，將資料匯入至做為 DirectQuery 資料來源的 SQL Server 資料庫中。  
  
###  <a name="validation-and-design-restrictions-for-directquery-mode"></a><a name="bkmk_Validation"></a>DirectQuery 模式的驗證和設計限制  
 當您撰寫要在 DirectQuery 模式下使用的模型時，最初必須將某些部分的資料載入快取中。 如果您最終使用的資料太大而無法放入記憶體中，您可以使用 [資料表匯入嚮導] 中的 [**預覽 & 篩選**] 選項來選取資料的子集，或撰寫 SQL 腳本來取得您想要的資料。  
  
> [!WARNING]  
>  因為 DirectQuery 模式不支援使用導出資料行，所以如果您有想要合併或執行其他作業的資料行，則應該預先規劃，並在資料匯入查詢或指令碼中建立資料行定義。  
  
 若要檢視和解決驗證錯誤，請在 **中開啟** [錯誤清單] [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)]。 導致無法使用 DirectQuery 模式的嚴重錯誤會顯示在 [**錯誤**] 索引標籤上。您必須先修正這些錯誤，然後再變更為 DirectQuery 模式。 比較難解決的驗證錯誤通常與 DirectQuery 模式不支援的公式相關。 如需公式和計算結果欄相關錯誤的總覽，請參閱[公式相容性](#bkmk_FormulaCompat)一節。  
  
 下列清單描述在撰寫要用於 DirectQuery 存取的模型時應注意的其他考量事項：  
  
-   即使處於 *「僅限 DirectQuery」* 模式，報表中的結果也會根據正在檢視結果的使用者的安全性內容而改變。 您應該以不同的認證對模型進行測試，以確保使用者得到預期結果。  
  
-   如果您將模型設定為以混合模式操作，允許使用快取或來自 SQL Server 的資料，則應該了解連接到每一個資料來源的用戶端可能會看到不同結果 (根據連接字串中指定的模式而定)。 如果您需要確保報表使用者只看到來自 SQL Server 的資料，則必須清除快取或將模型變更為 DirectQueryOnly。  
  
###  <a name="formula-compatibility-for-directquery-models"></a><a name="bkmk_FormulaCompat"></a>DirectQuery 模型的公式相容性  
 某些模型可能包含 DirectQuery 模式所不支援的公式，因此必須對模型進行重新設計，以防止驗證錯誤。 DirectQuery 模式所支援之公式的限制包含下列：  
  
-   任何表格式模型在啟用 DirectQuery 模式後都不支援導出資料行，甚至是混合模型也不支援。 如果模型需要導出資料行，請考慮在匯入定義中使用 Transact-SQL，將這些導出資料行轉換為衍生的資料行。  
  
-   DirectQuery 模型支援在量值中使用 DAX 公式，量值會轉換為針對關聯式資料存放區、以集合為基礎的運算。 支援透過使用隱含量值建立的所有量值。  
  
-   並非所有函數都受支援。 因為在查詢 DirectQuery 模型時 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 會將所有 DAX 公式和量值定義都轉換為 SQL 陳述式，所以包含無法轉換為 Transact-SQL 之元素的任何公式都會觸發模型驗證錯誤。 例如，不支援時間智慧函數。 即使支援的函數可能會有不同的行為，例如統計函數。 如需相容性問題的完整清單，請參閱[DirectQuery 模式中的公式相容性](../dax-formula-compatibility-in-directquery-mode-ssas-2014.md)。  
  
-   在您將模型切換至 DirectQuery 模式時，模型中的公式可能會通過驗證，但在對快取和關聯式資料存放區執行時，則會傳回不同的結果。 這是因為對快取的計算使用 xVelocity 記憶體中分析引擎 (VertiPaq) 的語意，其中包含用於模擬 Excel 行為的許多功能，而針對儲存在關聯式資料存放區之資料的查詢則需要使用 SQL Server 的語意。 如需在模型部署為即時時可能會傳回不同結果的 DAX 函數清單，請參閱[DirectQuery 模式中的公式相容性](../dax-formula-compatibility-in-directquery-mode-ssas-2014.md)。  
  
###  <a name="connecting-to-directquery-models"></a><a name="bkmk_Connecting"></a>連接到 DirectQuery 模型  
 使用 MDX 當做查詢語言的用戶端不能連接到使用 DirectQuery 模式的模型。 例如，如果您嘗試針對 DirectQuery 模型建立 MDX 查詢，則會出現錯誤，表示找不到或尚未處理 Cube。 您可以使用 [!INCLUDE[ssCrescent](../../includes/sscrescent-md.md)]、DAX 公式或 XMLA 查詢來針對 DirectQuery 模型建立查詢。 如需如何針對表格式模型執行特定查詢的詳細資訊，請參閱[表格式模型資料存取](tabular-model-data-access.md)。  
  
 如果您正在使用混合模型，可以藉由指定連接字串屬性 DirectQueryMode 來指定使用者是連接到快取還是使用 DirectQuery 資料。  
  
###  <a name="security-in-directquery-mode"></a><a name="bkmk_Security"></a>DirectQuery 模式中的安全性  
 在模型撰寫過程中，您會指定用於擷取來源資料的權限。 通常這是您自己的認證或是用於開發的帳戶。 但是，在模型切換為使用 DirectQuery 模式時，安全性內容更為複雜：  
  
-   考慮使用者是否具有存取關聯式資料存放區資料的必要層級。  
  
-   根據使用者的安全性內容，查看相同模型或報表的使用者可能會看到不同的資料。  
  
-   如果已保留模型快取，則會使用 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 安全性模型 (角色) 來保護快取的安全。 快取可能包含模型設計師有權看到、但使用者無權看到的資料。 模型和報表設計師應該清除快取，或透過角色控制存取權限來保護這些資料。  
  
-   連接到資料來源時，回應來自快取之查詢的模型不能模擬目前的使用者。 如果要在連接到資料來源時模擬目前的使用者，您必須使用 DirectQuery 模式。  
  
-   如果您的報表模型需要安全性，您有兩個選擇：使用 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 角色，或者對資料來源設定資料列層級權限。 關聯式資料來源中的安全性是用於控制對資料表的存取權限，並且不支援資料行層級安全性。 因此，如果某個區域中的使用者無權檢視來自不同區域的銷售數字，則包含根據 Sales 資料表之量值的報表將傳回空白或錯誤。  
  
 模擬設定屬性會指定當您使用 DirectQuery 連接到模型時所使用的認證，這適用於僅限 DirectQuery 模型或是使用 DirectQuery 回應查詢的混合模型。 此屬性有下列值：  
  
 **預設**  
 使用匯入精靈中指定的認證來連接到資料來源。 這可以是特定的 Windows 使用者或服務帳戶。  
  
 `ImpersonateCurrentUser`  
 使用目前使用者的認證來連接到資料來源。  
  
 如需如何設定這些屬性的詳細資訊，請參閱[DirectQuery 部署案例 &#40;SSAS 表格式&#41;](../directquery-deployment-scenarios-ssas-tabular.md)。  
  
##  <a name="directquery-properties"></a><a name="bkmk_PropertyList"></a>DirectQuery 屬性  
 下表列出可以在 [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)] 和 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 中設定的一些屬性，以便啟用 DirectQuery 及控制模型查詢所用的資料來源。  
  
|屬性名稱|描述|  
|-------------------|-----------------|  
|**DirectQueryMode 屬性**|此屬性會在模型設計師中啟用 DirectQuery 模式。 您必須將此屬性設定為 `On`，才能變更任何其他 DirectQuery 屬性。<br /><br /> 如需詳細資訊，請參閱[啟用 DirectQuery 設計模式 &#40;SSAS 表格式&#41;](enable-directquery-mode-in-ssdt.md)。|  
|**QueryMode 屬性**|此屬性指定 DirectQuery 模型的預設查詢方法。當您部署模型時，在模型設計師中設定此屬性，但稍後可以覆寫該屬性。 此屬性有下列值：<br /><br /> **DirectQuery** ：此設定會指定模型的所有查詢都應該只使用關聯式資料來源。<br /><br /> **搭配使用 DirectQuery 和 InMemory** ：根據預設，此設定會指定應該透過關聯式來源來回應查詢，除非在用戶端的連接字串中指定其他項目。<br /><br /> **InMemory** ：此設定會指定僅透過快取來回應查詢。<br /><br /> **搭配使用 InMemory 和 DirectQuery** ：根據預設，此設定會指定 應該透過快取來回應查詢，除非在用戶端的連接字串中指定其他項目。<br /><br /> <br /><br /> 如需詳細資訊，請參閱 [設定或變更 DirectQuery 的慣用連接方法](../set-or-change-the-preferred-connection-method-for-directquery.md)。|  
|**DirectQueryMode 屬性**|在部署模型之後，您可以透過在 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 中變更此屬性，變更 DirectQuery 模型的慣用查詢資料來源。<br /><br /> 與上一個屬性相似，此屬性指定模型的預設資料來源，而且有下列值：<br /><br /> **InMemory**：查詢只能使用快取。<br /><br /> **DirectQuerywithInMemory**：根據預設，查詢會使用關聯式資料來源，除非在用戶端的連接字串中指定另一個。<br /><br /> **InMemorywithDirectQuery**：查詢預設會使用快取，除非在用戶端的連接字串中指定另一個。<br /><br /> （**DirectQuery**：查詢只使用關聯式資料來源。<br /><br /> <br /><br /> 如需詳細資訊，請參閱 [設定或變更 DirectQuery 的慣用連接方法](../set-or-change-the-preferred-connection-method-for-directquery.md)。|  
|**模擬設定屬性**|此屬性定義在查詢時連接至 SQL Server 資料來源所用的認證。 您可以在模型設計師中設定此屬性，並且可以稍後在部署模型後變更值。<br /><br /> 請注意，這些認證只用於回應對關聯式資料存放區的查詢；它們不同於處理混合模型快取所用的認證。<br /><br /> 當模型只用於記憶體中時，不能使用模擬。 `ImpersonateCurrentUser` 設定無效，除非模型正在使用 DirectQuery 模式。|  
  
 此外，如果您的模型包含資料分割，您必須選擇一個資料分割做為 DirectQuery 模式查詢的來源。 如需詳細資訊，請參閱[&#40;SSAS 表格式&#41;的資料分割和 DirectQuery 模式](define-partitions-in-directquery-models-ssas-tabular.md)。  
  
##  <a name="related-topics-and-tasks"></a><a name="bkmk_related_tasks"></a>相關主題和工作  
  
|主題|描述|  
|-----------|-----------------|  
|[資料分割和 DirectQuery 模式 &#40;SSAS 表格式&#41;](define-partitions-in-directquery-models-ssas-tabular.md)|描述如何在設定 DirectQuery 模式的模型中使用資料分割。|  
|[DirectQuery 模式中的 DAX 公式相容性](../dax-formula-compatibility-in-directquery-mode-ssas-2014.md)|描述可在設定 DirectQuery 模式的模型中使用之公式的限制和相容性需求。|  
|[&#40;SSAS 表格式&#41;啟用 DirectQuery 設計模式](enable-directquery-mode-in-ssdt.md)|描述如何變更設計階段環境，好讓它支援使用 DirectQuery 模式。|  
|[變更 DirectQuery 資料分割 &#40;SSAS 表格式&#41;](../change-the-directquery-partition-ssas-tabular.md)|描述如何變更 DirectQuery 資料分割。|  
|[設定或變更 DirectQuery 的慣用連接方法](../set-or-change-the-preferred-connection-method-for-directquery.md)|描述如何針對設定 DirectQuery 的模型來設定或變更連接方法。|  
|[&#40;SSAS 表格式&#41;的 DirectQuery 部署案例](../directquery-deployment-scenarios-ssas-tabular.md)|描述 DirectQuery 部署案例。|  
|[為表格式模型資料庫設定 In-Memory 或 DirectQuery 存取](enable-directquery-mode-in-ssms.md)|了解 DirectQuery 組態|  
|[清除 Analysis Services 快取](../instances/clear-the-analysis-services-caches.md)|清除表格式模型的快取|  
  
## <a name="see-also"></a>另請參閱  
 [SSAS 表格式 &#40;的資料分割&#41;](partitions-ssas-tabular.md)   
 [&#40;SSAS 表格式&#41;的表格式模型專案](tabular-model-projects-ssas-tabular.md)   
 [在 Excel 中進行分析 &#40;SSAS 表格式&#41;](analyze-in-excel-ssas-tabular.md)  
