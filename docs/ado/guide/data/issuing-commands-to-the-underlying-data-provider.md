---
description: 發出命令給基礎資料提供者
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
ms.openlocfilehash: 6d9000fdf63a908257c9dbdfa29dc7b57dbb7ecf
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88453230"
---
# <a name="issuing-commands-to-the-underlying-data-provider"></a>發出命令給基礎資料提供者
任何不是以 SHAPE 開頭的命令都會傳遞至資料提供者。 這相當於以 "SHAPE {provider command}" 格式發出圖形命令。 這些命令 *不* 需要產生 **記錄集**。 例如，假設資料提供者支援 DROP TABLE，則 "SHAPE {DROP TABLE MyTable} 是完全有效的 SHAPE 命令。  
  
 這項功能可讓一般提供者命令和圖形命令共用相同的連接和交易。  
  
## <a name="see-also"></a>另請參閱  
 [資料成形範例](../../../ado/guide/data/data-shaping-example.md)   
 [正式式圖形文法](../../../ado/guide/data/formal-shape-grammar.md)   
 [一般 Shape 命令](../../../ado/guide/data/shape-commands-in-general.md)
