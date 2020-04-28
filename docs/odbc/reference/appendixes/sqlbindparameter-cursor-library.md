---
title: SQLBindParameter （資料指標程式庫） |Microsoft Docs
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
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "81305426"
---
# <a name="sqlbindparameter-cursor-library"></a>SQLBindParameter (資料指標程式庫)
> [!IMPORTANT]  
>  這項功能將會在未來的 Windows 版本中移除。 請避免在新的開發工作中使用這項功能，並規劃修改目前使用這項功能的應用程式。 Microsoft 建議使用驅動程式的資料指標功能。  
  
 本主題討論如何在資料指標程式庫中使用**SQLBindParameter**函數。 如需有關**SQLBindParameter**的一般資訊，請參閱[SQLBindParameter 函數](../../../odbc/reference/syntax/sqlbindparameter-function.md)。  
  
 應用程式可以呼叫**SQLBindParameter**來重新系結參數，只要 C 資料類型、資料行大小和系結資料行的小數位數保持不變即可。  
  
 資料指標程式庫支援將 SQL_ATTR_ROW_BIND_OFFSET_PTR 語句屬性設定為使用系結位移。 （不需要呼叫**SQLBindParameter** ，就會發生此重新系結）。  
  
 游標程式庫支援系結資料執行中參數。
