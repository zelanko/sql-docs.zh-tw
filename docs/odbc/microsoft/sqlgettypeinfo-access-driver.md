---
title: SQLGetTypeInfo （Access 驅動程式） |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- Access driver [ODBC], SQLGetTypeInfo
- SQLGetTypeInfo function [ODBC], Access Driver
ms.assetid: a28b16eb-ca36-4297-9297-ecd7c107a84e
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 788f0b8c69636ad9bf93de73632abc911a0fb0e3
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "67898758"
---
# <a name="sqlgettypeinfo-access-driver"></a>SQLGetTypeInfo (Access 驅動程式)
> [!NOTE]  
>  本主題提供存取驅動程式特定的資訊。 如需此函數的一般資訊，請參閱[ODBC API 參考](../../odbc/reference/syntax/odbc-api-reference.md)底下的適當主題。  
  
 **SQLGetTypeInfo**所產生之資料表中所傳回的類型名稱（TYPE_NAME）將會是資料來源最常使用的名稱。  
  
 在 Byte、Counter、Double、Single、Long 和 Short 資料類型的可搜尋資料行中，將會傳回 SQL_ALL_EXCEPT_LIKE。 （您可以使用 ODBC 標準轉換函式將值轉換為字元，然後執行比較）來達到類似的功能。
