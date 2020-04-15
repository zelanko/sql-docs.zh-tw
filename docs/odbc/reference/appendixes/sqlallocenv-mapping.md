---
title: SQLAllocEnv 映射 |微軟文件
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
ms.openlocfilehash: cb26e3443fabda2d6490c071b1f2668895e66b8d
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81304039"
---
# <a name="sqlallocenv-mapping"></a>SQLAllocEnv 對應
當應用程式透過 ODBC *3.x*驅動程式呼叫**SQLAllocEnv**時,對**SQLAllocEnv***(phenv*) 的呼叫將映射到**SQLAllocHandle,** 如下所示:  
  
1.  驅動程式管理員分配一個環境句柄並將其返回到應用程式。 驅動程式管理員調用**SQLSetEnvAttr**將SQL_ATTR_ODBC_VERSION環境屬性設置為SQL_OV_ODBC2。  
  
2.  當應用程式建立與驅動程式的第一個連接時,驅動程式管理員呼叫  
  
    ```  
    SQLAllocHandle(SQL_HANDLE_ENV, SQL_NULL_HANDLE, OutputHandlePtr)  
    ```  
  
     在具有*OutputHandlePtr*設置為*phenv*的驅動程式中。
