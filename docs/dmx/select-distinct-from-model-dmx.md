---
title: SELECT DISTINCT FROM&lt;模型&gt;(DMX) |Microsoft Docs
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 5906dc6d964603576831a5c7009cd0224f0ffb08
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/15/2019
ms.locfileid: "67928441"
---
# <a name="select-distinct-from-ltmodel-gt-dmx"></a>SELECT DISTINCT FROM&lt;模型&gt;(DMX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  傳回模型中選取之資料行的所有可能狀態。 傳回的值會隨著指定的資料行包含離散值、離散化的數值，還是連續數值而有所不同。  
  
## <a name="syntax"></a>語法  
  
```  
  
SELECT [FLATTENED] DISTINCT [TOP <n>] <expression list> FROM <model>   
[WHERE <condition list>][ORDER BY <expression>]  
```  
  
## <a name="arguments"></a>引數  
 *n*  
 選擇性。 指定要傳回多少資料列的整數。  
  
 *運算式清單*  
 相關之資料行識別碼 (從模型衍生) 或運算式的逗號分隔清單。  
  
 *model*  
 模型識別碼。  
  
 *條件清單*  
 限制從資料行清單傳回之值的條件。  
  
 *expression*  
 選擇性。 傳回純量值的運算式。  
  
## <a name="remarks"></a>備註  
 **SELECT DISTINCT FROM**陳述式僅適用於具有單一資料行或一組相關的資料行。 這個子句不能配合一組未關聯的資料行使用。  
  
 **SELECT DISTINCT FROM**陳述式可讓您直接參考巢狀資料表內部的資料行。 例如:  
  
```  
<model>.<table column reference>.<column reference>  
```  
  
 結果**SELECT DISTINCT FROM\<模型 >** 陳述式而有所不同，視資料行類型而定。 下表說明支援的資料行類型與陳述式的輸出。  
  
|資料行類型|Output|  
|-----------------|------------|  
|Discrete|資料行中的唯一值。|  
|Discretized|資料行中每個分隔式值區的中點。|  
|Continuous|資料行中之值的中點。|  
  
## <a name="discrete-column-example"></a>分隔資料行範例  
 下列程式碼範例根據`[TM Decision Tree]`您在中建立的模型[83c8-9df5dddfeb9c"&gt;basic Data Mining Tutorial&lt](https://msdn.microsoft.com/library/6602edb6-d160-43fb-83c8-9df5dddfeb9c)。 此查詢會傳回離散資料行 `Gender` 中存在的唯一值。  
  
```  
SELECT DISTINCT [Gender]  
FROM [TM Decision Tree]  
```  
  
 範例結果：  
  
|Gender|  
|------------|  
||  
|F|  
|M|  
  
 對於包含離散值的資料行，結果永遠包含「遺漏」狀態，其顯示為 Null 值。  
  
## <a name="continuous-column-example"></a>連續資料行範例  
 以下程式碼範例會傳回資料行中所有值的中點、最小時限與最大時限。  
  
```  
SELECT DISTINCT [Age] AS [Midpoint Age],   
    RangeMin([Age]) AS [Minimum Age],   
    RangeMax([Age]) AS [Maximum Age]  
FROM [TM Decision Tree]  
```  
  
 範例結果：  
  
|Midpoint Age|Minimum Age|Maximum Age|  
|------------------|-----------------|-----------------|  
||||  
|62|26|97|  
  
 此查詢也會查詢 Null 值的單一資料列，來表示遺漏值。  
  
## <a name="discretized-column-example"></a>離散化資料行範例  
 下列程式碼範例會針對演算法建立的每個值區，傳回 [`Yearly Income]` 資料行的中點、最大與最小值。 若要重新產生此範例的結果，您必須建立與 `[Targeted Mailing]` 相同的新採礦結構。 在精靈中，變更的內容型別`Yearly Income`資料行**連續**要**Discretized**。  
  
> [!NOTE]  
>  您也可以變更在＜基本採礦教學課程＞中建立的採礦模型，以便將採礦結構資料行 [`Yearly Income]` 離散化。 如需如何執行這項操作的資訊，請參閱[變更採礦模型中的資料行的離散化](../analysis-services/data-mining/change-the-discretization-of-a-column-in-a-mining-model.md)。 不過，當您變更資料行的離散化時，將會強制重新處理採礦結構，這樣會變更您使用該結構建立之其他模型的結果。  
  
```  
SELECT DISTINCT [Yearly Income] AS [Bucket Average],   
    RangeMin([Yearly Income]) AS [Bucket Minimum],   
    RangeMax([Yearly Income]) AS [Bucket Maximum]  
FROM [TM Decision Tree]  
```  
  
 範例結果：  
  
|Bucket Average|Bucket Minimum|Bucket Maximum|  
|--------------------|--------------------|--------------------|  
||||  
|24610.7|10000|39221.41|  
|55115.73|39221.41|71010.05|  
|84821.54|71010.05|98633.04|  
|111633.9|98633.04|124634.7|  
|147317.4|124634.7|170000|  
  
 您可以看到，[Yearly Income] 資料行的值已經離散化為 5 個值區，加上 Null 值的一個額外資料列，用以表示遺漏值。  
  
 結果中的小數位數取決於您用於查詢的用戶端。 小數位數在此處已捨入為兩個小數位數，可用於簡化，以及反映顯示在 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] 中的值。  
  
 例如，如果您使用決策樹檢視器瀏覽模型，然後按一下包含以收入分組之客戶的節點，下列節點屬性就會顯示在工具提示中：  
  
 Age > = 69 和每年的收益 < 39221.41  
  
> [!NOTE]  
>  最小值區的最小值與最大值區的最大值剛好分別是最高與最低的觀察值。 系統會假設超出此觀察範圍的任何值都屬於最小和最大值區。  
  
## <a name="see-also"></a>另請參閱  
 [SELECT &#40;DMX&#41;](../dmx/select-dmx.md)   
 [資料採礦延伸模組&#40;DMX&#41;資料操作陳述式](../dmx/dmx-statements-data-manipulation.md)   
 [資料採礦延伸模組 &#40;DMX&#41; 陳述式參考](../dmx/data-mining-extensions-dmx-statements.md)  
  
  
