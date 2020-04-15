---
title: SQLFreeEnv 映射 |微軟文件
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLFreeEnv function [ODBC], mapping
- mapping deprecated functions [ODBC], SQLFreeEnv
ms.assetid: c0f76455-d072-4bae-bee7-452277dfa479
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 1f56bfeaee32e83ded6d8269873c9c4c33ed434e
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81302029"
---
# <a name="sqlfreeenv-mapping"></a>SQLFreeEnv 對應
當應用程式透過 ODBC *3.x*驅動程式呼叫**SQLFreeEnv**時,呼叫  
  
```  
SQLFreeEnv(henv)   
```  
  
 對應  
  
```  
SQLFreeHandle(SQL_HANDLE_ENV,Handle)  
```  
  
 將*Handle*參數設置為*henv*中的值。
