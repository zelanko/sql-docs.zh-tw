---
title: 資料指標程式庫快取 |Microsoft Docs
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 597abe268979852d754e2e3e86ae81daa8f3fed8
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/15/2019
ms.locfileid: "68019073"
---
# <a name="cursor-library-cache"></a>資料指標程式庫快取
> [!IMPORTANT]  
>  Windows 的未來版本將移除這項功能。 請避免在新的開發工作中使用這項功能，並規劃修改目前使用這項功能的應用程式。 Microsoft 建議使用驅動程式的資料指標功能。  
  
 每個資料列的結果集中的資料，資料指標程式庫會快取每個繫結的資料行，每個繫結的資料行中的資料長度與資料列的狀態的資料。 資料指標程式庫使用的快取這兩個中的值，傳回透過**SQLFetch**並**SQLFetchScroll**並建構搜尋陳述式中的定位作業。 如需詳細資訊，請參閱 <<c0> [ 建構搜尋的陳述式](../../../odbc/reference/appendixes/constructing-searched-statements.md)。  
  
 此章節包含下列主題。  
  
-   [資料行資料](../../../odbc/reference/appendixes/column-data.md)  
  
-   [資料行資料長度](../../../odbc/reference/appendixes/length-of-column-data.md)  
  
-   [資料列狀態](../../../odbc/reference/appendixes/row-status.md)  
  
-   [快取的位置](../../../odbc/reference/appendixes/location-of-cache.md)
