---
description: 發出命令給基礎資料提供者
title: 發出命令給基礎 Data Provider |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
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
ms.openlocfilehash: d4f1db51d54b69bf42fe185d30b78df57b89df39
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/27/2020
ms.locfileid: "88980429"
---
# <a name="issuing-commands-to-the-underlying-data-provider"></a>發出命令給基礎資料提供者
任何不是以 SHAPE 開頭的命令都會傳遞至資料提供者。 這相當於以 "SHAPE {provider command}" 格式發出圖形命令。 這些命令 *不* 需要產生 **記錄集**。 例如，假設資料提供者支援 DROP TABLE，則 "SHAPE {DROP TABLE MyTable} 是完全有效的 SHAPE 命令。  
  
 這項功能可讓一般提供者命令和圖形命令共用相同的連接和交易。  
  
## <a name="see-also"></a>另請參閱  
 [資料成形範例](./data-shaping-example.md)   
 [正式式圖形文法](./formal-shape-grammar.md)   
 [一般 Shape 命令](./shape-commands-in-general.md)