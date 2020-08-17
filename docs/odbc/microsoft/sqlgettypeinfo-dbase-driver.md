---
description: SQLGetTypeInfo (dBASE 驅動程式)
title: SQLGetTypeInfo (dBASE 驅動程式) |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLGetTypeInfo function [ODBC], dBASE Driver
- DBase driver [ODBC], SQLGetTypeInfo
ms.assetid: 6e9ce02b-97c7-4c1a-91e0-829df7459c84
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 5c94bca8dbc8413f6a3b8fdffed61f9ecd15f78e
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88339964"
---
# <a name="sqlgettypeinfo-dbase-driver"></a>SQLGetTypeInfo (dBASE 驅動程式)
> [!NOTE]  
>  本主題提供 dBASE 驅動程式特定的資訊。 如需此函數的一般資訊，請參閱 [ODBC API 參考](../../odbc/reference/syntax/odbc-api-reference.md)下的適當主題。  
  
 **SQLGetTypeInfo**所產生之資料表中傳回的類型 (TYPE_NAME) 名稱，將會是資料來源最常使用的名稱。  
  
 SQL_ALL_EXCEPT_LIKE 將會傳回給 Byte、Counter、Double、Single、Long 和 Short 資料類型的可搜尋資料行。 您可以使用 ODBC 標準轉換函式將值轉換為字元，然後執行比較，來達成 (LIKE 功能。 ) 
