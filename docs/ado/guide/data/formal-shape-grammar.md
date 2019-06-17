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
manager: jroth
ms.openlocfilehash: 0af2421a0d1f80922560be556062c89074c21838
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "66701995"
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
|\<table-exp>|{\<provider-command-text>} &#124;<br /><br /> (\<shape-command>) &#124;<br /><br /> 資料表\<加上引號名稱 >&#124;<br /><br /> \<quoted-name>|  
|\<shape-action>|APPEND \<aliased-field-list> &#124;<br /><br /> 計算\<別名欄位清單 > [BY\<欄位清單 >]|  
|\<aliased-field-list>|\<aliased-field> [, \<aliased-field...>]|  
|\<aliased-field>|\<field-exp> [[AS] \<alias>]|  
|\<field-exp>|(\<relation-exp>) &#124;<br /><br /> \<calculated-exp> &#124;<br /><br /> \<aggregate-exp> &#124;<br /><br /> \<new-exp>|  
|<relation_exp>|\<table-exp> [[AS] \<alias>]<br /><br /> 有關\<關聯條件清單 >|  
|\<relation-cond-list>|\<relation-cond> [, \<relation-cond>...]|  
|\<relation-cond>|\<欄位名稱 > TO\<子 ref >|  
|\<child-ref>|\<field-name> &#124;<br /><br /> 參數\<param ref >|  
|\<param-ref>|\<number>|  
|\<field-list>|\<field-name> [, \<field-name>]|  
|\<aggregate-exp>|SUM(\<qualified-field-name>) &#124;<br /><br /> AVG(\<qualified-field-name>) &#124;<br /><br /> MIN(\<qualified-field-name>) &#124;<br /><br /> MAX(\<qualified-field-name>) &#124;<br /><br /> COUNT(\<qualified-alias> &#124; \<qualified-name>) &#124;<br /><br /> STDEV(\<qualified-field-name>) &#124;<br /><br /> ANY(\<qualified-field-name>)|  
|\<calculated-exp>|CALC(\<expression>)|  
|\<qualified-field-name>|\<alias>.[\<alias>...]\<field-name>|  
|\<alias>|\<quoted-name>|  
|\<field-name>|\<quoted-name> [[AS] \<alias>]|  
|\<quoted-name>|"\<string>" &#124;<br /><br /> '\<string>' &#124;<br /><br /> [\<string>] &#124;<br /><br /> \<name>|  
|\<qualified-name>|alias[.alias...]|  
|\<name>|alpha [ alpha &#124; digit &#124; _ &#124; # &#124; : &#124; ...]|  
|\<number>|digit [digit...]|  
|\<new-exp>|NEW \<field-type> [(\<number> [, \<number>])]|  
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
