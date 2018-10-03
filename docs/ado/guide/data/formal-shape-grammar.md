---
title: 正式 Shape 文法 |Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 3b26eaeb804f8d92a7122814641cadf5889b77b8
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47789266"
---
# <a name="formal-shape-grammar"></a>正式 Shape 文法
這是用於建立任何圖形命令的正式文法：  
  
-   必要的文法條款會以角括弧 ("<>") 分隔的文字字串。  
  
-   選擇性的詞彙是以方括號 ("[]") 分隔。  
  
-   替代項目會以斜線 ("&#124;")。  
  
-   重複的替代項目會以省略符號 （"..."）。  
  
-   *Alpha*表示英文字母的字串。  
  
-   *數字*表示數字的字串。  
  
-   *Unicode 數字*表示 unicode 數字的字串。  
  
 所有其他的詞彙是常值。  
  
|詞彙|定義|  
|----------|----------------|  
|\<shape-command>|SHAPE [\<table-exp> [[AS] \<alias>]][\<shape-action>]|  
|\<table-exp>|{\<提供者命令文字 >}&#124;<br /><br /> (\<shape 命令 >)&#124;<br /><br /> 資料表\<加上引號名稱 >&#124;<br /><br /> \<加上引號名稱 >|  
|\<shape-action>|附加\<別名欄位清單 >&#124;<br /><br /> 計算\<別名欄位清單 > [BY\<欄位清單 >]|  
|\<aliased-field-list>|\<別名欄位 > [，\<別名欄位...>]|  
|\<別名欄位 >|\<field-exp> [[AS] \<alias>]|  
|\<field-exp>|(\<關聯 exp >)&#124;<br /><br /> \<計算 exp >&#124;<br /><br /> \<彙總 exp >&#124;<br /><br /> \<new-exp>|  
|<relation_exp>|\<資料表 exp > [[AS]\<別名 >]<br /><br /> 有關\<關聯條件清單 >|  
|\<relation-cond-list>|\<關聯條件 > [，\<關聯條件 >...]|  
|\<關聯條件 >|\<欄位名稱 > TO\<子 ref >|  
|\<child-ref>|\<欄位名稱 >&#124;<br /><br /> 參數\<param ref >|  
|\<param-ref>|\<number>|  
|\<field-list>|\<欄位名稱 > [，\<欄位名稱 >]|  
|\<aggregate-exp>|SUM (\<限定欄位名稱 >)&#124;<br /><br /> AVG (\<限定欄位名稱 >)&#124;<br /><br /> 最小值 (\<限定欄位名稱 >)&#124;<br /><br /> 最大值 (\<限定欄位名稱 >)&#124;<br /><br /> 計數 (\<限定別名 > &#124; \<限定名稱 >)&#124;<br /><br /> Stdev 函數 (\<限定欄位名稱 >)&#124;<br /><br /> 任何 (\<限定欄位名稱 >)|  
|\<calculated-exp>|CALC(\<expression>)|  
|\<qualified-field-name>|\<alias>.[\<alias>...]\<field-name>|  
|\<別名 >|\<加上引號名稱 >|  
|\<field-name>|\<加上引號名稱 > [[AS]\<別名 >]|  
|\<加上引號名稱 >|"\<string>" &#124;<br /><br /> '\<字串 >'&#124;<br /><br /> [\<string>] &#124;<br /><br /> \<名稱 >|  
|\<qualified-name>|alias[.alias...]|  
|\<名稱 >|alpha [alpha&#124;數字&#124;_ &#124; # &#124; : &#124; ...]|  
|\<number>|數字 [數字...]|  
|\<new-exp>|新\<欄位類型 > [(\<數字 > [，\<數目 >])]|  
|\<field-type>|OLE DB 或 ADO 資料類型。|  
|\<string>|unicode 字元 [unicode 字元...]|  
|\<expression>|Visual Basic 應用程式其運算元都是相同的資料列中的其他非計算資料行的運算式。|  
  
## <a name="see-also"></a>另請參閱  
 [存取階層式資料錄集中的資料列](../../../ado/guide/data/accessing-rows-in-a-hierarchical-recordset.md)   
 [資料成形概觀](../../../ado/guide/data/data-shaping-overview.md)   
 [資料成形所需的提供者](../../../ado/guide/data/required-providers-for-data-shaping.md)   
 [Shape APPEND 子句](../../../ado/guide/data/shape-append-clause.md)   
 [一般 shape 命令](../../../ado/guide/data/shape-commands-in-general.md)   
 [Shape COMPUTE 子句](../../../ado/guide/data/shape-compute-clause.md)   
 [Visual Basic for Applications 函式](../../../ado/guide/data/visual-basic-for-applications-functions.md)
