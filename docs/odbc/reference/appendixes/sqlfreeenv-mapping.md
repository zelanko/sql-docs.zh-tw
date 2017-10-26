---
title: "SQLFreeEnv 對應 |Microsoft 文件"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- SQLFreeEnv function [ODBC], mapping
- mapping deprecated functions [ODBC], SQLFreeEnv
ms.assetid: c0f76455-d072-4bae-bee7-452277dfa479
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: a5c1dae2fb67d530e9e8bfefd041eb978eb5bf15
ms.contentlocale: zh-tw
ms.lasthandoff: 09/09/2017

---
# <a name="sqlfreeenv-mapping"></a>SQLFreeEnv 對應
當應用程式呼叫**SQLFreeEnv**透過 ODBC 3*.x*驅動程式，會呼叫  
  
```  
SQLFreeEnv(henv)   
```  
  
 對應到  
  
```  
SQLFreeHandle(SQL_HANDLE_ENV,Handle)  
```  
  
 與*處理*引數設定中的值為*henv*。

