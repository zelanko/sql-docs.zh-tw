---
title: 使用未命名的參數來建立查詢 (Visual Database Tools) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- unnamed parameters
- parameters [SQL Server], unnamed
ms.assetid: 5f4b664b-3d3d-4d07-a0e7-791d78743504
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: f9eebede28d257083b55ffd4b14943b7ebc1a95b
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "63184331"
---
# <a name="create-queries-with-unnamed-parameters-visual-database-tools"></a>使用未命名的參數建立查詢 (Visual Database Tools)
  您可以指定問號 (?) 做為常值的替代符號 (Placeholder)，以未命名的參數建立查詢。 查詢和檢視設計工具會為參數指定暫存名稱。 必要時，您可以在查詢中指定多個未命名參數。  
  
 當您在查詢和檢視設計工具中執行查詢時，[查詢參數] 對話方塊會顯示出暫存名稱。  
  
### <a name="to-specify-an-unnamed-parameter"></a>若要指定未命名參數  
  
1.  在 [[準則窗格]](visual-database-tools.md)中，新增您要搜尋的資料行或運算式。 如果不想讓搜尋資料行或運算式出現在查詢輸出中，請將它們從輸出資料行移除。  
  
2.  尋找內含您要搜尋之資料行或運算式的資料列，然後在 [篩選]  格線欄中輸入問號 (?)。  
  
     依照預設，查詢和檢視設計工具會加入 "=" 運算子。 不過，您可以編輯資料格，以替代 ">"、"<" 或其他 SQL 比較運算子。  
  
## <a name="see-also"></a>另請參閱  
 [使用參數查詢 &#40;Visual Database Tools&#41;](query-with-parameters-visual-database-tools.md)  
  
  
