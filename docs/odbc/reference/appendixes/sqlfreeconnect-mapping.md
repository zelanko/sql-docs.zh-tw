---
title: "SQLFreeConnect 對應 |Microsoft 文件"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: odbc
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- mapping deprecated functions [ODBC], SQLFreeConnect
- SQLFreeConnect function [ODBC], mapping
ms.assetid: 8a844538-93c0-4709-bab6-35c45e771d80
caps.latest.revision: "5"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 2695026040f7ac7d258012e502cebd961d5dc7fb
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/21/2017
---
# <a name="sqlfreeconnect-mapping"></a>SQLFreeConnect 對應
當應用程式呼叫**SQLFreeConnect**透過 ODBC 3*.x*驅動程式，會呼叫  
  
```  
SQLFreeConnect(hdbc)   
```  
  
 對應到  
  
```  
SQLFreeHandle(SQL_HANDLE_DBC,Handle)  
```  
  
 與*處理*引數設定中的值為*hdbc*。
