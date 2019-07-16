---
title: ALTER CUBE 陳述式 (MDX) |Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 750f8ae7a1b9275bdab734a15134d255916e7d44
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/15/2019
ms.locfileid: "68098519"
---
# <a name="mdx-data-definition---alter-cube"></a>MDX 資料定義 - ALTER CUBE


  改變指定 Cube 的結構，通常用來支援維度回寫。 如需應用程式中使用回寫的詳細資訊，請參閱此部落格文章：[建立回寫應用程式與 Analysis Services （部落格）](https://go.microsoft.com/fwlink/?LinkId=394977)  
  
 請注意，並行維度回寫可能會導致死結，其中第一個回寫由於第二個回寫保留共用鎖定而無法認可。 在此情況下，雖然不會產生錯誤，但是也無法進行作業。 最後，這兩個回寫會逾時，而系統會回復變更。  
  
## <a name="syntax"></a>語法  
  
```  
  
ALTER CUBE  
      Cube_Name | CURRENTCUBE  
      <alter clause>   
            [ < alter clause> ...n]  
  
< alter clause> ::=   
   <create dimension member clause>   
  | <remove dimension member clause>  
  | <move dimension member clause>   
    | <update clause>   
    | <create cell calculation clause>  
  
<create dimension member clause> ::=  
CREATE DIMENSION MEMBER [ParentName.]MemberName  
    , [[KEY = Key_Value]   
    | [Property_Name = Property_Value[, ...n]]  
  
<dropping clause>::=  
DROP   
      DIMENSION MEMBER Member_Name   
            Member_Name ...n ]   
      [WITH DESCENDANTS]  
      | [ SESSION ] [ CALCULATED ] MEMBER Member_Name   
                  [ ,Member_Name,...n ]   
    | SET Set_Name  
                  [ ,Set_Name,...n ]   
    | [ SESSION ] CELL CALCULATION CellCalc_Name  
                  [ ,CellCalc_Name,...n ]   
    | ACTION Action_Name  
  
<move dimension member clause> ::=  
MOVE DIMENSION MEMBER MemberName  
        [, SKIPPED_LEVELS = Unsigned_Integer]   
      [WITH DESCENDANTS]  
    UNDER ParentName      
  
<update clause> ::=  
UPDATE   
    CUSTOM ROLLUP FOR MEMBER MemberName  
      [,MemberName, ...n] AS MDX_Expression  
   | DIMENSION Dimension_Name | Hierarchy_Name  
      , DEFAULT_MEMBER = MDX_Expression  
   | DIMENSION MEMBER MemberName AS  
   [MDX_Expression]  
   [Property_Name = Property_Value[, ...n]]  
  
<create cell calculation clause>::=  
CELL CALCULATION Calculation_Name   
   FOR Set_Expression AS MDX_Expression   
            [ [ CONDITION = 'Logical_Expression' ]   
    | [ DISABLED = { TRUE | FALSE } ]   
    | [ DESCRIPTION =String ]   
    | [ CALCULATION_PASS_NUMBER = Integer]   
    | [ CALCULATION_PASS_DEPTH = Integer]   
    | [ SOLVE_ORDER = Integer]   
    | [ Calculation_Name= Scalar_Expression ], ...n]  
```  
  
## <a name="creating-a-dimension-member"></a>建立維度成員  
 將新資料列新增至基礎維度資料表。  
  
### <a name="arguments"></a>引數  
 *ParentName*  
 提供新維度成員之父系名稱的有效字串運算式，若維度成員是建立於根節點，便無法提供。  
  
 *MemberName*  
 提供成員名稱的有效字串運算式。  
  
 *Key_Value*  
 定義新維度成員之索引鍵值的有效純量運算式。  
  
 *Property_Name*  
 代表成員屬性的有效多維度運算式 (MDX) 識別碼。  
  
 *Property_Value*  
 定義導出成員屬性值的有效多維度運算式 (MDX) 純量運算式。  
  
## <a name="dropping-a-dimension-member"></a>卸除維度成員  
 從可寫入的維度卸除維度成員，會將成員及其對應的資料列從基礎維度資料表刪除。  
  
### <a name="arguments"></a>引數  
 *Cube_Name*  
 提供 Cube 名稱的有效字串運算式。  
  
 *Member_Name*  
 提供成員名稱或成員索引鍵的有效字串運算式。  
  
### <a name="remarks"></a>備註  
 如果沒有使用 WITH DESCENDANTS 子句，已卸除之成員的子系會成為其父系的子系。 如果使用 WITH DESCENDANTS 子句，同時也會卸除維度資料表中的所有下階及其資料列。  
  
> [!NOTE]  
>  如需卸除導出的成員、 命名集、 動作和資料格計算，請參閱[DROP MEMBER 陳述式&#40;MDX&#41;](../mdx/mdx-data-definition-drop-member.md)， [DROP SET 陳述式&#40;MDX&#41;](../mdx/mdx-data-definition-drop-set.md)，[DROP ACTION 陳述式&#40;MDX&#41;](../mdx/mdx-data-definition-drop-action.md)，以及[DROP CELL CALCULATION 陳述式&#40;MDX&#41;](../mdx/mdx-data-definition-drop-cell-calculation.md)。  
  
## <a name="updating-the-default-dimension-member"></a>更新預設維度成員  
 這個子句會更新 Cube 的預設成員，在 MDX 計算指令碼中使用可定義預設成員。 您可以指定資料庫維度、Cube 維度或使用者登入的預設成員。 在工作階段期間，也可以變更預設成員。  
  
### <a name="arguments"></a>引數  
 *Dimension_Name*  
 提供維度名稱的有效字串。  
  
 *MDX_Expression*  
 傳回單一成員的有效 MDX 運算式。  
  
### <a name="remarks"></a>備註  
 指定的 MDX 運算式可以是靜態或動態。  
  
## <a name="moving-a-dimension-member"></a>移動維度成員  
 修改基礎維度資料表中的資料列。  
  
### <a name="arguments"></a>引數  
 *ParentName*  
 為所移動的維度成員，提供新父系名稱的有效字串運算式。  
  
 *MemberName*  
 提供成員名稱的有效字串運算式。  
  
 Unsigned_*整數*  
 指定要略過之層級數目的有效數字。  
  
 如果指定了 WITH DESCENDANTS 子句，會移動整個樹狀結構。 如果沒有指定 WITH DESCENDANTS 子句，已移動之父系的子系會成為已移動之成員其父系的子系。 移動的作用只是更新基礎維度資料表中的父索引鍵資料行值。  
  
## <a name="updating-a-dimension-member"></a>更新維度成員  
 UPDATE DIMENSION MEMBER 子句讓您能修改成員屬性，以及與成員相關聯的自訂成員公式。  
  
### <a name="arguments"></a>引數  
 *MemberName*  
 提供成員名稱的有效字串運算式。  
  
 *MDX_Expression*  
 傳回單一成員的有效 MDX 運算式。  
  
 *Property_Value*  
 定義導出成員屬性值的有效 MDX 純量運算式。  
  
## <a name="creating-a-cell-calculation"></a>建立資料格計算  
 如需建立使用 ALTER CUBE 陳述式資料格計算的詳細資訊，請參閱[DROP CELL CALCULATION 陳述式&#40;MDX&#41;](../mdx/mdx-data-definition-drop-cell-calculation.md)。  
  
## <a name="see-also"></a>另請參閱  
 [MDX 資料定義陳述式&#40;MDX&#41;](../mdx/mdx-data-definition-statements-mdx.md)  
  
  
