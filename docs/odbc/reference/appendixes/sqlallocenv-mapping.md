---
title: SQLAllocEnv 對應 |Microsoft 文件
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- SQLAllocEnv function [ODBC], mapping
- mapping deprecated functions [ODBC], SQLAllocEnv
ms.assetid: 4bb51845-ee91-4b97-9dd4-2fab977f2aec
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 8ca05f911091bd3c18641371281f3ac4b1372063
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="sqlallocenv-mapping"></a>SQLAllocEnv 對應
當應用程式呼叫**SQLAllocEnv**透過 ODBC 3 *.x*驅動程式，會呼叫**SQLAllocEnv**(*phenv*) 會對應至**SQLAllocHandle** ，如下所示：  
  
1.  驅動程式管理員配置環境控制代碼，並傳回至應用程式。 驅動程式管理員呼叫**SQLSetEnvAttr**設 SQL_OV_ODBC2 SQL_ATTR_ODBC_VERSION 環境屬性。  
  
2.  當應用程式建立與驅動程式的第一個連接時，驅動程式管理員呼叫  
  
    ```  
    SQLAllocHandle(SQL_HANDLE_ENV, SQL_NULL_HANDLE, OutputHandlePtr)  
    ```  
  
     在驅動程式搭配*OutputHandlePtr*設*phenv*。
