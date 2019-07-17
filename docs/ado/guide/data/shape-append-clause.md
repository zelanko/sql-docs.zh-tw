---
title: 圖形 APPEND 子句 |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- shape commands [ADO]
- data shaping [ADO], APPEND clause
- append clause [ADO]
ms.assetid: f90fcf55-6b24-401d-94e1-d65bd24bd342
author: MightyPen
ms.author: genemi
ms.openlocfilehash: e09113b42f655a3b94ab3877ff81f2553a363931
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/15/2019
ms.locfileid: "67924186"
---
# <a name="shape-append-clause"></a>Shape APPEND 子句
Shape 命令 APPEND 子句附加的資料行或資料行**資料錄集**。 通常，這些資料行是章節資料行，參考的子系**資料錄集**。  
  
## <a name="syntax"></a>語法  
  
```  
SHAPE [parent-command [[AS] parent-alias]] APPEND column-list  
```  
  
## <a name="description"></a>描述  
 這個子句的部分如下所示：  
  
 *parent-command*  
 零或下列其中之一 (您可以省略*父命令*完全):  
  
-   提供者命令括在大括弧 ("{}")，會傳回**資料錄集**物件。 基礎資料提供者發出的命令和其語法取決於該提供者的需求。 這通常是 SQL 語言，雖然 ADO 不需要任何特定的查詢語言。  
  
-   另一個圖形命令內嵌在括號中。  
  
-   資料表關鍵字，後面加上資料表中的資料提供者的名稱。  
  
 *parent-alias*  
 父代是指的選擇性別名**資料錄集**。  
  
 *column-list*  
 一或多個項目：  
  
-   彙總的資料行。  
  
-   導出資料行。  
  
-   新的資料行，建立使用新的子句。  
  
-   章節資料行。 章節資料行定義為加括號 （"（）"）。 請參閱以下的語法。  
  
```  
SHAPE [parent-command [[AS] parent-alias]]  
   APPEND (child-recordset [ [[AS] child-alias]   
      RELATE parent-column TO child-column | PARAMETER param-number, ... ])  
   [[AS] chapter-alias]   
   [, ... ]  
```  
  
## <a name="remarks"></a>備註  
 *child-recordset*  
 -   提供者命令括在大括弧 ("{}")，會傳回**資料錄集**物件。 基礎資料提供者發出的命令和其語法取決於該提供者的需求。 這通常是 SQL 語言，雖然 ADO 不需要任何特定的查詢語言。  
  
-   另一個圖形命令內嵌在括號中。  
  
-   現有的形狀名稱**資料錄集**。  
  
-   資料表關鍵字，後面加上資料表中的資料提供者的名稱。  
  
 *child-alias*  
 子系的別名**資料錄集**。  
  
 *parent-column*  
 中的資料行**Recordset**所傳回*父命令。*  
  
 *child-column*  
 中的資料行**Recordset**由*子命令*。  
  
 *param-number*  
 請參閱[參數化命令的作業](../../../ado/guide/data/operation-of-parameterized-commands.md)。  
  
 *chapter-alias*  
 參考附加至父代的章節資料行的別名。  
  
> [!NOTE]
>  *「 父資料行*TO*子資料行"* 子句其實是一個清單，其中定義每個關聯性以逗號分隔  
  
> [!NOTE]
>  子句之後附加關鍵字其實是一個清單，其中每個子句會以逗號分隔，而會定義要附加至父代的另一個資料行。  
  
## <a name="remarks"></a>備註  
 當您從使用者輸入提供者命令建構圖形命令的一部分時，圖形會視為使用者提供提供者命令不透明的字串並準確地傳遞給提供者。 例如，在下列圖形命令中，  
  
```  
SHAPE {select * from t1} APPEND ({select * from t2} RELATE k1 TO k2)  
```  
  
 圖形將會執行兩個命令：`select * from t1`和 (`select * from t2 RELATE k1 TO k2)`。 如果使用者提供以分號隔開的多個提供者命令所組成的複合指令，圖形不可以區別的差異。 這在下列圖形命令中，  
  
```  
SHAPE {select * from t1; drop table t1} APPEND ({select * from t2} RELATE k1 TO k2)  
```  
  
 圖形執行`select * from t1; drop table t1`和 (`select * from t2 RELATE k1 TO k2),`他不知道，`drop table t1`還有一個在此案例中是很危險，提供者命令。 應用程式必須一律會驗證使用者輸入，以避免發生這種潛在的駭客攻擊。  
  
 此章節包含下列主題。  
  
-   [非參數化命令的作業](../../../ado/guide/data/operation-of-non-parameterized-commands.md)  
  
-   [參數化命令的作業](../../../ado/guide/data/operation-of-parameterized-commands.md)  
  
-   [混合式命令](../../../ado/guide/data/hybrid-commands.md)  
  
-   [中介 Shape COMPUTE 子句](../../../ado/guide/data/intervening-shape-compute-clauses.md)  
  
## <a name="see-also"></a>另請參閱  
 [資料成形範例](../../../ado/guide/data/data-shaping-example.md)   
 [正式 Shape 文法](../../../ado/guide/data/formal-shape-grammar.md)   
 [一般 Shape 命令](../../../ado/guide/data/shape-commands-in-general.md)
