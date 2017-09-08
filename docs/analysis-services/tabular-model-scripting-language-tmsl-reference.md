---
title: "表格式模型指令碼語言 (TMSL) 參考 |Microsoft 文件"
ms.custom:
- SQL2016_New_Updated
ms.date: 03/06/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
ms.assetid: c700d7f8-7e01-4052-a9ad-8200dd4009f2
caps.latest.revision: 20
author: Minewiskan
ms.author: owend
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 875dd29a77a341e3d40502002488fc0189947c9d
ms.contentlocale: zh-tw
ms.lasthandoff: 09/01/2017

---
# <a name="tabular-model-scripting-language-tmsl-reference"></a>表格式模型指令碼語言 (TMSL) 參考

[!INCLUDE[ssas-appliesto-sql2016-later-aas](../includes/ssas-appliesto-sql2016-later-aas.md)]

  表格式模型指令碼語言 (TMSL) 是命令和物件模型定義的相容性層級 1200年或更高版本的 Analysis Services 表格式模型資料庫。 Analysis Services 透過 XMLA 通訊協定，與外界溝通 TMSL 其中[XMLA。執行](../analysis-services/xmla/xml-elements-methods-execute.md)方法接受 JSON 型**陳述式**TMSL 與傳統 XML 架構中的指令碼中的指令碼[Analysis Services 指令碼語言 &#40;ASSL XMLA &#41;](../analysis-services/scripting/analysis-services-scripting-language-assl-for-xmla.md).  
  
 TMSL 的重要元素如下：  
  
-   表格式模型的語意為基礎的表格式中繼資料。 表格式模型是由資料表、 資料行和關聯性所組成。 對等物件定義以 TMSL 是現在，顯而易見地，資料表、 資料行、 關聯性和其他等等。  
  
     新的中繼資料引擎就會支援這些定義。  
  
-   物件定義的結構為 JSON 而不是 XML。  
  
 除了裝載格式化 （以 JSON 或 XML） 的方式，ASSL 和 TMSL 而且功能上相當於它們如何提供命令和中繼資料，以用於伺服器的通訊和資料傳輸的 XMLA 方法。  
  
## <a name="how-to-use-tmsl"></a>如何使用 TMSL  
 瀏覽 TMSL 指令碼的最簡單方式使用 CREATE、 ALTER、 DELETE 或處理程序命令在 SQL Server Management Studio (SSMS) 模型，您已經知道。 假設您使用現有的模型，請記得先升級至 1200年或更高的相容性層級。  
  
1.  找到您想要使用的命令：[中表格式模型指令碼語言 &#40; 命令TMSL &#41;](../analysis-services/tabular-models-scripting-language-commands/tmsl-reference-commands.md)  
  
2.  請檢查命令中使用物件的物件定義參考：[中表格式模型指令碼語言 &#40; 物件定義TMSL &#41;](../analysis-services/tabular-models-scripting-language-objects/tmsl-reference-tabular-objects.md)  
  
3.  選擇 提交 TMSL 指令碼的方式：  
  
    -   在 Management Studio 中的 XMLA 視窗  
  
    -   **叫用 ascmd**透過 AMO PowerShell ([Invoke-ascmd 指令程式](../analysis-services/powershell/invoke-ascmd-cmdlet.md))  
  
    -   [Analysis Services 執行 DDL 工作](../integration-services/control-flow/analysis-services-execute-ddl-task.md)在 SSIS 中。  
  
## <a name="model-definition-schema"></a>模型定義結構描述  
 下列螢幕擷取畫面顯示精簡的結構描述中，摺疊以顯示主要的物件。  
  
 ![SSAS_TabularMetadata](../analysis-services/media/ssas-tabularmetadata.JPG "SSAS_TabularMetadata")  
  
## <a name="scripting-languages-in-analysis-services"></a>在 Analysis Services 指令碼語言  
 Analysis Services 支援 ASSL 和 TMSL 指令碼語言。 只有建立 1200年相容性層級或更高的表格式模型所述 TMS JSON 格式。  
  
 [Analysis Services 指令碼語言 &#40;ASSL XMLA &#41;](../analysis-services/scripting/analysis-services-scripting-language-assl-for-xmla.md)是第一個指令碼語言，而且仍然是只有多維度模型和較低的相容性層級 （1100年或 1103年） 的表格式模型指令碼語言。 ASSL 中, 表格式 110 x 模型中所述多維度的詞彙，例如**cube** （適用於模型） 和**measuregroup** （適用於資料表）。  
  
> [!NOTE]  
>  在 [SQL Server Data Tools (SSDT)，您可以將較早版本表格式模型升級使用 TMSL 啟動其**CompatibilityLevel**為 1200年或更高。 請記住，升級無法回復。 之前升級，請備份您的模型，您稍後需要原始版本。  
  
 下表是在特定的相容性層級的不同版本的 Analysis Services 資料模型的指令碼語言矩陣。  

||||||  
|-|-|-|-|-|  
|**版本**|**多維度**|**表格式 110 x**|**表格式 1200**| **表格式 1400** |
|Azure Analysis Services|NA|NA|TMSL|TMSL| 
|SQL Server 2017|ASSL|ASSL|TMSL|TMSL| 
|SQL Server 2016|ASSL|ASSL|TMSL|TMSL| 
|SQL Server 2014|ASSL|ASSL|NA|NA|   
|SQL Server 2012|ASSL|ASSL|NA|NA|  

  
## <a name="see-also"></a>另請參閱  
 [Analysis Services 中表格式模型的相容性層級](../analysis-services/tabular-models/compatibility-level-for-tabular-models-in-analysis-services.md)   
 [Analysis Services 指令碼語言 &#40;ASSL XMLA &#41;](../analysis-services/scripting/analysis-services-scripting-language-assl-for-xmla.md)   
 [判斷 Analysis Services 執行個體的伺服器模式](../analysis-services/instances/determine-the-server-mode-of-an-analysis-services-instance.md)  
  
  
