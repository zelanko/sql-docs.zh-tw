---
title: 自動建立自我聯結 (Visual Database Tools) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.component: ssms-visual-db
ms.reviewer: ''
ms.suite: sql
ms.technology: ssms
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- automatic joins
- self-joins
- joins [SQL Server], self
ms.assetid: f9ec90e8-3aad-415c-a5c4-8dfa9540e37f
caps.latest.revision: 4
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 205733571795cbdd4544043e2f4cd482d07d3e0d
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
ms.locfileid: "33046865"
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
  
