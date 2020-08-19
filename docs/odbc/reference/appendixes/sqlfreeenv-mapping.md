---
description: SQLFreeEnv 對應
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 1c3ccbf3175c7f17d06b55799463fb7115997e01
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88421492"
---
# <a name="sqlfreeenv-mapping"></a>SQLFreeEnv 對應
當應用程式*透過 ODBC 3.x 驅動程式呼叫* **SQLFreeEnv**時，呼叫  
  
```  
SQLFreeEnv(henv)   
```  
  
 對應至  
  
```  
SQLFreeHandle(SQL_HANDLE_ENV,Handle)  
```  
  
 將 *控制碼* 引數設定為 *henv*中的值。
