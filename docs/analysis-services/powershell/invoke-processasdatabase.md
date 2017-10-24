---
title: "叫用 ProcessASDatabase |Microsoft 文件"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
ms.tgt_pltfrm: 
ms.topic: reference
ms.assetid: 66d5d154-88ce-4c2e-b1ef-e2d2f6fb1c44
caps.latest.revision: 11
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: f8e83493ed934a3f9bf32a1cef35969f04996223
ms.contentlocale: zh-tw
ms.lasthandoff: 09/01/2017

---
# <a name="invoke-processasdatabase"></a>Invoke-ProcessASDatabase

[!INCLUDE[ssas-appliesto-sqlas-all-aas](../../includes/ssas-appliesto-sqlas-all-aas.md)]

  在指定的 **Database** 進行 **Process** 作業，使用特定 **ProcessType** 或 **RefreshType** ，視基礎中繼資料類型而定。  
  
 使用 **ProcessType** 作為資料庫，並使用多維度中繼資料 (這包括相容性層級 1050、1100 或 1103 的表格式資料庫)。  
  
 使用 **RefreshType** 作為表格式資料庫，相容性層級 1200 或更高。  

>[!NOTE] 
>這份文件可能包含過時的資訊和範例。 使用 Get-help cmdlet 取得最新。
  
## <a name="syntax"></a>語法  
 `Invoke-ProcessASDatabase [-DatabaseName] <string> [-RefreshType] <RefreshType> {Full | ClearValues | Calculate |     DataOnly | Automatic | Add | Defragment} [-Server <string>] [-Credential <pscredential>] [-WhatIf] [-Confirm]     [<CommonParameters>]`  
  
 `Invoke-ProcessASDatabase [-DatabaseName] <string> [-ProcessType] <ProcessType> {ProcessFull | ProcessAdd |     ProcessUpdate | ProcessIndexes | ProcessData | ProcessDefault | ProcessClear | ProcessStructure |     ProcessClearStructureOnly | ProcessScriptCache | ProcessRecalc | ProcessDefrag} [-Server <string>] [-Credential     <pscredential>] [-WhatIf] [-Confirm]  [<CommonParameters>]`  
  
## <a name="description"></a>說明  
 **Invoke-ProcessASDatabase** Cmdlet 會將資料庫處理至您指定的層級。 例如，若為相容性層級 1200 的表格式資料庫，將 **RefreshType** 設為 **Full** 會以所有新資料覆寫現有資料。  
  
 處理類型 (多維度) 或重新整理類型 (表格式) 是必要的，且可以在資料庫和伺服器參數之前或之後指定︰  
  
