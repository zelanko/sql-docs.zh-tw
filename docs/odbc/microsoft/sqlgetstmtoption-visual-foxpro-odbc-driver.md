---
title: SQLGetStmtOption (Visual FoxPro ODBC Driver) |Microsoft Docs
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
manager: craigg
ms.openlocfilehash: 373f5e13712ef7b0864401ea3d2c204cb03ebb09
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "63240259"
---
# <a name="sqlgetstmtoption-visual-foxpro-odbc-driver"></a>SQLGetStmtOption (Visual FoxPro ODBC Driver)
> [!NOTE]  
>  本主題包含 Visual FoxPro ODBC 驅動程式特有的資訊。 如需此函式的一般資訊，請參閱底下的適當主題[ODBC API 參考](../../odbc/reference/syntax/odbc-api-reference.md)。  
  
 支援：完整  
  
 ODBC API 相容性：層級一個  
  
 傳回目前的陳述式選項的設定。  
  
|*Sqlfreestmt*|傳回值|  
|---------------|-------------|  
|SQL_GET_BOOKMARK|32 位元整數值，是目前的記錄數目的書籤|  
|SQL_ROW_NUMBER|32 位元整數，指定目前的資料列，結果中的位置設定|  
|SQL_TRANSLATE_DLL|Error:「 驅動程式不支援 」|  
  
 Visual FoxPro ODBC Driver 已轉譯的 Dll。  
  
 如需詳細資訊，請參閱 < [SQLGetStmtOption](../../odbc/reference/syntax/sqlgetstmtoption-function.md)中*ODBC 程式設計人員參考*。
