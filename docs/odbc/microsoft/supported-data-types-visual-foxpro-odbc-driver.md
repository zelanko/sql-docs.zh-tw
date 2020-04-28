---
title: 支援的資料類型（Visual FoxPro ODBC Driver） |Microsoft Docs
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
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "81301098"
---
# <a name="supported-data-types-visual-foxpro-odbc-driver"></a>支援的資料類型 (Visual FoxPro ODBC Driver)
驅動程式支援的資料類型清單會透過 ODBC API 和 Microsoft Query 來呈現。  
  
## <a name="data-types-in-c-applications"></a>C 應用程式中的資料類型  
 您可以使用 C 或 c + + 應用程式中的[SQLGetTypeInfo](../../odbc/microsoft/sqlgettypeinfo-visual-foxpro-odbc-driver.md)函數，取得 VISUAL FoxPro ODBC 驅動程式所支援的資料類型清單。  
  
## <a name="data-types-in-applications-using-microsoft-query"></a>使用 Microsoft Query 的應用程式中的資料類型  
 如果您的應用程式使用 Microsoft Query 在 Visual FoxPro 資料來源上建立新的資料表，Microsoft Query 會顯示 [**新增資料表定義**] 對話方塊。 [**欄位描述**] 底下的 [**類型**] 方塊會列出以單一字元表示的[Visual FoxPro 欄位資料類型](../../odbc/microsoft/visual-foxpro-field-data-types.md)。
