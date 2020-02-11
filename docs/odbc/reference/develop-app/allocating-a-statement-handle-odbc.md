---
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: d50b0a31aed4935c805ca30620575ccff70d4a0b
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "68077207"
---
# <a name="allocating-a-statement-handle-odbc"></a>配置陳述式控制代碼 ODBC
在應用程式可以執行語句之前，它必須配置語句控制碼，如下所示：  
  
1.  應用程式會宣告 HSTMT 類型的變數。 然後它會呼叫**SQLAllocHandle** ，並傳遞這個變數的位址、要在其中配置語句的連接控制碼，以及 SQL_HANDLE_STMT 選項。 例如：  
  
    ```  
    SQLHSTMT hstmt1;  
  
    SQLAllocHandle(SQL_HANDLE_STMT, hdbc1, &hstmt1);  
    ```  
  
2.  驅動程式管理員會配置用來儲存語句相關資訊的結構，並以 SQL_HANDLE_STMT 選項呼叫驅動程式中的**SQLAllocHandle** 。  
  
3.  驅動程式會配置自己的結構，在其中儲存語句的相關資訊，並將驅動程式語句控制碼傳回給驅動程式管理員。  
  
4.  驅動程式管理員會傳回應用程式變數中應用程式的驅動程式管理員語句控制碼。  
  
 語句控制碼會識別呼叫 ODBC 函數時要使用的語句。 如需語句控制碼的詳細資訊，請參閱[語句控制碼](../../../odbc/reference/develop-app/statement-handles.md)。
