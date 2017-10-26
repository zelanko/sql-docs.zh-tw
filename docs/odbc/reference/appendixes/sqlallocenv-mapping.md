---
title: "SQLAllocEnv 對應 |Microsoft 文件"
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
- SQLAllocEnv function [ODBC], mapping
- mapping deprecated functions [ODBC], SQLAllocEnv
ms.assetid: 4bb51845-ee91-4b97-9dd4-2fab977f2aec
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 66261c8fd8236a4abc35ac70e29f63b49f646daf
ms.contentlocale: zh-tw
ms.lasthandoff: 09/09/2017

---
# <a name="sqlallocenv-mapping"></a>SQLAllocEnv 對應
當應用程式呼叫**SQLAllocEnv**透過 ODBC 3*.x*驅動程式，會呼叫**SQLAllocEnv**(*phenv*) 會對應至**SQLAllocHandle** ，如下所示：  
  
1.  驅動程式管理員配置環境控制代碼，並傳回至應用程式。 驅動程式管理員呼叫**SQLSetEnvAttr**設 SQL_OV_ODBC2 SQL_ATTR_ODBC_VERSION 環境屬性。  
  
2.  當應用程式建立與驅動程式的第一個連接時，驅動程式管理員呼叫  
  
    ```  
    SQLAllocHandle(SQL_HANDLE_ENV, SQL_NULL_HANDLE, OutputHandlePtr)  
    ```  
  
     在驅動程式搭配*OutputHandlePtr*設*phenv*。

