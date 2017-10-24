---
title: "清除 Analysis Services 快取 |Microsoft 文件"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- analysis-services/multidimensional-tabular
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 6bf66fdd-6a03-4cea-b7e2-eb676ff276ff
caps.latest.revision: 11
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 67ea43179411006e5e549c44b13d4a3fa1d6074f
ms.contentlocale: zh-tw
ms.lasthandoff: 09/01/2017

---
# <a name="clear-the-analysis-services-caches"></a>清除 Analysis Services 快取
  Analysis Services 會快取資料以提高查詢效能。 此主題提供有關如何使用 XMLA ClearCache 命令，清除回應 MDX 查詢時所建立之快取的建議。 根據您使用的是表格式或多維度模型，執行 ClearCache 的影響有所不同。  
  
 **何時清除多維度模型的快取**  
  
 對於多維度資料庫，Analysis Services 會在評估計算時，於公式引擎和儲存引擎中建立維度查詢和量值群組查詢結果的快取。 當公式引擎需要資料格座標或 Subcube 的量值資料時，就會發生量值群組查詢。 查詢非自然階層以及套用自動存在時，就會發生維度查詢。  
  
 建議在進行效能測試時清除快取。 藉由清除測試回合之間的快取，可確保快取不會將測量查詢設計變更影響的任何測試結果扭曲。  
  
 **何時清除表格式模型的快取**  
  
 表格式模型通常儲存在記憶體中，而在執行查詢時執行彙總和其他計算。 因此，ClearCache 命令對表格式模型影響有限。 對於表格式模型，如果對它執行 MDX 查詢，資料可加入至 Analysis Services 快取。 具體來說，MDX 和自動存在作業所參考的 DAX 量值會將結果分別快取在公式快取和維度快取中。 但請注意，非自然階層和量值群組查詢不會將結果快取在儲存引擎中。 此外，務必了解 DAX 查詢不會將結果快取在公式和儲存引擎中。 另一方面來說，MDX 查詢會產生快取，而對表格式模型執行 ClearCache 會導致系統的任何快取資料無效。  
  
 執行 ClearCache 也會清除 xVelocity 記憶體中分析引擎 (VertiPaq) 中的記憶體中快取。 xVelocity 引擎維護小型的快取結果集。 執行 ClearCache 會導致 xVelocity 引擎中的這些快取無效。  
  
 最後，在表格式模型重新設定為 **DirectQuery** 模式時，執行 ClearCache 也會移除記憶體中的剩餘資料。 如果模型包含受到嚴格控制的敏感性資料，這是特別重要的。 在此情況下，執行 ClearCache 是可採取的預防動作，以確保敏感性資料只存在於預期的地方。 如果您使用 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] 部署模型及變更查詢模式，則需要手動清除快取。 相反地，使用 [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)] 在模型和資料分割上指定 **DirectQuery** ，則會在您將模型切換為使用該查詢模式時自動清除快取。  
  
 相較於效能測試期間清除多維度模型快取的建議，並沒有清除表格式模型快取的廣泛建議。 如果您未管理包含敏感性資料的表格式模型部署，則沒有需要清除快取的特定管理工作。  
  
## <a name="clear-the-cache-for-analysis-services-models"></a>清除 Analysis Services 模型的快取  
 若要清除快取，請使用 XMLA 和 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]。 您可以清除資料庫、Cube、維度、資料表或量值群組層級的快取。 下列清除資料庫層級快取的步驟適用於多維度模型和表格式模型。  
  
> [!NOTE]  
>  嚴格的效能測試可能需要更完整的方法來清除快取。 如需如何排清 Analysis Services 和檔案系統快取的指示，請參閱 [SQL Server 2008 R2 Analysis Services Operations Guide](http://go.microsoft.com/fwlink/?linkID=http://go.microsoft.com/fwlink/?LinkID=225539)(SQL Server 2008 R2 Analysis Services 操作指南) 中關於清除快取的章節。  
  
 對於多維度和表格式模型，清除部分快取是兩步驟的程序，包含在執行 ClearCache 時導致快取無效，接著在接收下一個查詢時清空快取。 記憶體耗用量只在快取實際上清空後才會明顯減少。  
  
 清除快取需要您在 XMLA 查詢中的 **ClearCache** 陳述式提供物件識別碼。 本主題中的第一個步驟解釋如何取得物件識別碼。  
  
#### <a name="step-1-get-the-object-identifier"></a>步驟 1：取得物件識別碼  
  
1.  在 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] 中，以滑鼠右鍵按一下物件，並選取 [屬性]，然後將 ID 屬性的值複製到 [屬性] 窗格。 這種方法適用於資料庫、Cube、維度或資料表。  
  
2.  若要取得量值群組識別碼，以滑鼠右鍵按一下該量值群組並選取 [編寫量值群組的指令碼為]。 選擇 [建立] 或 [改變]，並將查詢傳送至視窗。 量值群組識別碼會在物件定義中顯示。 複製物件定義的識別碼。  
  
#### <a name="step-2-run-the-query"></a>步驟 2：執行查詢  
  
1.  在 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] 中，以滑鼠右鍵按一下資料庫，並指向 [新增查詢]，然後選取 [XMLA]。  
  
2.  將下列程式碼範例複製到 XMLA 查詢視窗。 將 **DatabaseID** 變更為目前連接上的資料庫識別碼。  
  
    ```  
    <ClearCache xmlns="http://schemas.microsoft.com/analysisservices/2003/engine">  
      <Object>  
        <DatabaseID> Adventure Works DW Multidimensional</DatabaseID>  
      </Object>  
    </ClearCache>  
  
    ```  
  
     或者，您也可以指定子物件 (例如量值群組) 的路徑，只清除該物件的快取。  
  
    ```  
    <ClearCache xmlns="http://schemas.microsoft.com/analysisservices/2003/engine">  
      <Object>  
        <DatabaseID>Adventure Works DW Multidimensional</DatabaseID>  
            <CubeID>Adventure Works</CubeID>  
            <MeasureGroupID>Fact Currency Rate</MeasureGroupID>  
      </Object>  
    </ClearCache>  
    ```  
  
3.  按 F5 執行查詢。 您應該會看到下列結果：  
  
    ```  
    <return xmlns="urn:schemas-microsoft-com:xml-analysis">  
      <root xmlns="urn:schemas-microsoft-com:xml-analysis:empty" />  
    </return>  
    ```  
  
## <a name="see-also"></a>另請參閱  
 [監視 Analysis Services 執行個體](../../analysis-services/instances/monitor-an-analysis-services-instance.md)  
  
  

