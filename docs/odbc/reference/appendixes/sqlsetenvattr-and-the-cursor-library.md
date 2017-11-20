---
title: "SQLSetEnvAttr 和資料指標程式庫 |Microsoft 文件"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.reviewer: 
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- SQLSetEnvAttr function [ODBC], Cursor Library
ms.assetid: 59cc8eae-09ae-4796-869a-c5806488ae83
caps.latest.revision: 8
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: c08fab3b713e1f1a57d7a81f53ed29b1678893cd
ms.contentlocale: zh-tw
ms.lasthandoff: 09/09/2017

---
# <a name="sqlsetenvattr-and-the-cursor-library"></a>SQLSetEnvAttr 和資料指標程式庫
> [!IMPORTANT]  
>  將移除這項功能，在未來的版本的 Windows。 避免在新的開發工作中使用這項功能，並規劃修改目前使用這項功能的應用程式。 Microsoft 建議使用驅動程式的資料指標功能。  
  
 本主題討論使用**SQLSetEnvAttr**函式與資料指標程式庫。 如需一般資訊**SQLSetEnvAttr**，請參閱[SQLSetEnvAttr 函數](../../../odbc/reference/syntax/sqlsetenvattr-function.md)。  
  
 資料指標程式庫不會受到 SQL_ATTR_ODBC_VERSION 環境的屬性，不論應用程式版本或驅動程式版本的設定。

