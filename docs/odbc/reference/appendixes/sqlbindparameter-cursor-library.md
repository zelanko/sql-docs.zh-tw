---
title: SQLBind參數(游標庫) |微軟文件
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLBindParameter function [ODBC], Cursor Library
ms.assetid: 04c53e4c-cd1d-40b2-9997-684ebe43499f
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 55708cc5192fb40149d6db7710f6ee638c4880d2
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81305426"
---
# <a name="sqlbindparameter-cursor-library"></a>SQLBindParameter (資料指標程式庫)
> [!IMPORTANT]  
>  此功能將在將來版本的 Windows 中刪除。 避免在新的開發工作中使用此功能,並計劃修改當前使用此功能的應用程式。 Microsoft 建議使用驅動程式的游標功能。  
  
 本主題討論在游標庫中使用**SQLBind 參數**函數。 有關**SQLBind 參數的**一般資訊,請參閱[SQLBind 參數函數](../../../odbc/reference/syntax/sqlbindparameter-function.md)。  
  
 只要綁定列的 C 資料類型、列大小和十進位數位保持不變,應用程式就可以調用**SQLBindParameter**重新繫結參數。  
  
 游標庫支援將SQL_ATTR_ROW_BIND_OFFSET_PTR語句屬性設置為使用綁定偏移量。 **(SQLBind 參數**不必呼叫,此重新綁定發生。  
  
 游標庫支援綁定執行時的數據參數。
