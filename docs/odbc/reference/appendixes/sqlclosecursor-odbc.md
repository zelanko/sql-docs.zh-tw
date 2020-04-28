---
title: SQLCloseCursor_ODBC |Microsoft Docs
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: e1b61267d093e11bf7ea25158f5dc6a29ccba6a1
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "81296298"
---
# <a name="sqlclosecursor_odbc"></a>SQLCloseCursor_ODBC
> [!IMPORTANT]  
>  這項功能將會在未來的 Windows 版本中移除。 請避免在新的開發工作中使用這項功能，並規劃修改目前使用這項功能的應用程式。 Microsoft 建議使用驅動程式的資料指標功能。  
  
 本主題討論如何在資料指標程式庫中使用**SQLCloseCursor**函數。 如需有關**SQLCloseCursor**的一般資訊，請參閱[SQLCloseCursor 函數](../../../odbc/reference/syntax/sqlclosecursor-function.md)。  
  
 資料指標程式庫不支援呼叫**SQLCloseCursor** ，而沒有開啟的資料指標。 嘗試這會傳回 SQLSTATE 24000 （不正確資料指標狀態）。 當資料指標程式庫不支援開啟任何資料指標時，使用 SQL_CLOSE*選項*呼叫**SQLFreeStmt** 。
