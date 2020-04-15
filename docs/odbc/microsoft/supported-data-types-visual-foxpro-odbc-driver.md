---
title: 支援的數據類型(可視化福克斯Pro ODBC驅動程式) |微軟文件
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- Visual FoxPro ODBC driver [ODBC], data types
- FoxPro ODBC driver [ODBC], data types
- data types [ODBC], Visual FoxPro ODBC driver
ms.assetid: ab529cc6-d157-4b35-b6f9-6ffd09af098c
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 3fc28464a7c14f9801473cc125b0e90c50247d68
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81301098"
---
# <a name="supported-data-types-visual-foxpro-odbc-driver"></a>支援的資料類型 (Visual FoxPro ODBC Driver)
驅動程式支援的數據類型清單通過 ODBC API 和 Microsoft 查詢顯示。  
  
## <a name="data-types-in-c-applications"></a>C 應用程式中的數據型態  
 通過使用 C 或 C++應用程式中的[SQLGetTypeInfo](../../odbc/microsoft/sqlgettypeinfo-visual-foxpro-odbc-driver.md)函數,您可以獲取 Visual FoxPro ODBC 驅動程式支援的數據類型清單。  
  
## <a name="data-types-in-applications-using-microsoft-query"></a>使用 Microsoft 查詢的應用程式中的資料型態  
 如果應用程式使用 Microsoft 查詢在 Visual FoxPro 資料源上創建新錶,則 Microsoft 查詢將顯示 **「新表定義」** 對話框。 在**欄位描述**下,「**欄位**」 方塊顯示[的 Visual FoxPro 欄位資料類型](../../odbc/microsoft/visual-foxpro-field-data-types.md)。
