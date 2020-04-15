---
title: 行狀態 |微軟文件
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
- row status [ODBC]
- cache [ODBC]
ms.assetid: 0f0b1fb6-f697-4ced-811c-2908e210bc71
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: d4ae4169dc3f2a491663f4a86c564cfee5c2f4d6
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81305097"
---
# <a name="row-status"></a>資料列狀態
> [!IMPORTANT]  
>  此功能將在將來版本的 Windows 中刪除。 避免在新的開發工作中使用此功能,並計劃修改當前使用此功能的應用程式。 Microsoft 建議使用驅動程式的游標功能。  
  
 游標庫在緩存中為行狀態創建緩衝區。 游標庫從此緩衝區檢索行狀態陣列的值(使用SQL_ATTR_ROW_STATUS_PTR語句屬性指定)。 對於每行,游標庫將此緩衝區設置為:  
  
-   SQL_ROW_DELETED在行上執行定位刪除語句時。  
  
-   SQL_ROW_ERROR當遇到從**SQLFetch**從數據源檢索行時出錯時。  
  
-   SQL_ROW_SUCCESS,當它使用**SQLFetch**從數據源成功獲取行時。  
  
-   SQL_ROW_UPDATED在行上執行定位更新語句時。
