---
title: SQLTransact 對應 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- mapping deprecated functions [ODBC], SQLTransact
- SQLTransact function [ODBC], mapping
ms.assetid: 8a01041f-3572-46f9-8213-b817f3cf929c
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: d5cf669883ce81528adbe1fbd8faeff2ed716218
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47656174"
---
# <a name="sqltransact-mapping"></a>SQLTransact 對應
**SQLTransact**現在已由取代**SQLEndTran**。 兩個函式的主要差異在於**SQLEndTran**包含引數*HandleType*，以指定的工作完成的範圍。 *HandleType*引數可以指定的環境或連接控制代碼。 下列呼叫來**SQLTransact**:  
  
```  
SQLTransact(henv, hdbc, fType)  
```  
  
 對應至  
  
```  
SQLEndTran(SQL_HANDLE_DBC, ConnectionHandle, CompletionType);  
```  
  
 如果*ConnectionHandle*不等於 SQL_NULL_HDBC。 *ConnectionHandle*引數設定為值*hdbc*。  
  
 **SQL_Transact**會對應至  
  
```  
SQLEndTran (SQL_HANDLE_ENV, EnvironmentHandle, CompletionType);  
```  
  
 如果*ConnectionHandle*等於 SQL_NULL_HDBC。 *EnvironmentHandle*引數設定為值*henv*。  
  
 在上述所有情況下，這兩*CompletionType*引數設定為相同的值*fType*。
