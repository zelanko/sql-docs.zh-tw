---
title: "圖形 APPEND 子句 |Microsoft 文件"
ms.prod: sql-non-specified
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- shape commands [ADO]
- data shaping [ADO], APPEND clause
- append clause [ADO]
ms.assetid: f90fcf55-6b24-401d-94e1-d65bd24bd342
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 52c9495e221ba7a4b71ba91d276eefd576f6715d
ms.contentlocale: zh-tw
ms.lasthandoff: 09/09/2017

---
# <a name="shape-append-clause"></a>圖形 APPEND 子句
圖形命令 APPEND 子句將附加的資料行或資料行，以**資料錄集**。 通常，這些資料行是章節資料行，參考子系**資料錄集**。  
  
## <a name="syntax"></a>語法  
  
```  
SHAPE [parent-command [[AS] parent-alias]] APPEND column-list  
```  
  
## <a name="description"></a>Description  
 這個子句的部分如下所示：  
  
 *父命令*  
 零或下列其中一個 (您可以省略*父命令*完全):  
  
-   提供者命令括在大括弧 （"{}"） 會傳回**資料錄集**物件。 命令發行至基礎資料提供者，並且它的語法取決於該提供者的需求。 這通常會是 SQL 語言，雖然 ADO 不需要任何特殊的查詢語言。  
  
-   另一個圖形命令內嵌在括號中。  
  
-   資料表關鍵字，後面接著資料提供者中的資料表名稱。  
  
 *父別名*  
 指的是父代的選擇性別名**資料錄集**。  
  
 *資料行清單*  
 一或多個項目：  
  
-   彙總的資料行。  
  
-   導出資料行。  
  
-   新的資料行，使用新的子句所建立。  
  
-   章節資料行。 以括號 （"（）"） 括住的章節資料行定義。 請參閱以下的語法。  
  
```  
SHAPE [parent-command [[AS] parent-alias]]  
   APPEND (child-recordset [ [[AS] child-alias]   
      RELATE parent-column TO child-column | PARAMETER param-number, ... ])  
   [[AS] chapter-alias]   
   [, ... ]  
```  
  
## <a name="remarks"></a>備註  
 *子資料錄集*  
 -   提供者命令括在大括弧 （"{}"） 會傳回**資料錄集**物件。 命令發行至基礎資料提供者，並且它的語法取決於該提供者的需求。 這通常會是 SQL 語言，雖然 ADO 不需要任何特殊的查詢語言。  
  
-   另一個圖形命令內嵌在括號中。  
  
-   現有的形狀名稱**資料錄集**。  
  
-   資料表關鍵字，後面接著資料提供者中的資料表名稱。  
  
 *子別名*  
 別名，它是指子**資料錄集**。  
  
 *父資料行*  
 中的資料行**資料錄集**傳回*父命令。*  
  
 *子資料行*  
 中的資料行**資料錄集**傳回*子命令*。  
  
 *參數數目*  
 請參閱[作業的參數化命令](../../../ado/guide/data/operation-of-parameterized-commands.md)。  
  
 *章別名*  
 參考附加至父代的章節資料行別名。  
  
> [!NOTE]
>  *"父資料行*TO*子資料行 」*子句其實是一個清單，其中每個定義的關聯性以逗號分隔  
  
> [!NOTE]
>  子句之後附加關鍵字其實是一個清單，其中每個子句以逗號分隔，並定義要附加至父代的另一個資料行。  
  
## <a name="remarks"></a>備註  
 建構時提供者命令，從使用者輸入 SHAPE 命令的一部分，圖形會視為使用者提供的提供者命令不透明的字串並準確地傳遞給提供者。 例如，在下列圖形命令，  
  
```  
SHAPE {select * from t1} APPEND ({select * from t2} RELATE k1 TO k2)  
```  
  
 圖形會執行兩個命令：`select * from t1`和 (`select * from t2 RELATE k1 TO k2)`。 如果使用者提供以分號分隔的多個提供者命令所組成的複合命令，不能夠區分不同圖形。 在下列圖形命令中，因此  
  
```  
SHAPE {select * from t1; drop table t1} APPEND ({select * from t2} RELATE k1 TO k2)  
```  
  
 圖形執行`select * from t1; drop table t1`和 (`select * from t2 RELATE k1 TO k2),`他不知道的`drop table t1`都是在這種情況下，很危險，提供者命令。 應用程式必須一律先驗證使用者輸入，以避免發生這種潛在的駭客攻擊。  
  
 此章節包含下列主題。  
  
-   [非參數化命令的作業](../../../ado/guide/data/operation-of-non-parameterized-commands.md)  
  
-   [參數化命令的作業](../../../ado/guide/data/operation-of-parameterized-commands.md)  
  
-   [混合式命令](../../../ado/guide/data/hybrid-commands.md)  
  
-   [中介圖形 COMPUTE 子句](../../../ado/guide/data/intervening-shape-compute-clauses.md)  
  
## <a name="see-also"></a>另請參閱  
 [資料成形範例](../../../ado/guide/data/data-shaping-example.md)   
 [型式圖形文法](../../../ado/guide/data/formal-shape-grammar.md)   
 [在一般的圖形命令](../../../ado/guide/data/shape-commands-in-general.md)

