---
title: 資料列狀態 |Microsoft Docs
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
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "81305097"
---
# <a name="row-status"></a>資料列狀態
> [!IMPORTANT]  
>  這項功能將會在未來的 Windows 版本中移除。 請避免在新的開發工作中使用這項功能，並規劃修改目前使用這項功能的應用程式。 Microsoft 建議使用驅動程式的資料指標功能。  
  
 資料指標程式庫會在快取中建立資料列狀態的緩衝區。 資料指標程式庫會從這個緩衝區抓取資料列狀態陣列（以 SQL_ATTR_ROW_STATUS_PTR 語句屬性指定）的值。 針對每個資料列，資料指標程式庫會將此緩衝區設定為：  
  
-   當它在資料列上執行定位 delete 語句時，就會 SQL_ROW_DELETED。  
  
-   當它遇到錯誤，並使用**SQLFetch**從資料來源中抓取資料列時，SQL_ROW_ERROR。  
  
-   當它使用**SQLFetch**從資料來源成功提取資料列時，就會 SQL_ROW_SUCCESS。  
  
-   當它在資料列上執行定位的 update 語句時，SQL_ROW_UPDATED。
