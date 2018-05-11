---
title: 使用 Cube 回寫 (MDX) |Microsoft 文件
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: mdx
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 33fb0be296e6d8397e431bbccc7da86e23418be5
ms.sourcegitcommit: 38f8824abb6760a9dc6953f10a6c91f97fa48432
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/10/2018
---
# <a name="mdx-data-modification---using-cube-writebacks"></a>MDX 資料修改為使用 Cube 回寫
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  您可以使用 [UPDATE CUBE](../../../mdx/mdx-data-manipulation-update-cube.md) 陳述式更新 Cube。 您可以使用此陳述式，來更新具有特定值的 Tuple。 若要有效地使用 UPDATE CUBE 陳述式更新 Cube，您必須了解陳述式的語法、可能發生的錯誤狀況，以及更新在 Cube 上所會產生的影響。  
  
## <a name="update-cube-statement-syntax"></a>UPDATE CUBE 陳述式語法  
 以下語法描述 UPDATE CUBE 陳述式：  
  
```  
UPDATE [CUBE] <Cube_Name> SET <tuple>.VALUE = <value> [,<tuple>.VALUE = <value>...]  
 [ USE_EQUAL_ALLOCATION | USE_EQUAL_INCREMENT |  
  USE_WEIGHTED_ALLOCATION [BY <weight value_expression>] |  
  USE_WEIGHTED_INCREMENT [BY <weight value_expression>] ]   
```  
  
 如果未為 Tuple 指定完整的一組座標，未指定的座標將會使用階層的預設成員。 識別的 Tuple 必須參考以 [Sum](../../../mdx/sum-mdx.md) 函數彙總的資料格，而且絕不能使用導出成員作為資料格的其中一個座標。  
  
 您可以將 UPDATE CUBE 陳述式視為一個副程式，其會對不可部份完成的資料格產生一系列的個別回寫作業。 然後，所有個別的回寫作業就會積存到指定總和。  
  
> [!NOTE]  
>  當更新的資料格未重疊時， **Update Isolation Level** 連接字串屬性可用來增強 UPDATE CUBE 的效能。 如需詳細資訊，請參閱 <xref:Microsoft.AnalysisServices.AdomdClient.AdomdConnection.ConnectionString%2A>。  
  
## <a name="example"></a>範例  
 您可以在 Adventure Works Cube 中，使用銷售目標量值群組來測試 UPDATE CUBE。 此量值群組包含 SUM 彙總的量值，這是 UPDATE CUBE 的需求。  
  
1.  啟用 Adventure Works 資料庫中銷售目標量值群組的回寫功能。 在 Management Studio 中，以滑鼠右鍵按一下量值群組，指向 [回寫選項]，然後選擇 [啟用回寫]。  
  
     您應該會在 [回寫] 資料夾中看到新的回寫資料表。 資料表名稱為 WriteTable_Fact Sales Quota。  
  
2.  開啟 MDX 查詢視窗。 執行下列 SELECT 陳述式以檢視原始值：  
  
    ```  
    SELECT [Measures].[Sales Amount Quota] on 0 ,  
    [Employee].[Employee Department].[Title].&[Sales Representative].children on 1  
    FROM [Adventure Works]  
  
    ```  
  
     您應該會看到每個銷售代表的銷售量配額。  
  
3.  執行 UPDATE CUBE 陳述式以回寫新值。 在此範例中，我們將銷售量配額設為 0。 由於新值為 0，因此請勿指定配置方法。  
  
    ```  
    UPDATE CUBE [Adventure Works]   
    SET ([Measures].[Sales Amount Quota], [Employee].[Employee Department].[Department].&[Sales]) = 0  
  
    ```  
  
4.  重新執行 SELECT 陳述式。 您現在應該會看到配額為零。  
  
 回寫值受限於目前的工作階段。 若要跨使用者和工作階段持續使用此值，請處理回寫資料表。 在 Management Studio 中，以滑鼠右鍵按一下 WriteTable_Fact Sales Quota，然後選擇 [處理]。  
  
 若要指定配置方法，新值必須大於零。 在此範例中，銷售量配額的新值為兩百萬，而配置方法會將此數量分配給所有銷售代表。  
  
```  
UPDATE CUBE [Adventure Works]   
SET ([Measures].[Sales Amount Quota], [Employee].[Employee Department].[Department].&[Sales]) = 2000000   
USE_EQUAL_ALLOCATION  
```  
  
## <a name="error-conditions"></a>錯誤狀況  
 下表描述會導致回寫失敗及錯誤結果的狀況。  
  
|錯誤狀況|結果|  
|---------------------|------------|  
|更新包括相同維度但未能同時存在的成員。|更新將會失敗。 Cube 空間將不會包含參考資料格。|  
|更新包括來源為不帶正負號類型的量值。|更新將會失敗。 遞增需要量值能夠接受負值。|  
|更新包括非彙總總和的量值。|引發錯誤。|  
|嘗試在 Subcube 進行更新。|引發錯誤。|  
  
## <a name="affect-of-cube-changes"></a>Cube 變更的影響  
 以下變更將不會影響到回寫：  
  
-   處理 Cube、Cube 的量值群組，或 Cube 的維度。  
  
-   將屬性增加到任何維度。  
  
-   增加新的維度。  
  
-   刪除不包含回寫的維度。  
  
-   新增、修改或移除階層。  
  
-   增加新的量值。  
  
 不移除回寫資料，就無法做出以下變更：  
  
-   如果回寫中包含屬性在內，但要刪除屬性或其屬性階層。 這包括明確地移除屬性或其屬性階層，或移除屬性的父維度。  
  
-   刪除回寫中包含的量值。  
  
-   新增一個屬性，而回寫中包含的維度沒有 [(全部)] 層級。  
  
-   變更回寫中包含之維度的維度資料粒度。  
  
## <a name="see-also"></a>另請參閱  
 [修改資料 & #40;MDX & #41;](../../../analysis-services/multidimensional-models/mdx/mdx-data-modification-modifying-data.md)  
  
  
