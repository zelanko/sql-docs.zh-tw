---
title: SQLGetStmtOption （Visual FoxPro ODBC Driver） |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLGetStmtOption function [ODBC], Visual FoxPro ODBC Driver
ms.assetid: 984a8b1d-f12c-420c-8be4-f555114c764b
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 5521fb11cad064cf487d38562f4146fd32587993
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "67898790"
---
# <a name="sqlgetstmtoption-visual-foxpro-odbc-driver"></a>SQLGetStmtOption (Visual FoxPro ODBC Driver)
> [!NOTE]  
>  本主題包含 Visual FoxPro ODBC 驅動程式特有的資訊。 如需此函數的一般資訊，請參閱[ODBC API 參考](../../odbc/reference/syntax/odbc-api-reference.md)底下的適當主題。  
  
 支援：完整  
  
 ODBC API 一致性：層級一  
  
 傳回語句選項的目前設定。  
  
|*FOption*|傳回值|  
|---------------|-------------|  
|SQL_GET_BOOKMARK|32-位整數值，這是目前記錄號碼的書簽|  
|SQL_ROW_NUMBER|32-bit 整數，指定目前資料列在結果集內的位置|  
|SQL_TRANSLATE_DLL|錯誤：「驅動程式不能」|  
  
 Visual FoxPro ODBC 驅動程式沒有轉譯 Dll。  
  
 如需詳細資訊，請參閱 ODBC 程式設計*人員參考*中的[SQLGetStmtOption](../../odbc/reference/syntax/sqlgetstmtoption-function.md) 。
