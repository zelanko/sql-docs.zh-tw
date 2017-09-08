---
title: "Analysis Services 執行 DDL 工作 |Microsoft 文件"
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
- sql13.dts.designer.asexecuteddltask.f1
- sql13.dts.designer.asexecuteddltask.general.f1
- sql13.dts.designer.asexecuteddltask.ddl.f1
helpviewer_keywords:
- Analysis Services Execute DDL task
- DDL
ms.assetid: 7f25c8c6-b601-41f2-9553-be0a2ee0751a
caps.latest.revision: 48
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 8806c102eaec2c2540374bfaddc33b76d8f6e584
ms.openlocfilehash: a8272f3306050e8d184fd6d5e4e3d349c4e259e9
ms.contentlocale: zh-tw
ms.lasthandoff: 08/11/2017

---
# <a name="analysis-services-execute-ddl-task"></a>Analysis Services 執行 DDL 工作
  「 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 執行 DDL」工作會執行可建立、卸除或修改採礦模型和多維度物件 (如 Cube 和維度) 的資料定義語言 (DDL) 陳述式。 例如，DDL 陳述式可在 **Adventure Works** Cube 中建立資料分割，或在 [!INCLUDE[ssAWDWsp](../../includes/ssawdwsp-md.md)] ([!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 中所含的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]範例資料庫) 中刪除維度。  
  
 「 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 執行 DDL」工作會使用 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 連接管理員連接到 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 的執行個體或 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 專案。 如需相關資訊，請參閱 [Analysis Services Connection Manager](../../integration-services/connection-manager/analysis-services-connection-manager.md)。  
  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 包括多項執行商業智慧作業的工作，例如處理分析物件和執行資料採礦預測查詢。  
  
 如需有關相關之商業智慧工作的詳細資訊，請按下列其中一個主題：  
  
-   [Analysis Services 處理工作](../../integration-services/control-flow/analysis-services-processing-task.md)  
  
-   [資料採礦查詢工作](../../integration-services/control-flow/data-mining-query-task.md)  
  
## <a name="ddl-statements"></a>DDL 陳述式  
 DDL 陳述式會在 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 指令碼語言 (ASSL) 中以陳述式的方式呈現，在 XML for Analysis (XMLA) 命令中則會加上框架。  
  
