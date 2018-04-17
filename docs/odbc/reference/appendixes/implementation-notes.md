---
title: 實作注意事項 |Microsoft 文件
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: odbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 7ec14b9c-69b8-4c6e-838a-88d1ebdc8725
caps.latest.revision: 8
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 65facfed98692db0d8a9ce2e76e4973f8fbd9601
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/16/2018
---
# <a name="implementation-notes"></a>實作注意事項
> [!IMPORTANT]  
>  將移除這項功能，在未來的版本的 Windows。 避免在新的開發工作中使用這項功能，並規劃修改目前使用這項功能的應用程式。 Microsoft 建議使用驅動程式的資料指標功能。  
  
 本章節描述如何實作 ODBC 資料指標程式庫。 它會描述資料指標程式庫如何維護其快取、 執行 SQL 陳述式，而且會實作 ODBC 函數。  
  
 此章節包含下列主題。  
  
-   [資料指標程式庫快取](../../../odbc/reference/appendixes/cursor-library-cache.md)  
  
-   [處理 SQL 陳述式](../../../odbc/reference/appendixes/processing-sql-statements.md)  
  
-   [ODBC 函式和資料指標程式庫](../../../odbc/reference/appendixes/odbc-functions-and-the-cursor-library.md)
