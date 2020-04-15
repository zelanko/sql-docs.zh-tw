---
title: 游標庫快取 |微軟文件
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- ODBC cursor library [ODBC], cache
- cursor library [ODBC], cache
- cache [ODBC]
ms.assetid: d6a91cd6-3905-4e3a-98ab-37fce893dbe1
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 5686bf0c3e261b1df947c02e2edaa419da498ecb
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81284688"
---
# <a name="cursor-library-cache"></a>資料指標程式庫快取
> [!IMPORTANT]  
>  此功能將在將來版本的 Windows 中刪除。 避免在新的開發工作中使用此功能,並計劃修改當前使用此功能的應用程式。 Microsoft 建議使用驅動程式的游標功能。  
  
 對於結果集中的每一行數據,游標庫緩存每個綁定列的數據、每個綁定列中的數據長度以及行的狀態。 游標庫使用緩存中的值通過**SQLFetch**和**SQLFetchScroll**返回,並為定位操作構造搜索語句。 有關詳細資訊,請參閱[建構搜尋語句](../../../odbc/reference/appendixes/constructing-searched-statements.md)。  
  
 此章節包含下列主題。  
  
-   [資料行資料](../../../odbc/reference/appendixes/column-data.md)  
  
-   [資料行資料長度](../../../odbc/reference/appendixes/length-of-column-data.md)  
  
-   [資料列狀態](../../../odbc/reference/appendixes/row-status.md)  
  
-   [快取的位置](../../../odbc/reference/appendixes/location-of-cache.md)
