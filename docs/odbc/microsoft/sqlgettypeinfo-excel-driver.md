---
description: SQLGetTypeInfo (Excel 驅動程式)
title: SQLGetTypeInfo (Excel 驅動程式) |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLGetTypeInfo function [ODBC], Excel Driver
- Excel driver [ODBC], SQLGetTypeInfo
ms.assetid: 708845be-e6a1-4677-8113-c52819a43fa4
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: ca7e70d9f26a87ededb21bc6c48f3d3cd31d8af3
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88339954"
---
# <a name="sqlgettypeinfo-excel-driver"></a>SQLGetTypeInfo (Excel 驅動程式)
> [!NOTE]  
>  本主題提供 Excel 驅動程式特定的資訊。 如需此函數的一般資訊，請參閱 [ODBC API 參考](../../odbc/reference/syntax/odbc-api-reference.md)下的適當主題。  
  
 **SQLGetTypeInfo**所產生之資料表中傳回的類型 (TYPE_NAME) 名稱，將會是資料來源最常使用的名稱。  
  
 SQL_ALL_EXCEPT_LIKE 將會傳回給 Byte、Counter、Double、Single、Long 和 Short 資料類型的可搜尋資料行。 您可以使用 ODBC 標準轉換函式將值轉換為字元，然後執行比較，來達成 (LIKE 功能。 )   
  
 使用 Microsoft Excel 驅動程式時，會在 **SQLGetTypeInfo**所傳回的 TYPE_NAME 資料行中傳回 ODBC 型別名稱。
