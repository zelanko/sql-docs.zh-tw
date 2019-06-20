---
title: 發出命令給基礎資料提供者 |Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 231d9ced5bf370b8ee7c507e930e6961cfbed5a8
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "66700575"
---
# <a name="issuing-commands-to-the-underlying-data-provider"></a>發出命令給基礎資料提供者
任何開頭不是圖形的命令傳遞給資料提供者。 這就相當於發出"SHAPE {提供者命令}"形式的圖形命令。 這些命令*不*擁有以產生**資料錄集**。 比方說，「 圖形 {卸除資料表 MyTable} 是完全有效圖形命令，假設此資料提供者支援卸除資料表。  
  
 這項功能可讓一般提供者命令和圖形的命令，來共用相同的連接和交易。  
  
## <a name="see-also"></a>另請參閱  
 [資料成形範例](../../../ado/guide/data/data-shaping-example.md)   
 [正式 Shape 文法](../../../ado/guide/data/formal-shape-grammar.md)   
 [一般 Shape 命令](../../../ado/guide/data/shape-commands-in-general.md)
