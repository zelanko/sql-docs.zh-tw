---
description: Shape APPEND 子句
title: Shape APPEND 子句 |Microsoft Docs
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
author: rothja
ms.author: jroth
ms.openlocfilehash: f2a04e532256de30295f2179f7b15386bceaa8b3
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88452860"
---
# <a name="shape-append-clause"></a>Shape APPEND 子句
Shape 命令 APPEND 子句會將一個或多個資料行附加到 **記錄集**。 這些資料行通常是參考子 **記錄集**的章節資料行。  
  
## <a name="syntax"></a>語法  
  
```  
SHAPE [parent-command [[AS] parent-alias]] APPEND column-list  
```  
  
## <a name="description"></a>描述  
 此子句的部分如下所示：  
  
 *parent-command*  
 零或下列其中一項 (您可以完全省略 *父命令*) ：  
  
-   以大括弧括住的提供者命令 ( " {} " ) 會傳回 **記錄集** 物件。 此命令會發出至基礎資料提供者，而且其語法取決於該提供者的需求。 這通常是 SQL 語言，雖然 ADO 不需要任何特定的查詢語言。  
  
-   內嵌在括弧中的另一個圖形命令。  
  
-   資料表關鍵字，後面接著資料提供者中的資料表名稱。  
  
 *父系-別名*  
 參考父 **記錄集**的選擇性別名。  
  
 *資料行清單*  
 下列其中一項或多項：  
  
-   匯總資料行。  
  
-   計算結果欄。  
  
-   使用 NEW 子句建立的新資料行。  
  
-   章節資料行。 章節資料行定義是以括弧括住 ( " ( # A2" ) 。 請參閱下列語法。  
  
```  
SHAPE [parent-command [[AS] parent-alias]]  
   APPEND (child-recordset [ [[AS] child-alias]   
      RELATE parent-column TO child-column | PARAMETER param-number, ... ])  
   [[AS] chapter-alias]   
   [, ... ]  
```  
  
## <a name="remarks"></a>備註  
 *子記錄集*  
 -   以大括弧括住的提供者命令 ( " {} " ) 會傳回 **記錄集** 物件。 此命令會發出至基礎資料提供者，而且其語法取決於該提供者的需求。 這通常是 SQL 語言，雖然 ADO 不需要任何特定的查詢語言。  
  
-   內嵌在括弧中的另一個圖形命令。  
  
-   現有形狀 **記錄集**的名稱。  
  
-   資料表關鍵字，後面接著資料提供者中的資料表名稱。  
  
 *child-alias*  
 參考子 **記錄集**的別名。  
  
 *父資料行*  
 *父命令*所傳回之**記錄集中**的資料行。  
  
 *子資料行*  
 *子命令*所傳回之**記錄集中**的資料行。  
  
 *param-number*  
 請參閱 [參數化命令的操作](../../../ado/guide/data/operation-of-parameterized-commands.md)。  
  
 *章節-別名*  
 別名，參考附加至父系的章節資料行。  
  
> [!NOTE]
>  「 *父資料行* 到 *子資料行* 」子句實際上是一個清單，其中定義的每個關聯性都會以逗號分隔  
  
> [!NOTE]
>  附加關鍵字後面的子句實際上是一個清單，其中每個子句會以逗號分隔，並定義要附加至父系的另一個資料行。  
  
## <a name="remarks"></a>備註  
 當您將使用者輸入中的提供者命令設計為 SHAPE 命令的一部分時，SHAPE 會將使用者提供的提供者命令視為不透明的字串，並將它們如實傳遞給提供者。 例如，在下列 SHAPE 命令中，  
  
```  
SHAPE {select * from t1} APPEND ({select * from t2} RELATE k1 TO k2)  
```  
  
 SHAPE 會執行兩個命令： `select * from t1` 和 (`select * from t2 RELATE k1 TO k2)` 。 如果使用者提供的複合命令包含以分號分隔的多個提供者命令，圖形就無法區別差異。 因此，在下列 SHAPE 命令中，  
  
```  
SHAPE {select * from t1; drop table t1} APPEND ({select * from t2} RELATE k1 TO k2)  
```  
  
 SHAPE 會執行， `select * from t1; drop table t1` 且 (`select * from t2 RELATE k1 TO k2),` 不 `drop table t1` 會發現它是個別的，在此情況下是危險的提供者命令。 應用程式必須一律驗證使用者輸入，以避免發生這類潛在駭客攻擊。  
  
 此章節包含下列主題。  
  
-   [非參數化命令的作業](../../../ado/guide/data/operation-of-non-parameterized-commands.md)  
  
-   [參數化命令的作業](../../../ado/guide/data/operation-of-parameterized-commands.md)  
  
-   [混合式命令](../../../ado/guide/data/hybrid-commands.md)  
  
-   [中介 Shape COMPUTE 子句](../../../ado/guide/data/intervening-shape-compute-clauses.md)  
  
## <a name="see-also"></a>另請參閱  
 [資料成形範例](../../../ado/guide/data/data-shaping-example.md)   
 [正式式圖形文法](../../../ado/guide/data/formal-shape-grammar.md)   
 [一般 Shape 命令](../../../ado/guide/data/shape-commands-in-general.md)
