---
title: SQLFreeEnv 對應 |Microsoft Docs
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: ef89943f95a6492614972c3e89fe2129becc1aa5
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/15/2019
ms.locfileid: "68086417"
---
# <a name="sqlfreeenv-mapping"></a>SQLFreeEnv 對應
當應用程式呼叫**SQLFreeEnv**透過 ODBC *3.x*驅動程式，會呼叫  
  
```  
SQLFreeEnv(henv)   
```  
  
 對應至  
  
```  
SQLFreeHandle(SQL_HANDLE_ENV,Handle)  
```  
  
 具有*處理*引數設定中的值為*henv*。
