---
title: SQL 延伸取得(游標庫) |微軟文件
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLExtendedFetch function [ODBC], Cursor Library
ms.assetid: 06fbf06f-127b-475c-b636-7b784918475d
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: fe39b2d2cbbaf72ce3844c35187040589d1dac58
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81302059"
---
# <a name="sqlextendedfetch-cursor-library"></a>SQLExtendedFetch (資料指標程式庫)
> [!IMPORTANT]  
>  此功能將在將來版本的 Windows 中刪除。 避免在新的開發工作中使用此功能,並計劃修改當前使用此功能的應用程式。 Microsoft 建議使用驅動程式的游標功能。  
  
 本主題討論在游標庫中使用**SQL 擴展獲取**函數。 有關 SQL**擴充取得**的一般資訊,請參考[SQL 擴充取得函數](../../../odbc/reference/syntax/sqlextendedfetch-function.md)。  
  
 游標庫透過在驅動程式中重複調用**SQLFetch**實現**SQL 擴展。**  
  
 游標庫支援使用SQL_FETCH_BOOKMARK*的提取方向*呼叫**SQL 延伸 。**  
  
 使用游標庫時,對**SQLAaFetch 的**調用不能與**SQLFetchScroll 或** **SQLFetch**的調用混合。
