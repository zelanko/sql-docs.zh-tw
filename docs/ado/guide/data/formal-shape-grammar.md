---
title: "型式圖形文法 |Microsoft 文件"
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: ado
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- shape commands [ADO], shape grammar
- data shaping [ADO], shape grammar
ms.assetid: ea691475-0f03-4abe-a785-b77e77712d1d
caps.latest.revision: 
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: f9eb99feba381701f7e590add3906cd0285b2720
ms.sourcegitcommit: acab4bcab1385d645fafe2925130f102e114f122
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/09/2018
---
# <a name="formal-shape-grammar"></a>型式圖形文法
這是建立任何圖形命令的正式文法：  
  
-   必要的文法條款將會以角括弧 ("<>") 分隔的文字字串。  
  
-   選擇性的詞彙是以方括號 ("[]") 分隔。  
  
-   替代方案以斜線 ("&#124;")。  
  
-   重複的替代項目會以省略符號 （"…"）。  
  
-   *Alpha*表示英文字母的字串。  
  
-   *數字*表示數字的字串。  
  
-   *Unicode 數字*表示 unicode 數字的字串。  
  
 所有其他的詞彙是常值。  
  
|詞彙|定義|  
|----------|----------------|  
|\<shape-command>|SHAPE [\<table-exp> [[AS] \<alias>]][\<shape-action>]|  
|\<table-exp>|{\<provider-command-text>} &#124;<br /><br /> (\<shape 命令 >) &#124;<br /><br /> 資料表\<加上引號名稱 > &#124;<br /><br /> \<quoted-name>|  
|\<shape-action>|附加\<別名欄位清單 > &#124;<br /><br /> 計算\<別名欄位清單 > [依\<欄位清單 >]|  
|\<aliased-field-list>|\<aliased-field> [, \<aliased-field...>]|  
|\<aliased-field>|\<field-exp> [[AS] \<alias>]|  
|\<field-exp>|(\<關聯 exp >) &#124;<br /><br /> \<calculated-exp> &#124;<br /><br /> \<aggregate-exp> &#124;<br /><br /> \<new-exp>|  
|<relation_exp>|\<table-exp> [[AS] \<alias>]<br /><br /> RELATE \<relation-cond-list>|  
|\<relation-cond-list>|\<relation-cond> [, \<relation-cond>...]|  
|\<relation-cond>|\<field-name> TO \<child-ref>|  
|\<child-ref>|\<欄位名稱 > &#124;<br /><br /> PARAMETER \<param-ref>|  
|\<param-ref>|\<number>|  
|\<field-list>|\<field-name> [, \<field-name>]|  
|\<aggregate-exp>|SUM (\<限定欄位名稱 >) &#124;<br /><br /> AVG (\<限定欄位名稱 >) &#124;<br /><br /> MIN (\<限定欄位名稱 >) &#124;<br /><br /> 最大值 (\<限定欄位名稱 >) &#124;<br /><br /> 計數 (\<限定別名 > &#124;\<限定名稱 >) &#124;<br /><br /> STDEV(\<qualified-field-name>) &#124;<br /><br /> ANY(\<qualified-field-name>)|  
|\<calculated-exp>|CALC(\<expression>)|  
|\<qualified-field-name>|\<alias>.[\<alias>...]\<field-name>|  
|\<alias>|\<quoted-name>|  
|\<field-name>|\<加上引號名稱 > [[AS]\<別名 >]|  
|\<quoted-name>|"\<string>" &#124;<br /><br /> '\<string>' &#124;<br /><br /> [\<string>] &#124;<br /><br /> \<name>|  
|\<qualified-name>|alias[.alias...]|  
|\<name>|alpha [alpha &#124; 數字 &#124; _ &#124; # &#124;: &#124;...]|  
|\<number>|digit [digit...]|  
|\<new-exp>|新\<欄位類型 > [(\<數字 > [，\<數目 >])]|  
|\<field-type>|OLE DB 或 ADO 資料類型。|  
|\<string>|unicode 字元 [unicode 字元...]|  
|\<expression>|Visual Basic 中為應用程式的運算元都是相同的資料列中的其他非計算資料行的運算式的。|  
  
## <a name="see-also"></a>另請參閱  
 [存取資料列中的階層式資料錄集](../../../ado/guide/data/accessing-rows-in-a-hierarchical-recordset.md)   
 [資料成形概觀](../../../ado/guide/data/data-shaping-overview.md)   
 [提供者所需的資料成形](../../../ado/guide/data/required-providers-for-data-shaping.md)   
 [圖形 APPEND 子句](../../../ado/guide/data/shape-append-clause.md)   
 [在一般的圖形命令](../../../ado/guide/data/shape-commands-in-general.md)   
 [圖形 COMPUTE 子句](../../../ado/guide/data/shape-compute-clause.md)   
 [Visual Basic for Applications 函式](../../../ado/guide/data/visual-basic-for-applications-functions.md)
