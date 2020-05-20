---
title: 發出命令給基礎 Data Provider |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- shape commands [ADO]
- underlying providers [ADO]
- data shaping [ADO], commands
ms.assetid: d6001863-7733-4c32-817f-081e48587fa1
author: rothja
ms.author: jroth
ms.openlocfilehash: 6bc30f35ebfe2ddc59e9ef1404253e9bc99d62e0
ms.sourcegitcommit: 6037fb1f1a5ddd933017029eda5f5c281939100c
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/04/2020
ms.locfileid: "82757804"
---
# <a name="issuing-commands-to-the-underlying-data-provider"></a>發出命令給基礎資料提供者
不是以 SHAPE 開頭的任何命令都會傳遞到資料提供者。 這相當於以 "SHAPE {provider command}" 形式發出圖形命令。 這些命令*不*需要產生**記錄集**。 例如，假設資料提供者支援卸載資料表，則「圖形 {DROP TABLE MyTable} 是完全有效的圖形」命令。  
  
 這項功能可讓一般提供者命令和圖形命令共用相同的連接和交易。  
  
## <a name="see-also"></a>另請參閱  
 [資料成形範例](../../../ado/guide/data/data-shaping-example.md)   
 [正式圖形文法](../../../ado/guide/data/formal-shape-grammar.md)   
 [一般 Shape 命令](../../../ado/guide/data/shape-commands-in-general.md)
