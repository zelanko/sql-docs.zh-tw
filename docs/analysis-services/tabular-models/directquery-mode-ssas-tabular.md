---
title: DirectQuery 模式 |Microsoft 文件
ms.date: 05/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: tabular-models
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: a65db56348dd58f8d3db242cc565a2ed1b4c6062
ms.sourcegitcommit: 38f8824abb6760a9dc6953f10a6c91f97fa48432
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/10/2018
---
# <a name="directquery-mode"></a>DirectQuery 模式
[!INCLUDE[ssas-appliesto-sqlas-aas](../../includes/ssas-appliesto-sqlas-aas.md)]
  本文說明*DirectQuery 模式*1200年 （含） 以上的相容性層級的 Analysis Services 表格式模型。 您可以針對在 SSDT 中設計的模型開啟 DirectQuery 模式；或者，針對已部署的表格式模型，則可以在 SSMS 中變更為 DirectQuery 模式。 選擇 DirectQuery 模式之前，請務必了解優點與限制。
  
##  <a name="bkmk_Benefits"></a> 優點
 根據預設，表格式模型會使用記憶體中快取來儲存和查詢資料。 當表格式模型查詢位於記憶體中的資料時，即使是複雜查詢也可以非常快速地執行。 但是，使用快取資料有一些限制。 那就是，大型資料集可以超過可用的記憶體，且如果在正常處理排程上並非不可能達成的話，資料有效性需求可能會有困難。  
  
 DirectQuery 會克服這些限制，同時也利用 RDBMS 功能，讓查詢執行更有效率。 使用 DirectQuery：  
  
-   資料是最新的，並且沒有必須維護另一份資料複本的額外管理負荷 (在記憶體內部快取中)。 基礎來源資料的變更可立即反映在對資料模型的查詢中。  
  
-   資料集可以大於 Analysis Services 伺服器的記憶體容量。  
  
-   DirectQuery 可以利用提供者端的查詢加速功能，例如記憶體最佳化資料行索引所提供。  
  
-   後端資料庫可以使用資料庫中的資料列層級安全性功能來執行安全 (或者，您可以透過 DAX 在模型中使用資料列層級安全性)。  
  
-   如果模型包含可能需要多個查詢的複雜公式，Analysis Services 可以執行最佳化，以確保對後端資料庫執行之查詢的查詢計畫將盡可能有效率。  
  
##  <a name="bkmk_prereq"></a>限制
DirectQuery 模式中的表格式模型具有一些限制。 在切換模式之前，請務必判斷在後端伺服器上執行查詢的優點是否遠大於任何功能降低。  
  
 如果您變更 [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)]中現有模型的模式，模型設計師會通知您模型中任何與 DirectQuery 模式不相容的功能。  
  
 下列清單摘要說明須注意的主要功能限制︰  
  
