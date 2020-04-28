---
title: 孫匯總 |Microsoft Docs
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
ms.openlocfilehash: ac0b06479b3ad4feedaa63bdac227d028b7a9e09
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "67925233"
---
# <a name="grandchild-aggregates"></a>孫系彙總
在 shape 命令的子句中所建立的章節資料行，可能會提供*章節別名名稱*（通常使用 AS 關鍵字）。 您可以使用可識別包含資料行之子系的完整名稱，來識別已塑造之**記錄集**任一章節中的任何資料行。 例如，如果父系章節 chap1 包含一個子章節 chap2，其中具有金額資料行 amt，則限定名稱會是 chap1. chap2 amt。然後，限定名稱可以當做其中一個彙總函式（SUM、AVG、MAX、MIN、COUNT、STDEV 或 ANY）的引數使用。  
  
## <a name="see-also"></a>另請參閱  
 [資料成形範例](../../../ado/guide/data/data-shaping-example.md)
