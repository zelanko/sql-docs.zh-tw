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
ms.openlocfilehash: b2082a97b24284afcc879048bb08e86a7b2bb3ba
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/15/2019
ms.locfileid: "68070115"
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
