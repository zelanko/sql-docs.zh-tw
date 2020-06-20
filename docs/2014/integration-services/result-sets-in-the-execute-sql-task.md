---
title: 執行 SQL 工作中的結果集 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- result sets [Integration Services]
- Execute SQL task [Integration Services]
ms.assetid: 62605b63-d43b-49e8-a863-e154011e6109
author: janinezhang
ms.author: janinez
ms.openlocfilehash: 535ab473d8fe6cf9a89fafa1fc0c9f45b0096f7e
ms.sourcegitcommit: f71e523da72019de81a8bd5a0394a62f7f76ea20
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/17/2020
ms.locfileid: "84964568"
---
# <a name="result-sets-in-the-execute-sql-task"></a>執行 SQL 工作中的結果集
  在 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 封裝中，結果集是否會傳回到執行 SQL 工作，端視工作所使用的 SQL 命令類型而定。 例如，SELECT 陳述式通常會傳回結果集，INSERT 陳述式則不會。  
  
 結果集所包含的內容也會隨著 SQL 命令而有所不同。 例如，來自 SELECT 陳述式的結果集可包含零個資料列、一個資料列或多個資料列。 但是，SELECT 陳述式中傳回計數或總和的結果集只包含單一資料列。  
  
 在執行 SQL 工作中使用結果集比只是知道 SQL 命令是否傳回結果集，以及結果集所包含的內容還要複雜。 若要在執行 SQL 工作中成功使用結果集，需要有其他使用需求與指導方針。 本主題的其餘部分包含這些使用需求和指導方針：  
  
