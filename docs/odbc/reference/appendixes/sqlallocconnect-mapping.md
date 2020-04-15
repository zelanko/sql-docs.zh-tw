---
title: SQLAlloc連接映射 |微軟文件
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLAllocConnect function [ODBC], mapping
- mapping deprecated functions [ODBC], SQLAllocConnect
ms.assetid: ac89dd1f-c565-47cc-8fa3-6fa5f80b5d63
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 25e72cd3830cea8504983f4348f6c200261490f4
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81305519"
---
# <a name="sqlallocconnect-mapping"></a>SQLAllocConnect 對應
當應用程式通過ODBC 3調用**SQLAllocConnect**時。*x*驅動程式,對**SQLAllocConnect**的呼叫 *(henv,* *phdbc*) 映射到**SQLAllocHandle,** 如下所示:  
  
1.  驅動程式管理員分配連接並將其返回到應用程式。  
  
2.  當應用程式建立連接時,驅動程式管理員呼叫  
  
    ```  
    SQLAllocHandle(SQL_HANDLE_DBC, InputHandle, OutputHandlePtr)  
    ```  
  
     在驅動程式與*輸入句柄*設定為*henv,* 與*輸出句柄Ptr*設定為*phdbc*。
