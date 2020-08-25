---
description: 孫系彙總
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
ms.openlocfilehash: 7215846215db30d31d9a7b54f8e3a3aa2a955a43
ms.sourcegitcommit: 33e774fbf48a432485c601541840905c21f613a0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/25/2020
ms.locfileid: "88806795"
---
# <a name="grandchild-aggregates"></a>孫系彙總
在 shape 命令的子句中建立的章節資料行，可以指定 *章節別名名稱* ， (通常使用 AS 關鍵字) 。 您可以使用完整名稱來識別已成形 **記錄集** 任何章節中的任何資料行，以識別包含該資料行的子系。 例如，如果父系章節 chap1 包含的子章節 chap2 （具有金額資料行 amt），則限定名稱會是 chap1. chap2. amt。然後，限定名稱可以當做其中一個彙總函式的引數使用 (SUM、AVG、MAX、MIN、COUNT、STDEV 或任何) 。  
  
## <a name="see-also"></a>另請參閱  
 [資料成形範例](./data-shaping-example.md)