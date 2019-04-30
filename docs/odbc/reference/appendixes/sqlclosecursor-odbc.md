---
title: SQLCloseCursor_ODBC | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLCloseCursor function [ODBC], ODBC
ms.assetid: 5e47e3f7-e1b8-451f-bf75-daa19b7c7271
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 827f7195c5d4eb4f67cb3298b75519a5583053d1
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "63199509"
---
# <a name="sqlclosecursorodbc"></a>SQLCloseCursor_ODBC
> [!IMPORTANT]  
>  Windows 的未來版本將移除這項功能。 請避免在新的開發工作中使用這項功能，並規劃修改目前使用這項功能的應用程式。 Microsoft 建議使用驅動程式的資料指標功能。  
  
 本主題討論使用**SQLCloseCursor**資料指標程式庫中的函式。 如需一般資訊**SQLCloseCursor**，請參閱[SQLCloseCursor 函式](../../../odbc/reference/syntax/sqlclosecursor-function.md)。  
  
 資料指標程式庫不支援呼叫**SQLCloseCursor**未開啟資料指標。 嘗試進行這會傳回 SQLSTATE 24000 （無效的資料指標狀態）。 呼叫**SQLFreeStmt**具有*選項*以 SQL_CLOSE 的任何資料指標開啟時支援資料指標程式庫。
