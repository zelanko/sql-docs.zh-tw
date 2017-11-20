---
title: "資料指標程式庫快取 |Microsoft 文件"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.reviewer: 
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- ODBC cursor library [ODBC], cache
- cursor library [ODBC], cache
- cache [ODBC]
ms.assetid: d6a91cd6-3905-4e3a-98ab-37fce893dbe1
caps.latest.revision: 8
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 06b893a857f87c2d6c3911e3d81fd0cd02d89668
ms.contentlocale: zh-tw
ms.lasthandoff: 09/09/2017

---
# <a name="cursor-library-cache"></a>資料指標程式庫快取
> [!IMPORTANT]  
>  將移除這項功能，在未來的版本的 Windows。 避免在新的開發工作中使用這項功能，並規劃修改目前使用這項功能的應用程式。 Microsoft 建議使用驅動程式的資料指標功能。  
  
 每個資料列的結果集中的資料，資料指標程式庫會快取每個繫結的資料行，資料列的狀態和每個繫結的資料行中的資料長度的資料。 資料指標程式庫使用快取中這兩個值，來透過傳回**SQLFetch**和**SQLFetchScroll**和建構搜尋陳述式中的定位作業。 如需詳細資訊，請參閱[建構搜尋陳述式](../../../odbc/reference/appendixes/constructing-searched-statements.md)。  
  
 此章節包含下列主題。  
  
-   [資料行的資料](../../../odbc/reference/appendixes/column-data.md)  
  
-   [資料行資料的長度](../../../odbc/reference/appendixes/length-of-column-data.md)  
  
-   [資料列狀態](../../../odbc/reference/appendixes/row-status.md)  
  
-   [快取的位置](../../../odbc/reference/appendixes/location-of-cache.md)

