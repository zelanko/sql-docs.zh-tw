---
title: "身為下下層的彙總 |Microsoft 文件"
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
- grandchild aggregates [ADO]
- data shaping [ADO], grandchild aggregates
ms.assetid: 4162d35f-2ce1-4218-80a5-b6933348837e
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 0785bede442b0f89a9a8a1efacaac03c1aedf2d3
ms.contentlocale: zh-tw
ms.lasthandoff: 09/09/2017

---
# <a name="grandchild-aggregates"></a>身為下下層的彙總
建立圖形命令的子句中的章節資料行可能提供*章別名*（通常是使用 AS 關鍵字）。 您可以識別任何資料行中的形狀任何章**資料錄集**識別包含資料行的子系的完整名稱。 例如，如果父章 chap1，包含子章節，chap2，都具有 amount 資料行時，amt，就限定的名稱會是 chap1.chap2.amt。限定的名稱可用做為引數，其中彙總函式 （SUM、 AVG、 MAX、 MIN、 計數、 STDEV、 或任何）。  
  
## <a name="see-also"></a>另請參閱  
 [資料成形範例](../../../ado/guide/data/data-shaping-example.md)