-   [指定結果集類型](#Result_set_type)  
  
-   [以結果集填入變數](#Populate_variable_with_result_set)  
  
-   [在執行 SQL 工作編輯器中設定結果集](#Configure_result_sets)  
  
##  <a name="specifying-a-result-set-type"></a><a name="Result_set_type"></a>指定結果集類型  
 執行 SQL 工作支援下列類型的結果集︰  
  
-   **無** ：結果集是在查詢未傳回任何結果時使用。 例如，此結果集用於加入、變更和刪除資料表中記錄的查詢。  
  
-   **單一資料列** ：結果集是在查詢只傳回一個資料列時使用。 例如，此結果集用於傳回計數或總和的 SELECT 陳述式。  
  
-   **完整結果集** ：結果集是在查詢傳回多個資料列時使用。 例如，此結果集用於擷取資料表中所有資料列的 SELECT 陳述式。  
  
-   **XML** ：結果集是在查詢傳回 XML 格式的結果集時使用。 例如，此結果集用於包含 FOR XML 子句的 SELECT 陳述式。  
  
 如果執行 SQL 工作使用 **[完整結果集]** 結果集，且查詢傳回多個資料列集，則工作只會傳回第一個資料列集。 如果此資料列集產生錯誤，則工作會報告該錯誤。 如果其他資料列集產生錯誤，則工作不會報告它們。  
  
##  <a name="populating-a-variable-with-a-result-set"></a><a name="Populate_variable_with_result_set"></a>以結果集填入變數  
 如果查詢傳回的結果集類型為單一資料列、資料列集或 XML，則您可將結果集繫結至使用者自訂的變數。  
  
 如果結果集類型為 **Single row**，則可以藉由使用資料行名稱做為結果集名稱將傳回結果中的資料行繫結至變數，或者可以使用資料行清單中資料行的序數位置做為結果集名稱。 例如，查詢 `SELECT Color FROM Production.Product WHERE ProductID = ?` 的結果集名稱可以為 **Color** 或 **0**。 如果查詢傳回多個資料行，並且您要存取所有資料行中的值，則您必須將每個資料行繫結至不同的變數。 如果您透過使用數字做為結果集名稱將資料行對應至變數，則該數字會反映資料行在查詢的資料行清單中所顯示的順序。 例如，在查詢 `SELECT Color, ListPrice, FROM Production.Product WHERE ProductID = ?`中，您將 0 用於 **Color** 資料行，將 1 用於 **ListPrice** 資料行。 使用資料行名稱做為結果集名稱的功能取決於將該工作設定為使用的提供者。 並非所有的提供者可以使用資料行名稱做為結果集名稱。  
  
 部分傳回單一值的查詢可能不包含資料行名稱。 例如， `SELECT COUNT (*) FROM Production.Product` 陳述式不會傳回任何資料行名稱。 您可以使用序數位置 0 做為結果名稱來存取傳回的結果。 若要依據資料行名稱存取傳回的結果，查詢必須包含 AS \<alias name> 子句來提供資料行名稱。 `SELECT COUNT (*)AS CountOfProduct FROM Production.Product`陳述式會提供 **CountOfProduct** 資料行。 接著您可以使用 **CountOfProduct** 資料行名稱或序數位置 0 來存取傳回結果資料行。  
  
 如果結果集類型為 **完整結果集** 或 **XML**，則必須使用 0 作為結果集名稱。  
  
 當您將變數對應至結果集類型為 **Single row** 的結果集時，此變數須具有與結果集包含的資料行之資料類型相容的資料類型。 例如，包含資料類型為 `String` 之資料行的結果集不能對應至數值資料類型的變數。 當您將**TypeConversionMode**屬性設定為時 `Allowed` ，「執行 SQL」工作會嘗試將輸出參數和查詢結果轉換為指派結果之變數的資料類型。  
  
 XML 結果集只可對應至資料類型為 `String` 或 `Object` 的變數。 如果變數有 `String` 資料類型，則執行 SQL 工作會傳回字串，且 XML 來源可使用 XML 資料。 如果變數有 `Object` 資料類型，則執行 SQL 工作會傳回「文件物件模組 (DOM)」物件。  
  
 **完整結果集**必須對應至 `Object` 資料類型的變數。 傳回結果為資料列集物件。 您可以使用 Foreach 迴圈容器，將儲存在 Object 變數中的資料表資料列值，擷取到封裝變數中，然後使用指令碼工作，將儲存在封裝變數中的資料寫入檔案。 如需如何使用 Foreach 迴圈容器和指令碼工作執行此作業的示範，請參閱 msftisprodsamples.codeplex.com 上的 CodePlex 範例 [執行 SQL 參數及結果集](https://go.microsoft.com/fwlink/?LinkId=157863)(英文)。  
  
 下表列出可對應至結果集之變數的資料類型。  
  
|結果集類型|變數的資料類型|物件類型|  
|---------------------|---------------------------|--------------------|  
|單一資料列|與結果集之類型資料行相容的任何類型。|不適用|  
|完整結果集|`Object`|如果工作使用原生連接管理員 (包括 ADO、OLE DB、Excel 與 ODBC 連接管理員)，則傳回的物件是 ADO `Recordset`。<br /><br /> 如果工作使用 Managed 連接管理員 (例如 [!INCLUDE[vstecado](../includes/vstecado-md.md)] 連接管理員)，傳回的物件便會是 `System.Data.DataSet`。<br /><br /> 您可以使用指令碼工作來存取 `System.Data.DataSet` 物件，如下列範例所示。<br /><br /> `Dim dt As Data.DataTable` <br /> `Dim ds As Data.DataSet = CType(Dts.Variables("Recordset").Value, DataSet)` <br /> `dt = ds.Tables(0)`|  
|XML|`String`|`String`|  
|XML|`Object`|如果工作使用原生連接管理員 (包括 ADO、OLE DB、Excel 與 ODBC 連接管理員)，則傳回的物件是 `MSXML6.IXMLDOMDocument`。<br /><br /> 如果工作使用 Managed 連接管理員 (例如 [!INCLUDE[vstecado](../includes/vstecado-md.md)] 連接管理員)，那麼傳回的物件是 `System.Xml.XmlDocument`。|  
  
 變數可在執行 SQL 工作或封裝範圍內定義。 如果變數包含封裝範圍，則結果集可用於該封裝內的其他工作和容器，並可用於「執行封裝」或「執行 DTS 2000 封裝」工作所執行的任何封裝。  
  
 將變數對應到 **單一資料列** 結果集時，如果符合下列條件，SQL 陳述式傳回的非字串值就會轉換為字串：  
  
-   **TypeConversionMode** 屬性設為 True。 您可以在 [屬性] 視窗中設定屬性值，也可以使用 **[執行 SQL 工作編輯器]**。  
  
-   轉換不會導致資料截斷。  
  
 如需將結果集載入變數中的資訊，請參閱 [在執行 SQL 工作中將結果集對應至變數](control-flow/execute-sql-task.md)。  
  
##  <a name="configuring-result-sets-in-the-execute-sql-task"></a><a name="Configure_result_sets"></a>在執行 SQL 工作中設定結果集  
 如需有關可以在 [!INCLUDE[ssIS](../includes/ssis-md.md)] 設計師中設定之結果集屬性的詳細資訊，請按下列主題：  
  
-   [[執行 SQL 工作編輯器] &#40;[結果集] 頁面&#41;](../../2014/integration-services/execute-sql-task-editor-result-set-page.md)  
  
 如需有關如何在「 [!INCLUDE[ssIS](../includes/ssis-md.md)] 設計師」中設定這些屬性的詳細資訊，請按下列主題：  
  
-   [設定工作或容器的屬性](../../2014/integration-services/set-the-properties-of-a-task-or-container.md)  
  
## <a name="related-tasks"></a>相關工作  
 [在執行 SQL 工作中將結果集對應至變數](control-flow/execute-sql-task.md)  
  
## <a name="related-content"></a>相關內容  
  
-   位於 msftisprodsamples.codeplex.com 的 CodePlex 範例： [執行 SQL 參數和結果集](https://go.microsoft.com/fwlink/?LinkId=157863)  
  
  
