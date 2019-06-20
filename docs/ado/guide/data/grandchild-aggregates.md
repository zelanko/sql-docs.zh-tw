---
title: 孫系彙總 |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- grandchild aggregates [ADO]
- data shaping [ADO], grandchild aggregates
ms.assetid: 4162d35f-2ce1-4218-80a5-b6933348837e
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: e81a2d2274d557bf722a3762f7a3e039dfcc5d4d
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "66700840"
---
# <a name="grandchild-aggregates"></a>孫系彙總
可能會提供形狀命令的子句中所建立的章節資料行*章別名*（通常是使用 AS 關鍵字）。 您可以識別形狀的任何一章中的任何資料行**資料錄集**識別包含資料行的子系的完整名稱。 比方說，如果父本章 chap1，包含子章節，chap2，具有 amount 資料行時，amt，則限定的名稱會是 chap1.chap2.amt。限定的名稱可用做為引數，其中一個彙總函式 （SUM、 AVG、 MAX、 最小值、 計數、 STDEV，或任何）。  
  
## <a name="see-also"></a>另請參閱  
 [資料成形範例](../../../ado/guide/data/data-shaping-example.md)
