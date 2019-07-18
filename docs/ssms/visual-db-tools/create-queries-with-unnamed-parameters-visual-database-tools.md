---
title: 使用未命名的參數來建立查詢 (Visual Database Tools) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- unnamed parameters
- parameters [SQL Server], unnamed
ms.assetid: 5f4b664b-3d3d-4d07-a0e7-791d78743504
author: markingmyname
ms.author: maghan
manager: jroth
ms.openlocfilehash: 74754bbd3b4af014febc532e5fb522e7c8a0b82a
ms.sourcegitcommit: 5d839dc63a5abb65508dc498d0a95027d530afb6
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/09/2019
ms.locfileid: "67690514"
---
# <a name="create-queries-with-unnamed-parameters-visual-database-tools"></a>使用未命名的參數建立查詢 (Visual Database Tools)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
您可以指定問號 (?) 做為常值的替代符號 (Placeholder)，以未命名的參數建立查詢。 查詢和檢視設計工具會為參數指定暫存名稱。 必要時，您可以在查詢中指定多個未命名參數。  
  
當您在查詢和檢視設計工具中執行查詢時，[查詢參數] 對話方塊會顯示出暫存名稱。  
  
### <a name="to-specify-an-unnamed-parameter"></a>若要指定未命名參數  
  
1.  在 [[準則窗格]](../../ssms/visual-db-tools/criteria-pane-visual-database-tools.md)中，新增您要搜尋的資料行或運算式。 如果不想讓搜尋資料行或運算式出現在查詢輸出中，請將它們從輸出資料行移除。  
  
2.  尋找內含您要搜尋之資料行或運算式的資料列，然後在 [篩選]  格線欄中輸入問號 (?)。  
  
    依照預設，查詢和檢視設計工具會加入 "=" 運算子。 不過，您可以編輯資料格，以替代 ">"、"<" 或其他 SQL 比較運算子。  
  
## <a name="see-also"></a>另請參閱  
[使用參數查詢 &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/query-with-parameters-visual-database-tools.md)  
  
