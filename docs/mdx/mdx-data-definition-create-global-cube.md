---
description: MDX 資料定義 - CREATE GLOBAL CUBE
title: CREATE GLOBAL CUBE 語句 (MDX) |Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 1bc5a787f6bc1b214aa60ef54b5b8172f07c11a5
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88494861"
---
# <a name="mdx-data-definition---create-global-cube"></a>MDX 資料定義 - CREATE GLOBAL CUBE


  根據伺服器上 Cube 的 Subcube，建立和擴展本機保存的 Cube。 連接到本機保存的 Cube 不需要連接伺服器。 如需本機 cube 的詳細資訊，請參閱 [&#40;Analysis Services 多維度資料&#41;的本機 cube ](https://docs.microsoft.com/analysis-services/multidimensional-models/olap-physical/local-cubes-analysis-services-multidimensional-data)。  
  
## <a name="syntax"></a>語法  
  
```  
  
CREATE GLOBAL CUBE local_cube_name STORAGE 'Cube_Location'   
FROM source_cube_name (<param list>)  
  
<param list>::= <param> ,<param list> | <param>  
  
<param>::= <dims list> | <measures list>  
  
<measures list>::= <measure>[, <measures list>]   
  
<dims list>::= <dim def> [, <dims list>]  
  
<measure>::= MEASURE source_cube_name.measure_name [<visibility qualifier>] [AS measure_name]   
  
<dim def>::= <source dim def> | <derived dim def>  
  
<source dim def>::= DIMENSION source_cube_name.dimension_name [<dim flags>] [<visibility qualifier>] [AS dimension_name>] [FROM <dim from clause> ] [<dim content def>]  
  
<dim flags>::= NOT_RELATED_TO_FACTS   
  
<dim from clause>::= < dim DM from clause> | <reg dim from clause>   
  
<dim DM from clause>::= dm_model_name> COLUMN column_name   
  
<dim reg from clause>::= dimension_name  
  
<dim content def>::= ( <level list> [,<grouping list>] [,<member slice list>] [,<default member>] )  
  
<level list>::= <level def> [, <level list>]  
  
<level def>::= LEVEL level_name [<level type> ] [AS level_name] [<level content def>]  
  
<level content def>::= ( <property list> ) | NO_PROPERTIES  
  
<level type>::= GROUPING  
  
<property list>::= <property def> [, <property list>]  
  
<property def>::= PROPERTY property_name   
  
<grouping list>::= <grouping entity> [,<grouping list>]  
  
<grouping entity>::= GROUP group_level_name.group_name (<mixed list>)  
  
<grp mixed list>::= <grp mixed element> [,<grp mixed list>]  
  
<grp mixed element>::= <grouping entity> | <member def>  
  
<member slice list>::= <member list>  
  
<member list>::= <member def> [, <member list>]  
  
<member def>::= MEMBER member_name  
  
<default member>::= DEFAULT_MEMBER AS MDX_expression  
  
<visibility qualifier>::= HIDDEN   
```  
  
## <a name="syntax-elements"></a>語法元素  
 local_cube_name  
 本機 Cube 的名稱。  
  
 'Cube_Location'  
 本機保存之 Cube 的名稱和路徑。  
  
 source_cube_name  
 本機 Cube 所依據的 Cube 名稱。  
  
 source_cube_name.measure_name  
 包含在本機 Cube 內之來源量值的完整名稱。 不允許使用「量值」維度的導出成員。  
  
 measure_name  
 本機 Cube 中量值的名稱。  
  
 source_cube_name.dimension_name  
 包含在本機 Cube 內之來源維度的完整名稱。  
  
 dimension_name  
 本機 Cube 中維度的名稱。  
  
 FROM \<dim from clause>  
 只適用於衍生維度定義的有效規格。  
  
 NOT_RELATED_TO_FACTS  
 只適用於衍生維度定義的有效規格。  
  
 \<level type>  
 只適用於衍生維度定義的有效規格。  
  
## <a name="remarks"></a>備註  
 本機 cube 是定義它的量值和定義的 definedin 條款。 維度有二種類型：  
  
-   來源維度 - 這些是屬於來源 Cube 的維度。  
  
-   衍生維度 - 這些是提供新分析功能的維度。 衍生維度可以是根據水平或垂直切割的來源維度所定義的一般維度，或包含自訂維度成員群組的一般維度。 衍生維度也可以是以資料採礦模型為基礎的資料採礦維度。  
  
> [!NOTE]  
>  Dimension 關鍵字所指的可以是維度或階層。  
  
 在本機 Cube 中，您可以執行下列工作：  
  
-   刪除存在來源 Cube 中的維度  
  
-   在維度中加入或刪除階層  
  
-   刪除量值群組或特定量值  
  
 CREATE GLOBAL CUBE 陳述式遵守下列規則：  
  
-   CREATE GLOBAL CUBE 陳述式會自動將所有命令 (例如導出量值或動作) 複製到本機 Cube。 如果命令包含明確參考父 Cube 的「多維度運算式」(MDX) 運算式，本機 Cube 就無法執行該命令。 若要避免這個問題，請在定義命令的 MDX 運算式時使用 **CURRENTCUBE** 關鍵字。 參考 MDX 運算式內的 cube 時， **CURRENTCUBE** 關鍵字會使用目前的 cube 內容。  
  
-   從本機 Cube 檔案中現有的全域 Cube 所建立的全域 Cube，無法儲存在相同的本機 Cube 檔案。 例如，您建立了一個名稱為 SalesLocal1 的全域 Cube，並將此 Cube 儲存到 C:\SalesLocal.cub 檔案。 然後連接到 C:\SalesLocal.cub 檔案並建立第二個名稱為 SalesLocal2 的全域 Cube。 如果您現在嘗試將 SalesLocal2 全域 Cube 儲存到 C:\SalesLocal.cub 檔案，會收到錯誤。 但是，您可以將 SalesLocal2 全域 Cube 儲存到不同的本機 Cube 檔案。  
  
-   全域 Cube 不支援相異計數量值。 因為包含相異計數量值的 Cube 無法加總，所以 CREATE GLOBAL CUBE 陳述式不支援建立或使用相異計數量值。  
  
-   在本機 Cube 中加入量值時，至少也要包括一個與所加入量值相關的維度。  
  
-   在本機 Cube 中加入父子式階層時，將會忽略父子式階層上的層級和篩選，而且會包含整個父子式階層。  
  
-   本機 Cube 中不支援成員屬性。  
  
-   您不能從檢視方塊建立本機 Cube。  
  
-   在本機 Cube 中包含局部加總量值時，適用下列規則：  
  
    -   如果所加入之量值的 AggregateFunction 屬性為 ByAccount，就必須包含帳戶維度。  
  
    -   如果所加入之量值的 AggregateFunction 屬性為 FirstChild、LastChild、FirstNonEmpty、LastNonEmpty 或 AverageOfChildren，就必須包含整個時間維度。  
  
-   資料採礦維度不能加入至本機 Cube。  
  
-   參考維度已具體化，並以一般維度形式加入。  
  
-   包含多對多維度時，適用下列規則：  
  
    -   必須加入整個多對多維度。  
  
    -   必須加入中繼量值群組。  
  
    -   必須完整加入涉及多對多關係的兩個量值群組共同的所有維度。  
  
 以下範例示範建立本機、保存版本的 Adventure Works Cube，其中只包含 Reseller Sales Amount 量值、Reseller 維度和 Date 維度。  
  
```  
CREATE GLOBAL CUBE [LocalReseller]  
   Storage 'C:\LocalAWReseller1.cub'  
   FROM [Adventure Works]  
   (  
      MEASURE  [Adventure Works].[Reseller Sales Amount],  
      DIMENSION [Adventure Works].[Reseller],  
      DIMENSION [Adventure Works].[Date]  
   )  
```  
  
 以下範例示範建立本機 Cube 時的切割。 建立的全域 Cube 是以 Adventure Works Cube 為基礎，以 Fiscal Year 層級的 2005 成員垂直切割，並以 Fiscal Year 和 Month 層級水平切割。  
  
```  
CREATE GLOBAL CUBE [LocalReseller]  
   Storage 'C:\LocalAWReseller2.cub'  
   FROM [Adventure Works]  
   (  
      MEASURE  [Adventure Works].[Reseller Sales Amount],  
      DIMENSION [Adventure Works].[Reseller],  
      DIMENSION [Adventure Works].[Date]  
      (  
LEVEL [Fiscal Year],  
LEVEL [Month],  
MEMBER [Date].[Fiscal].[Fiscal Year].&[2005]  
      )  
   )  
```  
  
## <a name="see-also"></a>另請參閱  
 [Mdx 資料定義語句 &#40;MDX&#41;](../mdx/mdx-data-definition-statements-mdx.md)   
 [CREATE SESSION CUBE 語句 &#40;MDX&#41;](../mdx/mdx-data-definition-create-session-cube.md)  
  
  
