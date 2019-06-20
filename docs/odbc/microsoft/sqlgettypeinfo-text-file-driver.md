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
manager: craigg
ms.openlocfilehash: 3c1c38b66e9b8a3c1cbed4a3712f7af866935089
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "63210230"
---
# <a name="sqlgettypeinfo-text-file-driver"></a>SQLGetTypeInfo (文字檔驅動程式)
> [!NOTE]  
>  本主題提供文字檔驅動程式特有的資訊。 如需此函式的一般資訊，請參閱底下的適當主題[ODBC API 參考](../../odbc/reference/syntax/odbc-api-reference.md)。  
  
 產生的資料表中所傳回的型別 (TYPE_NAME) 名稱**SQLGetTypeInfo**會是最常用的資料來源的名稱。  
  
 SQL_ALL_EXCEPT_LIKE 就會傳回可搜尋的資料行中位元組、 計數器、 Double、 單一、 長時間，以及 Short 資料類型。 （LIKE 功能可藉由將值轉換成使用 ODBC 標準的轉換函式，然後執行比較的字元。）  
  
 使用文字驅動程式時， **SQLGetTypeInfo**資料類型 （CHAR 和 LONGCHAR） 會傳回文字 CASE_SENSITIVE 值為 FALSE 時的資料類型實際上是區分大小寫。
