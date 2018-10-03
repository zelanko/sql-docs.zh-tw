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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 4ce45314cef92404fe14a43e033c14d6a272e1bf
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47765786"
---
# <a name="row-status"></a>資料列狀態
> [!IMPORTANT]  
>  Windows 的未來版本將移除這項功能。 請避免在新的開發工作中使用這項功能，並規劃修改目前使用這項功能的應用程式。 Microsoft 建議使用驅動程式的資料指標功能。  
  
 資料指標程式庫建立緩衝區資料列狀態的快取中。 資料指標程式庫會從這個緩衝區中擷取資料列狀態陣列 （具有 sql_attr_row_status_ptr 設定陳述式屬性指定） 的值。 針對每個資料列，資料指標程式庫會將這個緩衝區設定為：  
  
-   SQL_ROW_DELETED 執行定位時刪除資料列上的陳述式。  
  
-   遇到與資料來源擷取資料列發生錯誤時的 SQL_ROW_ERROR **SQLFetch**。  
  
-   當它已成功擷取的資料列與資料來源的 SQL_ROW_SUCCESS **SQLFetch**。  
  
-   SQL_ROW_UPDATED 資料列上執行定位的 update 陳述式時。
