---
description: SQLFreeStmt 對應
title: SQLFreeStmt 對應 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLFreeStmt function [ODBC], mapping
- mapping deprecated functions [ODBC], SQLFreeStmt
ms.assetid: 267d95f2-4f0c-47ab-9411-5afe105215a2
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 1f5066593e900fc60eea0ce5a5fc183eb2e83137
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88421482"
---
# <a name="sqlfreestmt-mapping"></a>SQLFreeStmt 對應
當應用程式*透過 ODBC 3.x 驅動程式以*SQL_DROP 的*選項*引數呼叫**SQLFreeStmt**時，呼叫  
  
```  
SQLFreeStmt(hstmt, SQL_DROP)   
```  
  
 對應至  
  
```  
SQLFreeHandle(SQL_HANDLE_STMT,Handle)  
```  
  
 將 *控制碼* 引數設定為 *hstmt*中的值。
