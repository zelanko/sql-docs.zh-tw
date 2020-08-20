---
description: 正式 Shape 文法
title: 正式式圖形文法 |Microsoft Docs
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
ms.openlocfilehash: 6a8d92abc3a1b0d7e6d39ac4149c186c5a2fc2eb
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88453370"
---
# <a name="formal-shape-grammar"></a>正式 Shape 文法
這是建立任何 shape 命令的正式文法：  
  
-   必要的語法詞彙是以角括弧分隔的文字字串 ( "<>" ) 。  
  
-   選用詞彙以方括弧分隔 ( "[]" ) 。  
  
-   替代專案會以 virgule ( "&#124;" ) 表示。  
  
-   重複的替代專案會以省略號 ( "..." ) 表示。  
  
-   *Alpha* 表示以字母順序表示的字串。  
  
-   *數位* 表示數位字串。  
  
-   *Unicode 位數* 表示 unicode 數位的字串。  
  
 所有其他詞彙都是常值。  
  
|詞彙|定義|  
|----------|----------------|  
|\<shape-command>|SHAPE [ \<table-exp> [[AS] \<alias> ]] [ \<shape-action> ]|  
|\<table-exp>|{ \<provider-command-text> } &#124;<br /><br />  (\<shape-command>) &#124;<br /><br /> 資料表 \<quoted-name> &#124;<br /><br /> \<quoted-name>|  
|\<shape-action>|附加 \<aliased-field-list> &#124;<br /><br /> 計算 \<aliased-field-list> [依據 \<field-list> ]|  
|\<aliased-field-list>|\<aliased-field> [, \<aliased-field...>]|  
|\<aliased-field>|\<field-exp> [[AS] \<alias> ]|  
|\<field-exp>| (\<relation-exp>) &#124;<br /><br /> \<calculated-exp> &#124;<br /><br /> \<aggregate-exp> &#124;<br /><br /> \<new-exp>|  
|<relation_exp>|\<table-exp> [[AS] \<alias> ]<br /><br /> 與 \<relation-cond-list>|  
|\<relation-cond-list>|\<relation-cond> [, \<relation-cond>...]|  
|\<relation-cond>|\<field-name> 自 \<child-ref>|  
|\<child-ref>|\<field-name> &#124;<br /><br /> 參數 \<param-ref>|  
|\<param-ref>|\<number>|  
|\<field-list>|\<field-name> [, \<field-name>]|  
|\<aggregate-exp>|SUM (\<qualified-field-name>) &#124;<br /><br /> 平均 (\<qualified-field-name>) &#124;<br /><br /> 最小 (\<qualified-field-name>) &#124;<br /><br /> 最大 (\<qualified-field-name>) &#124;<br /><br /> 計數 (\<qualified-alias> &#124; \<qualified-name>) &#124;<br /><br /> STDEV (\<qualified-field-name>) &#124;<br /><br /> 任何 (\<qualified-field-name>) |  
|\<calculated-exp>|CALC (\<expression>) |  
|\<qualified-field-name>|\<alias>.[\<alias>...]\<field-name>|  
|\<alias>|\<quoted-name>|  
|\<field-name>|\<quoted-name> [[AS] \<alias> ]|  
|\<quoted-name>|" \<string> " &#124;<br /><br /> ' \<string> ' &#124;<br /><br /> [ \<string> ] &#124;<br /><br /> \<name>|  
|\<qualified-name>|別名 [. 別名 ...]|  
|\<name>|Alpha [Alpha &#124; 位數 &#124; _ &#124; # &#124;： &#124; ...]|  
|\<number>|位數 [數位 ...]|  
|\<new-exp>|NEW \<field-type> [ (\<number> [， \<number> ] ) ]|  
|\<field-type>|OLE DB 或 ADO 資料類型。|  
|\<string>|unicode-char [unicode-char ...]|  
|\<expression>|Visual Basic for Applications 運算式，其運算元是相同資料列中的其他非計算資料行。|  
  
## <a name="see-also"></a>另請參閱  
 [存取階層式記錄集中的資料列](../../../ado/guide/data/accessing-rows-in-a-hierarchical-recordset.md)   
 [資料成形總覽](../../../ado/guide/data/data-shaping-overview.md)   
 [資料成形所需的提供者](../../../ado/guide/data/required-providers-for-data-shaping.md)   
 [Shape APPEND 子句](../../../ado/guide/data/shape-append-clause.md)   
 [一般圖形命令](../../../ado/guide/data/shape-commands-in-general.md)   
 [Shape COMPUTE 子句](../../../ado/guide/data/shape-compute-clause.md)   
 [Visual Basic for Applications 函式](../../../ado/guide/data/visual-basic-for-applications-functions.md)
