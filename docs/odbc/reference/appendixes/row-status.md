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
ms.openlocfilehash: a62bad0e69a8bf8b5365575f97e4791cbbf270d6
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "68057116"
---
# <a name="row-status"></a>資料列狀態
> [!IMPORTANT]  
>  這項功能將會在未來的 Windows 版本中移除。 請避免在新的開發工作中使用這項功能，並規劃修改目前使用這項功能的應用程式。 Microsoft 建議使用驅動程式的資料指標功能。  
  
 資料指標程式庫會在快取中建立資料列狀態的緩衝區。 資料指標程式庫會從這個緩衝區抓取資料列狀態陣列（以 SQL_ATTR_ROW_STATUS_PTR 語句屬性指定）的值。 針對每個資料列，資料指標程式庫會將此緩衝區設定為：  
  
-   當它在資料列上執行定位 delete 語句時，就會 SQL_ROW_DELETED。  
  
-   當它遇到錯誤，並使用**SQLFetch**從資料來源中抓取資料列時，SQL_ROW_ERROR。  
  
-   當它使用**SQLFetch**從資料來源成功提取資料列時，就會 SQL_ROW_SUCCESS。  
  
-   當它在資料列上執行定位的 update 語句時，SQL_ROW_UPDATED。