|||  
|-|-|  
|**功能區**|**限制**|  
|**資料來源**|DirectQuery 模型只能使用下列類型之單一關聯式資料庫的資料：SQL Server、Azure SQL Database、Oracle 和 Teradata。  如需版本和提供者資訊，請參閱本文後面 DirectQuery 所支援的資料來源。| 
|**SQL 預存程序**|針對 DirectQuery 模型，使用 [資料匯入精靈] 時，不能在 SQL 陳述式中指定預存程序來定義資料表。 |   
|**計算資料表**|DirectQuery 模型中不支援導出資料表，但支援導出資料行。 如果您嘗試轉換包含導出資料表的表格式模型，會出現錯誤，指出模型不能包含貼上的資料。|  
|**查詢限制**|預設資料列限制是一百萬個資料列，而在 msmdsrv.ini 檔案中指定 **MaxIntermediateRowSize** 就可以增加此值。 如需詳細資訊，請參閱 [DAX 屬性](../../analysis-services/server-properties/dax-properties.md) 。
|**DAX 公式**|使用 DirectQuery 模式查詢表格式模型時， [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 會將 DAX 公式和量值定義轉換成 SQL 陳述式。 包含無法轉換為 SQL 語法之元素的 DAX 公式會傳回模型的驗證錯誤。<br /><br /> 這項限制通常限制於特定 DAX 函數。 若是量值，DAX 公式會針對關聯式資料存放區轉換為以集合為基礎的作業。 這表示支援以隱含方式建立的所有量值。 <br /><br /> 發生驗證錯誤時，您需要替代不同的函數來重新撰寫公式，或使用資料來源中的衍生資料行來因應。  當您在設計工具中切換至 DirectQuery 模式時，就會回報表格式模型包括含有不相容函數的公式。 <br /><br />**注意：**  在您將模型切換至 DirectQuery 模式時，模型中的公式可能會通過驗證，但在對快取和關聯式資料存放區執行時，則會傳回不同的結果。 這是因為對快取的計算使用記憶體內部分析引擎的語意，其中包含用於模擬 Excel 行為的功能，而針對關聯式資料來源中所儲存資料的查詢會使用 SQL Server 的語意。<br /><br /> SQL 預存  <br /><br /> 若要進一步了解，請參閱[DirectQuery 模式中的 DAX 公式相容性](../../analysis-services/tabular-models/dax-formula-compatibility-in-directquery-mode-ssas-2016.md)。|  
|**公式的一致性**|在某些情況下，相較於只使用關聯式資料存放區的 DirectQuery 模型，相同公式可能在快取模型下傳回不同的結果。 這些差異是由於記憶體中分析引擎和 SQL Server 之間的語意差異所導致。<br /><br /> 如需相容性問題，包括可能會傳回不同的結果時將模型部署至即時環境的函式的完整清單，請參閱[DirectQuery 模式 (SQL Server Analysis Services) 中的 DAX 公式相容性](http://msdn.microsoft.com/en-us/981b6a68-434d-4db6-964e-d92f8eb3ee3e)。|  
|**MDX 限制**|沒有相對的物件名稱。 所有的物件名稱必須是完整名稱。<br /><br /> 沒有工作階段範圍的 MDX 陳述式 (具名的集合、導出成員、導出資料格、視覺化總計、預設成員等等)，但是您可以使用查詢範圍建構，例如 'WITH' 子句。<br /><br /> 無具有與 MDX subselect 子句中的不同層級成員的 Tuple。<br /><br /> 無使用者定義的階層。<br /><br /> 沒有原生 SQL 查詢 (一般來說，Analysis Services 支援 T-SQL 子集，但 DirectQuery 模型則不適用)。|  

## <a name="data-sources-supported-for-directquery"></a>DirectQuery 支援的資料來源
相容性層級 1200年 （含） 以上的 DirectQuery 表格式模型是相容的下列資料來源和提供者：

資料來源   |版本  |提供者
---------|---------|---------
Microsoft SQL Server    |  2008 及更新版本      |       OLE DB Provider for SQL Server、SQL Server Native Client OLE DB 提供者、.NET Framework Data Provider for SQL Client  
Microsoft Azure SQL Database    |   全部      |  OLE DB Provider for SQL Server、SQL Server Native Client OLE DB 提供者、.NET Framework Data Provider for SQL Client            
Microsoft Azure SQL 資料倉儲     |   全部     |  .NET Framework Data Provider for SQL Client       
Microsoft SQL Analytics Platform System (APS)     |   全部      |  OLE DB Provider for SQL Server、SQL Server Native Client OLE DB 提供者、.NET Framework Data Provider for SQL Client       
Oracle 關聯式資料庫     |  Oracle 9i 和更新版本       |  Oracle OLE DB Provider       
Teradata 關聯式資料庫    |  Teradata V2R6 和更新版本     | .Net Data Provider for Teradata        

## <a name="connecting-to-a-data-source"></a>連接到資料來源
在 SSDT 中設計 DirectQuery 模型時，連接到資料來源以及選取要包括在模型中的資料表和欄位，與使用記憶體內部模型相同。 

如果您已經開啟 DirectQuery，但尚未連接到資料來源，則可以使用 [資料表匯入精靈] 連接到資料來源、選取資料表和欄位、指定 SQL 查詢等。 差別在於完成時，記憶體內部快取實際上未匯入任何資料。 

![DirectQuery 匯入成功](../../analysis-services/tabular-models/media/directquery-import-success.png)

如果您已經使用 [資料表匯入精靈] 匯入資料，但尚未開啟 DirectQuery 模式，則這麼做將會清除記憶體內部快取。

  
## <a name="additional-articles-in-this-section"></a>本節中的其他文件
[在 SSDT 中啟用 DirectQuery 模式](../../analysis-services/tabular-models/enable-directquery-mode-in-ssdt.md)

[在 SSMS 中啟用 DirectQuery 模式](../../analysis-services/tabular-models/enable-directquery-mode-in-ssms.md)

[在設計模式中將範例資料加入 DirectQuery 模型中](../../analysis-services/tabular-models/add-sample-data-to-a-directquery-model-in-design-mode.md)

[在 DirectQuery 模式中定義分割區](../../analysis-services/tabular-models/define-partitions-in-directquery-models-ssas-tabular.md)
  
[在 DirectQuery 模式中測試模型](../../analysis-services/tabular-models/test-a-model-in-directquery-mode.md)

[在 DirectQuery 模式中的 DAX 公式相容性](../../analysis-services/tabular-models/dax-formula-compatibility-in-directquery-mode-ssas-2016.md)
  
