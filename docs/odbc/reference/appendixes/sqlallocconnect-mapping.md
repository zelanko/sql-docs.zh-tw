---
title: "SQLAllocConnect 對應 |Microsoft 文件"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.reviewer: 
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- SQLAllocConnect function [ODBC], mapping
- mapping deprecated functions [ODBC], SQLAllocConnect
ms.assetid: ac89dd1f-c565-47cc-8fa3-6fa5f80b5d63
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 0188c47d6abfd294dc1a9c20c04ea7d271443a18
ms.contentlocale: zh-tw
ms.lasthandoff: 09/09/2017

---
# <a name="sqlallocconnect-mapping"></a>SQLAllocConnect 對應
當應用程式呼叫**SQLAllocConnect**透過 ODBC 3。*x*驅動程式，會呼叫**SQLAllocConnect**(*henv*， *phdbc*) 會對應至**SQLAllocHandle** ，如下所示：  
  
1.  驅動程式管理員配置的連接，並傳回至應用程式。  
  
2.  當應用程式建立連接時，驅動程式管理員呼叫  
  
    ```  
    SQLAllocHandle(SQL_HANDLE_DBC, InputHandle, OutputHandlePtr)  
    ```  
  
     在驅動程式搭配*InputHandle*設*henv*，和*OutputHandlePtr*設*phdbc*。

