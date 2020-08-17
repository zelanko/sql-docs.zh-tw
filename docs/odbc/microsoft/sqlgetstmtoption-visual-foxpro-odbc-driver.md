---
description: SQLGetStmtOption (Visual FoxPro ODBC Driver)
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: e57456ca05e39c12b83da80cd19c34f482c3d8df
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88340084"
---
# <a name="sqlgetstmtoption-visual-foxpro-odbc-driver"></a>SQLGetStmtOption (Visual FoxPro ODBC Driver)
> [!NOTE]  
>  本主題包含 Visual FoxPro ODBC 驅動程式特定的資訊。 如需此函數的一般資訊，請參閱 [ODBC API 參考](../../odbc/reference/syntax/odbc-api-reference.md)下的適當主題。  
  
 支援： Full  
  
 ODBC API 一致性：層級1  
  
 傳回語句選項的目前設定。  
  
|*FOption*|傳回|  
|---------------|-------------|  
|SQL_GET_BOOKMARK|32位整數值，這是目前記錄號碼的書簽。|  
|SQL_ROW_NUMBER|32位整數，指定結果集內目前資料列的位置|  
|SQL_TRANSLATE_DLL|錯誤：「驅動程式無法執行」|  
  
 Visual FoxPro ODBC 驅動程式沒有轉譯 Dll。  
  
 如需詳細資訊，請參閱《 *ODBC 程式設計人員參考*》中的[SQLGetStmtOption](../../odbc/reference/syntax/sqlgetstmtoption-function.md) 。
