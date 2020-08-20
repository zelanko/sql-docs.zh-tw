---
description: 支援的資料類型 (Visual FoxPro ODBC Driver)
title: 支援的資料類型 (Visual FoxPro ODBC 驅動程式) |Microsoft Docs
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
ms.openlocfilehash: 04f2039d18f134fe2c48397f6c0dc987e97bf47d
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88471520"
---
# <a name="supported-data-types-visual-foxpro-odbc-driver"></a>支援的資料類型 (Visual FoxPro ODBC Driver)
驅動程式支援的資料類型清單會透過 ODBC API 和 Microsoft Query 來呈現。  
  
## <a name="data-types-in-c-applications"></a>C 應用程式中的資料類型  
 您可以使用 C 或 c + + 應用程式中的 [SQLGetTypeInfo](../../odbc/microsoft/sqlgettypeinfo-visual-foxpro-odbc-driver.md) 函式，取得 VISUAL FoxPro ODBC 驅動程式所支援的資料類型清單。  
  
## <a name="data-types-in-applications-using-microsoft-query"></a>使用 Microsoft Query 的應用程式中的資料類型  
 如果您的應用程式使用 Microsoft Query 在 Visual FoxPro 資料來源上建立新的資料表，Microsoft 查詢會顯示 [ **新增資料表定義** ] 對話方塊。 在 [ **欄位描述**] 下，[ **類型** ] 方塊會列出以單一字元表示的 [Visual FoxPro 欄位資料類型](../../odbc/microsoft/visual-foxpro-field-data-types.md)。