-   ASSL 是用來定義和描述 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 的執行個體，及其包含的資料庫和資料庫物件。 如需詳細資訊，請參閱 [Analysis Services 指令碼語言 &#40;ASSL&#41; 參考](../../analysis-services/scripting/analysis-services-scripting-language-assl-for-xmla.md)。  
  
-   XMLA 為命令語言，用來傳送動作命令 (如「建立」、「改變」或「處理」) 至 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 的執行個體。 如需詳細資訊，請參閱 [XML for Analysis &#40;XMLA&#41; 參考](../../analysis-services/xmla/xml-for-analysis-xmla-reference.md)。  
  
 如果 DDL 程式碼存放在另一個檔案中，「[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 執行 DDL」工作便會使用「檔案」連線管理員指定該檔案的路徑。 如需相關資訊，請參閱 [File Connection Manager](../../integration-services/connection-manager/file-connection-manager.md)。  
  
 由於 DDL 陳述式可能包含密碼和其他機密資訊，因此包含一或多項「[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 執行 DDL」工作的封裝應使用封裝保護等級 **EncryptAllWithUserKey** 或 **EncryptAllWithPassword**。 如需詳細資訊，請參閱 [Integration Services &#40;SSIS&#41; 封裝](../../integration-services/integration-services-ssis-packages.md)。  
  
### <a name="ddl-examples"></a>DDL 範例  
 下列三種 DDL 陳述式由 [!INCLUDE[ssAWDWsp](../../includes/ssawdwsp-md.md)] ([!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 中所含的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]資料庫) 中的指令碼物件所產生。  
  
 下列 DDL 陳述式會刪除 **Promotion** 維度。  
  
```  
<Delete xmlns="http://schemas.microsoft.com/analysisservices/2003/engine">  
    <Object>  
        <DatabaseID>Adventure Works DW Multidimensional 2012</DatabaseID>  
        <DimensionID>Dim Promotion</DimensionID>  
    </Object>  
</Delete>  
  
```  
  
 下列 DDL 陳述式會處理 [!INCLUDE[ssAWDWsp](../../includes/ssawdwsp-md.md)] Cube。  
  
```  
<Batch xmlns="http://schemas.microsoft.com/analysisservices/2003/engine">  
  <Parallel>  
    <Process xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">  
      <Object>  
        <DatabaseID>Adventure Works DW Multidimensional 2012</DatabaseID>  
      </Object>  
      <Type>ProcessFull</Type>  
      <WriteBackTableCreation>UseExisting</WriteBackTableCreation>  
    </Process>  
  </Parallel>  
</Batch>  
  
```  
  
 下列 DDL 陳述式會建立 **預測** 採礦模型。  
  
```  
<Create xmlns="http://schemas.microsoft.com/analysisservices/2003/engine">  
    <ParentObject>  
        <DatabaseID>Adventure Works DW Multidimensional 2012</DatabaseID>  
        <MiningStructureID>Forecasting</MiningStructureID>  
    </ParentObject>  
    <ObjectDefinition>  
        <MiningModel xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">  
            <ID>Forecasting</ID>  
            <Name>Forecasting</Name>  
            <Algorithm>Microsoft_Time_Series</Algorithm>  
            <AlgorithmParameters>  
                <AlgorithmParameter>  
                    <Name>PERIODICITY_HINT</Name>  
                    <Value xsi:type="xsd:string">{12}</Value>  
                </AlgorithmParameter>  
            </AlgorithmParameters>  
            <Columns>  
                <Column>  
                    <ID>Amount</ID>  
                    <Name>Amount</Name>  
                    <SourceColumnID>Amount</SourceColumnID>  
                    <Usage>Predict</Usage>  
                </Column>  
                <Column>  
                    <ID>Model Region</ID>  
                    <Name>Model Region</Name>  
                    <SourceColumnID>Model Region</SourceColumnID>  
                    <Usage>Key</Usage>  
                </Column>  
                <Column>  
                    <ID>Quantity</ID>  
                    <Name>Quantity</Name>  
                    <SourceColumnID>Quantity</SourceColumnID>  
                    <Usage>Predict</Usage>  
                </Column>  
                <Column>  
                    <ID>Time Index</ID>  
                    <Name>Time Index</Name>  
                    <SourceColumnID>Time Index</SourceColumnID>  
                    <Usage>Key</Usage>  
                </Column>  
            </Columns>  
            <Collation>Latin1_General_CS_AS_KS</Collation>  
        </MiningModel>  
    </ObjectDefinition>  
</Create>  
  
```  
  
 下列三種 DDL 陳述式由 [!INCLUDE[ssAWDWsp](../../includes/ssawdwsp-md.md)] ([!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 中所含的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]資料庫) 中的指令碼物件所產生。  
  
 下列 DDL 陳述式會刪除 **Promotion** 維度。  
  
```  
<Delete xmlns="http://schemas.microsoft.com/analysisservices/2003/engine">  
    <Object>  
        <DatabaseID>Adventure Works DW Multidimensional 2012</DatabaseID>  
        <DimensionID>Dim Promotion</DimensionID>  
    </Object>  
</Delete>  
  
```  
  
 下列 DDL 陳述式會處理 [!INCLUDE[ssAWDWsp](../../includes/ssawdwsp-md.md)] Cube。  
  
```  
<Batch xmlns="http://schemas.microsoft.com/analysisservices/2003/engine">  
  <Parallel>  
    <Process xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">  
      <Object>  
        <DatabaseID>Adventure Works DW Multidimensional 2012</DatabaseID>  
      </Object>  
      <Type>ProcessFull</Type>  
      <WriteBackTableCreation>UseExisting</WriteBackTableCreation>  
    </Process>  
  </Parallel>  
</Batch>  
  
```  
  
 下列 DDL 陳述式會建立 **預測** 採礦模型。  
  
```  
<Create xmlns="http://schemas.microsoft.com/analysisservices/2003/engine">  
    <ParentObject>  
        <DatabaseID>Adventure Works DW Multidimensional 2012</DatabaseID>  
        <MiningStructureID>Forecasting</MiningStructureID>  
    </ParentObject>  
    <ObjectDefinition>  
        <MiningModel xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">  
            <ID>Forecasting</ID>  
            <Name>Forecasting</Name>  
            <Algorithm>Microsoft_Time_Series</Algorithm>  
            <AlgorithmParameters>  
                <AlgorithmParameter>  
                    <Name>PERIODICITY_HINT</Name>  
                    <Value xsi:type="xsd:string">{12}</Value>  
                </AlgorithmParameter>  
            </AlgorithmParameters>  
            <Columns>  
                <Column>  
                    <ID>Amount</ID>  
                    <Name>Amount</Name>  
                    <SourceColumnID>Amount</SourceColumnID>  
                    <Usage>Predict</Usage>  
                </Column>  
                <Column>  
                    <ID>Model Region</ID>  
                    <Name>Model Region</Name>  
                    <SourceColumnID>Model Region</SourceColumnID>  
                    <Usage>Key</Usage>  
                </Column>  
                <Column>  
                    <ID>Quantity</ID>  
                    <Name>Quantity</Name>  
                    <SourceColumnID>Quantity</SourceColumnID>  
                    <Usage>Predict</Usage>  
                </Column>  
                <Column>  
                    <ID>Time Index</ID>  
                    <Name>Time Index</Name>  
                    <SourceColumnID>Time Index</SourceColumnID>  
                    <Usage>Key</Usage>  
                </Column>  
            </Columns>  
            <Collation>Latin1_General_CS_AS_KS</Collation>  
        </MiningModel>  
    </ObjectDefinition>  
</Create>  
  
```  
  
## <a name="configuration-of-the-analysis-services-execute-ddl-task"></a>設定 Analysis Services 執行 DDL 工作  
 您可以透過「 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 設計師」或以程式設計方式設定屬性。  
  
 如需有關可在 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 設計師中設定之屬性的詳細資訊，請按下列主題：  
  
-   [運算式頁面](../../integration-services/expressions/expressions-page.md)  
  
 如需在 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 設計師中設定這些屬性的詳細資訊，請按下列主題：  
  
-   [設定工作或容器的屬性](http://msdn.microsoft.com/library/52d47ca4-fb8c-493d-8b2b-48bb269f859b)  
  
## <a name="programmatic-configuration-of-the-analysis-services-execute-ddl-task"></a>以程式設計方式設定 Analysis Services 執行 DDL 工作  
 如需有關以程式設計方式設定這些屬性的詳細資訊，請按下列主題：  
  
-   <xref:Microsoft.DataTransformationServices.Tasks.DTSProcessingTask.ASExecuteDDLTask>  
  
## <a name="analysis-services-execute-ddl-task-editor-general-page"></a>Analysis Services 執行 DDL 工作編輯器 (一般頁面)
  使用 **[Analysis Services 執行 DDL 工作編輯器]** 對話方塊的 **[一般]** 頁面，即可命名並描述 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 執行 DDL 工作。  
  
### <a name="options"></a>選項。  
 **名稱**  
 提供 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 執行 DDL 工作的唯一名稱。 這個名稱是作為工作圖示中的標籤使用。  
  
> [!NOTE]  
>  工作名稱在封裝內必須是唯一的。  
  
 **說明**  
 輸入 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 執行 DDL 工作的描述。  
  
## <a name="analysis-services-execute-ddl-task-editor-ddl-page"></a>Analysis Services 執行 DDL 工作編輯器 (DDL 頁面)
  使用 [Analysis Services 執行 DDL 工作編輯器] 對話方塊的 [DDL] 頁面，即可指定 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 專案或 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 資料庫的連接，並提供資料定義語言 (DDL) 陳述式來源的相關資訊。  
  
### <a name="static-options"></a>靜態選項  
 **連接**  
 選取[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]專案或[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]連接管理員 中的清單或按一下\<**新增連接...**>，並使用**加入 Analysis Services 連接管理員**對話方塊，即可建立新的連接。  
  
 **相關主題：** [加入 Analysis Services 連線管理員對話方塊 UI 參考](../../integration-services/connection-manager/add-analysis-services-connection-manager-dialog-box-ui-reference.md)、 [Analysis Services 連線管理員](../../integration-services/connection-manager/analysis-services-connection-manager.md)  
  
 **SourceType**  
 指定 DDL 陳述式的來源類型。 此屬性具有下表所列的選項：  
  
|Value|說明|  
|-----------|-----------------|  
|**直接輸入**|將來源設定為 **[SourceDirect]** 文字方塊中所儲存的 DDL 陳述式。 選取這個值就會顯示在下列章節中的動態選項。|  
|**檔案連接**|將來源設定為包含 DDL 陳述式的檔案。 選取這個值就會顯示在下列章節中的動態選項。|  
|**變數**|將來源設定為變數。 選取這個值就會顯示在下列章節中的動態選項。|  
  
### <a name="dynamic-options"></a>動態選項  
  
#### <a name="sourcetype--direct-input"></a>SourceType = 直接輸入  
 **Source**  
 輸入 DDL 陳述式或按一下省略符號 **(…)**，然後在 **[DDL 陳述式]** 對話方塊中輸入陳述式。  
  
#### <a name="sourcetype--file-connection"></a>SourceType = 檔案連接  
 **Source**  
 在清單中，選取檔案連接，或按一下\<**新增連接...**>，並使用**檔案 」 連接管理員**對話方塊，即可建立新的連接。  
  
 **相關主題：** [檔案連線管理員](../../integration-services/connection-manager/file-connection-manager.md)  
  
#### <a name="sourcetype--variable"></a>SourceType = 變數  
 **Source**  
 在清單中，選取變數，或按一下\<**新增變數...**>，並使用**加入變數**對話方塊，即可建立新的變數。  
  
 **相關主題：** [Integration Services &#40;SSIS&#41; 變數](../../integration-services/integration-services-ssis-variables.md)  
  

