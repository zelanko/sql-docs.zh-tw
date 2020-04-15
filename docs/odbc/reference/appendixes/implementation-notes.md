---
title: 實施說明 |微軟文件
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 7ec14b9c-69b8-4c6e-838a-88d1ebdc8725
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 970188a2fca45706405e398cece0f04d38dfdc68
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81284308"
---
# <a name="implementation-notes"></a>實作附註
> [!IMPORTANT]  
>  此功能將在將來版本的 Windows 中刪除。 避免在新的開發工作中使用此功能,並計劃修改當前使用此功能的應用程式。 Microsoft 建議使用驅動程式的游標功能。  
  
 本節介紹如何實現 ODBC 游標庫。 它描述了游標庫如何維護其緩存、執行 SQL 語句以及實現 ODBC 函數。  
  
 此章節包含下列主題。  
  
-   [資料指標程式庫快取](../../../odbc/reference/appendixes/cursor-library-cache.md)  
  
-   [處理 SQL 陳述式](../../../odbc/reference/appendixes/processing-sql-statements.md)  
  
-   [ODBC 函式和資料指標程式庫](../../../odbc/reference/appendixes/odbc-functions-and-the-cursor-library.md)
