---
description: SQLAllocEnv 對應
title: SQLAllocEnv 對應 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLAllocEnv function [ODBC], mapping
- mapping deprecated functions [ODBC], SQLAllocEnv
ms.assetid: 4bb51845-ee91-4b97-9dd4-2fab977f2aec
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 5783eaa717b5716dd6021f34b7a904ba3994759d
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88429510"
---
# <a name="sqlallocenv-mapping"></a>SQLAllocEnv 對應
當應用程式*透過 ODBC 3.x 驅動程式呼叫* **SQLAllocEnv**時， **SQLAllocEnv** (*Phenv*) 的呼叫會對應到**SQLAllocHandle** ，如下所示：  
  
1.  驅動程式管理員會配置環境控制碼，並將其傳回給應用程式。 驅動程式管理員會呼叫 **SQLSetEnvAttr** ，將 SQL_ATTR_ODBC_VERSION 環境屬性設定為 SQL_OV_ODBC2。  
  
2.  當應用程式建立第一次連接至驅動程式時，驅動程式管理員會呼叫  
  
    ```  
    SQLAllocHandle(SQL_HANDLE_ENV, SQL_NULL_HANDLE, OutputHandlePtr)  
    ```  
  
     在 *OutputHandlePtr* 設定為 *phenv*的驅動程式中。
