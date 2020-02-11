---
title: SQLGetTypeInfo （文字檔驅動程式） |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLGetTypeInfo function [ODBC], Text File Driver
- text file driver [ODBC], SQLGetTypeInfo
ms.assetid: 05a58975-093c-4bd9-bd72-b5f0026a6e36
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 2659b3251cf77882f3762ce5699c36441e6c8ebc
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "67898645"
---
# <a name="sqlgettypeinfo-text-file-driver"></a>SQLGetTypeInfo (文字檔驅動程式)
> [!NOTE]  
>  本主題提供文字檔驅動程式特定的資訊。 如需此函數的一般資訊，請參閱[ODBC API 參考](../../odbc/reference/syntax/odbc-api-reference.md)底下的適當主題。  
  
 **SQLGetTypeInfo**所產生之資料表中所傳回的類型名稱（TYPE_NAME）將會是資料來源最常使用的名稱。  
  
 在 Byte、Counter、Double、Single、Long 和 Short 資料類型的可搜尋資料行中，將會傳回 SQL_ALL_EXCEPT_LIKE。 （您可以使用 ODBC 標準轉換函式將值轉換為字元，然後執行比較）來達到類似的功能。  
  
 當使用文字驅動程式時，當資料類型實際區分大小寫時， **SQLGetTypeInfo**會傳回文字資料類型（CHAR 和 LONGCHAR）的 CASE_SENSITIVE 值 FALSE。
