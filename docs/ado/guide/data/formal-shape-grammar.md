---
title: 正式圖形文法 |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- shape commands [ADO], shape grammar
- data shaping [ADO], shape grammar
ms.assetid: ea691475-0f03-4abe-a785-b77e77712d1d
author: rothja
ms.author: jroth
ms.openlocfilehash: ce65f6961502a5bfe43278e4a29a11c4210d4af8
ms.sourcegitcommit: 6037fb1f1a5ddd933017029eda5f5c281939100c
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/04/2020
ms.locfileid: "82758254"
---
# <a name="formal-shape-grammar"></a>正式 Shape 文法
這是用來建立任何圖形命令的正式文法：  
  
-   必要的語法詞彙是以角括弧（"<>"）分隔的文字字串。  
  
-   選擇性詞彙會以方括弧（"[]"）分隔。  
  
-   替代方案會以 virgule （"&#124;"）來表示。  
  
-   重複的替代專案會以省略號（"..."）來表示。  
  
-   *Alpha*表示字母順序的字串。  
  
-   *數位*表示數位的字串。  
  
-   *Unicode 數位*表示 unicode 數位的字串。  
  
 所有其他詞彙都是常值。  
  
|詞彙|定義|  
|----------|----------------|  
|\<圖形-命令>|SHAPE [ \< 資料表-exp> [[AS] \< alias>]] [ \< 圖形動作>]|  
|\<資料表-exp>|{ \< provider-命令-text>} &#124;<br /><br /> （ \< 圖形-命令>） &#124;<br /><br /> 以 \< 引號括住的名稱> &#124;<br /><br /> \<加上引號的名稱>|  
|\<圖形-動作>|附加 \< 別名欄位清單> &#124;<br /><br /> 計算 \< 別名-欄位清單> [依 \< 欄位清單>]|  
|\<別名-欄位清單>|\<別名-欄位> [， \< 別名欄位 ... >]|  
|\<別名-欄位>|\<欄位 exp> [[AS] \< alias>]|  
|\<欄位-exp>|（ \< 關聯性-exp>） &#124;<br /><br /> \<計算-exp> &#124;<br /><br /> \<匯總-exp> &#124;<br /><br /> \<新的-exp>|  
|<relation_exp>|\<資料表-exp> [[AS] \< alias>]<br /><br /> 關聯 \< 關係-導線清單>|  
|\<關聯性-導線清單>|\<關聯性> [， \< 關聯-導線> ...]|  
|\<關係-導線>|\<> \< 子參考> 的功能變數名稱|  
|\<子參考>|\<功能變數名稱> &#124;<br /><br /> 參數 \< param-ref>|  
|\<參數-ref>|\<> 數目|  
|\<欄位清單>|\<功能變數名稱> [， \< 功能變數名稱稱>]|  
|\<匯總-exp>|SUM （ \< 限定功能變數名稱>） &#124;<br /><br /> 平均（ \< 限定功能變數名稱>） &#124;<br /><br /> 最小值（ \< 限定功能變數名稱>） &#124;<br /><br /> 最大值（ \< 限定功能變數名稱>） &#124;<br /><br /> 計數（ \< 限定別名> &#124; \< 限定名稱>） &#124;<br /><br /> STDEV （ \< 限定功能變數名稱>） &#124;<br /><br /> ANY （ \< 限定功能變數名稱>）|  
|\<計算-exp>|CALC （ \< expression>）|  
|\<合格功能變數名稱>|\<別名>。[ \< alias> ...] \<功能變數名稱>|  
|\<別名>|\<加上引號的名稱>|  
|\<功能變數名稱>|\<加上引號的名稱> [[AS] \< alias>]|  
|\<加上引號的名稱>|" \< string>" &#124;<br /><br /> ' \< string> ' &#124;<br /><br /> [ \< string>] &#124;<br /><br /> \<名稱>|  
|\<限定名稱>|alias [. alias ...]|  
|\<名稱>|Alpha [Alpha &#124; 數位 &#124; _ &#124; # &#124;： &#124; ...]|  
|\<> 數目|數位 [數位 ...]|  
|\<新的-exp>|新 \< 的欄位類型> [（ \< 數位> [， \< 數位>]）]|  
|\<欄位類型>|OLE DB 或 ADO 資料類型。|  
|\<字串>|unicode-char [unicode-char ...]|  
|\<運算式>|Visual Basic for Applications 運算式，其運算元為相同資料列中的其他非 CALC 資料行。|  
  
## <a name="see-also"></a>另請參閱  
 [存取階層式記錄集中的資料列](../../../ado/guide/data/accessing-rows-in-a-hierarchical-recordset.md)   
 [資料成形總覽](../../../ado/guide/data/data-shaping-overview.md)   
 [資料成形所需的提供者](../../../ado/guide/data/required-providers-for-data-shaping.md)   
 [Shape APPEND 子句](../../../ado/guide/data/shape-append-clause.md)   
 [一般的圖形命令](../../../ado/guide/data/shape-commands-in-general.md)   
 [Shape COMPUTE 子句](../../../ado/guide/data/shape-compute-clause.md)   
 [Visual Basic for Applications 函式](../../../ado/guide/data/visual-basic-for-applications-functions.md)
