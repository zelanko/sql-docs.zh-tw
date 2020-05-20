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
author: rothja
ms.author: jroth
ms.openlocfilehash: 148a2798d04bc7ec41832e5103d8ec097ffa9a0c
ms.sourcegitcommit: 6037fb1f1a5ddd933017029eda5f5c281939100c
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/04/2020
ms.locfileid: "82764819"
---
# <a name="grandchild-aggregates"></a>孫系彙總
在 shape 命令的子句中所建立的章節資料行，可能會提供*章節別名名稱*（通常使用 AS 關鍵字）。 您可以使用可識別包含資料行之子系的完整名稱，來識別已塑造之**記錄集**任一章節中的任何資料行。 例如，如果父系章節 chap1 包含一個子章節 chap2，其中具有金額資料行 amt，則限定名稱會是 chap1. chap2 amt。然後，限定名稱可以當做其中一個彙總函式（SUM、AVG、MAX、MIN、COUNT、STDEV 或 ANY）的引數使用。  
  
## <a name="see-also"></a>另請參閱  
 [資料成形範例](../../../ado/guide/data/data-shaping-example.md)
