---
title: "SQLTransact 對應 |Microsoft 文件"
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
- mapping deprecated functions [ODBC], SQLTransact
- SQLTransact function [ODBC], mapping
ms.assetid: 8a01041f-3572-46f9-8213-b817f3cf929c
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 252339f7fcd2a3893f030c0ffbc4485ab5441152
ms.contentlocale: zh-tw
ms.lasthandoff: 09/09/2017

---
# <a name="sqltransact-mapping"></a>SQLTransact 對應
**SQLTransact**現在取代**SQLEndTran**。 兩個函式之間的主要差異在於**SQLEndTran**包含引數*HandleType*，以指定要完成工作的範圍。 *HandleType*引數可以指定的環境或連接控制代碼。 下列呼叫**SQLTransact**:  
  
```  
SQLTransact(henv, hdbc, fType)  
```  
  
 對應到  
  
```  
SQLEndTran(SQL_HANDLE_DBC, ConnectionHandle, CompletionType);  
```  
  
 如果*ConnectionHandle*不等於 SQL_NULL_HDBC。 *ConnectionHandle*引數設定的值為*hdbc*。  
  
 **SQL_Transact**對應到  
  
```  
SQLEndTran (SQL_HANDLE_ENV, EnvironmentHandle, CompletionType);  
```  
  
 如果*ConnectionHandle*等於 SQL_NULL_HDBC。 *EnvironmentHandle*引數設定的值為*henv*。  
  
 在上述的情況下，這兩*CompletionType*引數設定為相同的值做為*fType*。
