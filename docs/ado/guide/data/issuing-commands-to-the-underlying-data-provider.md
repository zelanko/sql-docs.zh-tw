---
title: "發出命令至基礎資料提供者 |Microsoft 文件"
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: ado
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- shape commands [ADO]
- underlying providers [ADO]
- data shaping [ADO], commands
ms.assetid: d6001863-7733-4c32-817f-081e48587fa1
caps.latest.revision: 
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: f27f4fb143db0c210097f0ae1ab7804ae827853e
ms.sourcegitcommit: acab4bcab1385d645fafe2925130f102e114f122
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/09/2018
---
# <a name="issuing-commands-to-the-underlying-data-provider"></a>發出命令至基礎資料提供者
任何不是以圖形的命令傳遞給資料提供者。 這相當於發出圖形中的命令格式為"SHAPE {提供者命令}"。 這些命令執行*不*必須產生**資料錄集**。 比方說，「 形狀 {卸除資料表 MyTable} 是完全有效圖形命令，假設此資料提供者支援卸除資料表。  
  
 這項功能可讓一般提供者命令和圖形的命令，來共用相同的連線和交易。  
  
## <a name="see-also"></a>另請參閱  
 [資料成形範例](../../../ado/guide/data/data-shaping-example.md)   
 [型式圖形文法](../../../ado/guide/data/formal-shape-grammar.md)   
 [一般 Shape 命令](../../../ado/guide/data/shape-commands-in-general.md)
