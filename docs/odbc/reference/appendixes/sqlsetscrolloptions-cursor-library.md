---
description: SQLSetScrollOptions (資料指標程式庫)
title: SQLSetScrollOptions (資料指標程式庫) |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLSetScrollOptions function [ODBC], Cursor Library
ms.assetid: c5c0ac6d-a6c1-4077-8186-1644df1944f8
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: f40e5cd3b62b91b1b0b832b9b8fcf36101487c10
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88386554"
---
# <a name="sqlsetscrolloptions-cursor-library"></a>SQLSetScrollOptions (資料指標程式庫)
> [!IMPORTANT]  
>  未來的 Windows 版本將會移除這項功能。 請避免在新的開發工作中使用這項功能，並規劃修改目前使用這項功能的應用程式。 Microsoft 建議使用驅動程式的資料指標功能。  
  
 本主題討論如何在資料指標程式庫中使用 **SQLSetScrollOptions** 函數。 如需 **SQLSetScrollOptions**的一般資訊，請參閱 [SQLSetScrollOptions 函數](../../../odbc/reference/syntax/sqlsetscrolloptions-function.md)。  
  
 資料指標程式庫只支援 **SQLSetScrollOptions** 回溯相容性;應用程式應該改為使用 SQL_ATTR_CONCURRENCY、SQL_ATTR_CURSOR_TYPE 和 SQL_ATTR_ROW_ARRAY_SIZE 的語句屬性。
