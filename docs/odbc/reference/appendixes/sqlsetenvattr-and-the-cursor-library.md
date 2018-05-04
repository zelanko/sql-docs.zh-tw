---
title: SQLSetEnvAttr 和資料指標程式庫 |Microsoft 文件
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: odbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- SQLSetEnvAttr function [ODBC], Cursor Library
ms.assetid: 59cc8eae-09ae-4796-869a-c5806488ae83
caps.latest.revision: 8
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: ba46e2b455c6f2e70d392387a4015cadc1b30a85
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="sqlsetenvattr-and-the-cursor-library"></a>SQLSetEnvAttr 和資料指標程式庫
> [!IMPORTANT]  
>  將移除這項功能，在未來的版本的 Windows。 避免在新的開發工作中使用這項功能，並規劃修改目前使用這項功能的應用程式。 Microsoft 建議使用驅動程式的資料指標功能。  
  
 本主題討論使用**SQLSetEnvAttr**函式與資料指標程式庫。 如需一般資訊**SQLSetEnvAttr**，請參閱[SQLSetEnvAttr 函數](../../../odbc/reference/syntax/sqlsetenvattr-function.md)。  
  
 資料指標程式庫不會受到 SQL_ATTR_ODBC_VERSION 環境的屬性，不論應用程式版本或驅動程式版本的設定。
