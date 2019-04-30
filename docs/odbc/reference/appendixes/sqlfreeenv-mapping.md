---
title: SQLFreeEnv Mapping | Microsoft Docs
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
manager: craigg
ms.openlocfilehash: 5c1ab12a975d7b9c0aba77db9af31accac398a16
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "63199414"
---
# <a name="sqlfreeenv-mapping"></a>SQLFreeEnv 對應
當應用程式呼叫**SQLFreeEnv**透過 ODBC 3 *.x*驅動程式，會呼叫  
  
```  
SQLFreeEnv(henv)   
```  
  
 對應至  
  
```  
SQLFreeHandle(SQL_HANDLE_ENV,Handle)  
```  
  
 具有*處理*引數設定中的值為*henv*。
