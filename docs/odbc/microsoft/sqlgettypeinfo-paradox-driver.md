---
title: SQLGetTypeInfo （Paradox 驅動程式） |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLGetTypeInfo function [ODBC], Paradox Driver
- Paradox driver [ODBC], SQLGetTypeInfo
ms.assetid: e65063c7-ba9e-4cf0-ac13-4bb5bd2937db
author: MightyPen
ms.author: genemi
ms.openlocfilehash: c212584972f4a7e329d124cc8512be3b1f7a6b9d
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/15/2019
ms.locfileid: "67898619"
---
# <a name="sqlgettypeinfo-paradox-driver"></a>SQLGetTypeInfo (Paradox 驅動程式)
> [!NOTE]  
>  本主題提供 Paradox 驅動程式特有的資訊。 如需此函式的一般資訊，請參閱底下的適當主題[ODBC API 參考](../../odbc/reference/syntax/odbc-api-reference.md)。  
  
 產生的資料表中所傳回的型別 (TYPE_NAME) 名稱**SQLGetTypeInfo**會是最常用的資料來源的名稱。  
  
 SQL_ALL_EXCEPT_LIKE 就會傳回可搜尋的資料行中位元組、 計數器、 Double、 單一、 長時間，以及 Short 資料類型。 (LIKE 功能可藉由將值轉換成字元，使用 ODBC 標準的轉換函式中，然後再執行比較。)
