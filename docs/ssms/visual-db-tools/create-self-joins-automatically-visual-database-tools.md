---
title: 自動建立自我聯結 (Visual Database Tools) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- automatic joins
- self-joins
- joins [SQL Server], self
ms.assetid: f9ec90e8-3aad-415c-a5c4-8dfa9540e37f
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: 770d6c0813d210843f4606783aa3e9e025b81eb3
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "65095644"
---
# <a name="create-self-joins-automatically-visual-database-tools"></a>自動建立自我聯結 (Visual Database Tools)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
如果資料表具有資料庫中的自反關聯性 (Reflexive relationship)，就可讓它自動聯結至它本身。  
  
### <a name="to-create-a-self-join-automatically"></a>若要自動建立自我聯結  
  
1.  將要使用的資料表新增至 [圖表窗格](../../ssms/visual-db-tools/diagram-pane-visual-database-tools.md) 中。  
  
2.  再加入同一資料表，使 [圖表] 窗格顯示兩次相同的資料表。  
  
    [查詢和檢視表設計工具](../../ssms/visual-db-tools/query-and-view-designer-tools-visual-database-tools.md) 藉由在資料表名稱新增連續編號，來指派第二個執行個體的別名。 此外，查詢和檢視設計師會在代表這兩個以不同方式加入查詢的資料表之兩個矩形間建立聯結線。  
  
## <a name="see-also"></a>另請參閱  
[使用聯結查詢 &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/query-with-joins-visual-database-tools.md)  
  
