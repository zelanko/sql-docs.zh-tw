---
title: SQLSetCursor 名稱(可視化狐狸 Pro ODBC 驅動程式) |微軟文件
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLSetCursorName function [ODBC], Visual FoxPro ODBC Driver
ms.assetid: 2ac5a8b5-f084-405b-b0d7-546284dfa111
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: b89bc77d12a4966762fa3aa2cf8b702ca6b47ac6
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81306123"
---
# <a name="sqlsetcursorname-visual-foxpro-odbc-driver"></a>SQLSetCursorName (Visual FoxPro ODBC Driver)
> [!NOTE]  
>  本主題包含 Visual FoxPro ODBC 特定於驅動程式的資訊。 有關此功能的一般資訊,請參閱[ODBC API 參考](../../odbc/reference/syntax/odbc-api-reference.md)下的相應主題。  
  
 支援: 完整  
  
 ODBC API 一致性:核心等級  
  
 將游標名稱與活動語句句柄*hstmt*關聯。 **SQLSetCursorName**包含在 Visual FoxPro ODBC 驅動程式 API 中,因為它是核心級 ODBC API 功能的一部分;它不能與其他 API 函數一起使用,因為驅動程式不支援定位更新。  
  
 有關詳細資訊,請參閱*ODBC 程式師參考*中的[SQLSetCursorName。](../../odbc/reference/syntax/sqlsetcursorname-function.md)
