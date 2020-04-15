---
title: SQLGetStmtOption(可視化福克斯Pro ODBC驅動程式) |微軟文件
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
ms.openlocfilehash: 2624783f7bd55903f5741c62190626e455a9096d
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81295138"
---
# <a name="sqlgetstmtoption-visual-foxpro-odbc-driver"></a>SQLGetStmtOption (Visual FoxPro ODBC Driver)
> [!NOTE]  
>  本主題包含 Visual FoxPro ODBC 特定於驅動程式的資訊。 有關此功能的一般資訊,請參閱[ODBC API 參考](../../odbc/reference/syntax/odbc-api-reference.md)下的相應主題。  
  
 支援: 完整  
  
 ODBC API 符合性:一級  
  
 返回語句選項的當前設置。  
  
|*FOption*|傳回值|  
|---------------|-------------|  
|SQL_GET_BOOKMARK|32 位元整數值,是目前記錄編號的書籤|  
|SQL_ROW_NUMBER|32 位元整數,指定結果集中目前的列的位置|  
|SQL_TRANSLATE_DLL|錯誤:"驅動程序無法使用"|  
  
 可視化 FoxPro ODBC 驅動程式沒有翻譯 DLL。  
  
 有關詳細資訊,請參閱*ODBC 程式師參考*中的[SQLGetStmtOption。](../../odbc/reference/syntax/sqlgetstmtoption-function.md)
