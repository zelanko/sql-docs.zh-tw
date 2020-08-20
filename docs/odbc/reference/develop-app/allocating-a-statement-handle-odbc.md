---
description: 配置陳述式控制代碼 ODBC
title: 配置語句控制碼 ODBC |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQL statements [ODBC], statement handles
- statement handles [ODBC]
- allocating statement handles [ODBC]
- handles [ODBC], statement
ms.assetid: 4ce3b446-34ab-46dc-96e5-f40ec95c267e
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 624490beee55c7fa37346087fc85b560904f6b93
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88487541"
---
# <a name="allocating-a-statement-handle-odbc"></a>配置陳述式控制代碼 ODBC
在應用程式可以執行語句之前，它必須配置語句控制碼，如下所示：  
  
1.  應用程式會宣告 HSTMT 型別的變數。 然後，它會呼叫 **SQLAllocHandle** ，並傳遞這個變數的位址、要在其中配置語句的連接控制碼，以及 SQL_HANDLE_STMT 選項。 例如：  
  
    ```  
    SQLHSTMT hstmt1;  
  
    SQLAllocHandle(SQL_HANDLE_STMT, hdbc1, &hstmt1);  
    ```  
  
2.  驅動程式管理員會配置用來儲存語句相關資訊的結構，並使用 SQL_HANDLE_STMT 選項來呼叫驅動程式中的 **SQLAllocHandle** 。  
  
3.  驅動程式會配置自己的結構來儲存語句的相關資訊，並將驅動程式語句控制碼傳回驅動程式管理員。  
  
4.  驅動程式管理員會將驅動程式管理員語句控制碼傳回到應用程式變數中的應用程式。  
  
 語句控制碼會識別呼叫 ODBC 函數時要使用的語句。 如需語句控制碼的詳細資訊，請參閱 [語句控制碼](../../../odbc/reference/develop-app/statement-handles.md)。
