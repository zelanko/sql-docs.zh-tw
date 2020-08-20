---
description: SQLCloseCursor_ODBC
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
ms.openlocfilehash: d91ce573a48602ad6dce4f0cb0759c2c8dddd3aa
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88466050"
---
# <a name="sqlclosecursor_odbc"></a>SQLCloseCursor_ODBC
> [!IMPORTANT]  
>  未來的 Windows 版本將會移除這項功能。 請避免在新的開發工作中使用這項功能，並規劃修改目前使用這項功能的應用程式。 Microsoft 建議使用驅動程式的資料指標功能。  
  
 本主題討論如何在資料指標程式庫中使用 **SQLCloseCursor** 函數。 如需 **SQLCloseCursor**的一般資訊，請參閱 [SQLCloseCursor 函數](../../../odbc/reference/syntax/sqlclosecursor-function.md)。  
  
 資料指標程式庫不支援在沒有開啟資料指標的情況下呼叫 **SQLCloseCursor** 。 嘗試這麼做會傳回 SQLSTATE 24000 (不正確資料指標狀態) 。 當資料指標程式庫不支援開啟任何資料指標時，使用 SQL_CLOSE 的*選項*來呼叫**SQLFreeStmt** 。