-   針對多維度，請參閱[處理選項和設定 &#40;Analysis Services&#41;](../../analysis-services/multidimensional-models/processing-options-and-settings-analysis-services.md)。  
  
-   針對表格式，請參閱[處理資料庫、資料表或資料分割 &#40;Analysis Services&#41;](../../analysis-services/tabular-models/process-database-table-or-partition-analysis-services.md)。  
  
## <a name="parameters"></a>參數  
  
### <a name="-databasename-string"></a>-DatabaseName\<字串 >  
 指定要處理的表格式或多維度資料庫。  
  
|||  
|-|-|  
|必要項？|true|  
|位置？|0|  
|預設值||  
|接受管線輸入？|false|  
|接受萬用字元？|false|  
  
### <a name="-servermicrosoftanalysissevicesserver"></a>伺服器\<Microsoft.AnalysisSevices.Server >  
 選擇性地指定如果您不是使用 **SQLAS** 提供者目錄作為內容時要連接的伺服器執行個體。  
  
|||  
|-|-|  
|必要項？|false|  
|位置？|具名|  
|預設值||  
|接受管線輸入？|false|  
|接受萬用字元？|false|  
  
### <a name="-refreshtype-microsoftanalysisservicesrefreshtype"></a>-RefreshType \<Microsoft.AnalysisServices.RefreshType >  
 指定表格式資料庫的處理類型。  有效值為 Full、ClearValues、Calculate、DataOnly、Automatic、Add 和 Defragment。 如需說明與指引，請參閱[處理資料庫、資料表或資料分割 &#40;Analysis Services&#41;](../../analysis-services/tabular-models/process-database-table-or-partition-analysis-services.md)。  
  
|||  
|-|-|  
|必要項？|true|  
|位置？|1|  
|預設值||  
|接受管線輸入？|false|  
|接受萬用字元？|false|  
  
### <a name="-processtype-microsoftanalysisservicesprocesstype"></a>-ProcessType \<Microsoft.AnalysisServices.ProcessType >  
 指定相容性層級 1050-1103 的多維度資料庫或表格式資料庫的處理類型。 有效值為：ProcessFull、ProcessAdd、ProcessUpdate、ProcessIndexes、ProcessData、ProcessDefault、ProcessClear、ProcessStructure、ProcessCelarStructureOnly、ProcessScriptCache、ProcessRecalc。 如需說明與指引，請參閱[處理選項和設定 &#40;Analysis Services&#41;](../../analysis-services/multidimensional-models/processing-options-and-settings-analysis-services.md)。  
  
|||  
|-|-|  
|必要項？|true|  
|位置？|1|  
|預設值||  
|接受管線輸入？|false|  
|接受萬用字元？|false|  
  
### <a name="-credential"></a>-Credential  
 如果指定了此參數，傳遞的使用者名稱和密碼將會用來連接到 Analysis Services 執行個體。 如果沒有指定認證，則會假設為執行指令碼之使用者的預設 Windows 帳戶。  
  
|||  
|-|-|  
|必要項？|false|  
|位置？|具名|  
|預設值||  
|接受管線輸入？|false|  
|接受萬用字元？|false|  
  
## <a name="-whatif"></a>-Whatif  
 包含此參數，以在執行之前取得作業影響的資訊。  
  
|||  
|-|-|  
|必要項？|false|  
|位置？|具名|  
|預設值||  
|接受管線輸入？|false|  
|接受萬用字元？|false|  
  
## <a name="-confirm"></a>-Confirm  
 包含此參數，以在作業執行之前以是或否回應的互動方式來確認作業。  
  
|||  
|-|-|  
|必要項？|false|  
|位置？||  
|預設值||  
|接受管線輸入？||  
|接受萬用字元？|false|  
  
## <a name="example-1-sqlas-provider"></a>範例 1 (SQLAS 提供者)  
 這個範例會使用 **SQLAS** 提供者，將內容設定為預設執行個體上的資料庫清單。  如果列出資料庫目錄的內容，您會看到所有的資料庫以及它們的處理狀態和讀寫模式。  
  
 您可以從資料庫資料夾中，執行僅指定資料庫名稱的 **Invoke-ProcessASDatabase** 。  
  
```  
PS > import-module SQLPS -DisableNameChecking  
PS  SQL Server > cd sqlas\ssas-srv-01\default\databases  
PS SQLSERVER:\sqlas\ssas-srv-01\default\databases> dir  
. . . .  
PS SQLSERVER:\sqlas\ssas-srv-01\default\databases> Invoke-ProcessASDatabase "adventureworks"  
  
```  
  
 視資料庫類型而定，系統會提示您指定 **RefreshType** 或 **ProcessType**。  
  
 處理證明是 return 陳述式的影響物件是否存在︰Microsoft.AnalysisServices.Tabular.ObjectImpact。  
  
 請注意，物件狀態資訊有時候會快取，因此如果您在處理成功之後列出目錄的內容，資料庫狀態會保留其原始的「未處理」描述元。 這會使人產生誤解，因為只要傳回 objectimact，實際上便已處理資料庫。  
  
 您可以藉由在 Management Studio 查看資料庫屬性頁面、啟動新的工作階段，或藉由從資料庫物件傳回處理狀態 (透過 [Microsoft.AnalysisServices.ProcessableMajorObject.LastProcessed](https://msdn.microsoft.com/library/microsoft.analysisservices.processablemajorobject.lastprocessed.aspx))，確認處理成功。  
  
## <a name="example-2"></a>範例 2  
 這個範例示範只使用 Cmdlet 而沒有提供者的相同作業。 需要額外的參數以指定伺服器和處理類型。  
  
```  
PS > import-module SQLPS -DisableNameChecking  
PS  SQL Server >  Invoke-ProcessASDatabase -databasename "AdventureWorks" -server '\\server-name\instancename' –ProcessType "ProcessFull"  
  
```  
  
  
  

