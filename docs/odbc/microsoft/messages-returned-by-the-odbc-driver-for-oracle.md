---
title: ODBC Driver for Oracle 所傳回的訊息 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- error messages [ODBC], ODBC driver for Oracle
- ODBC driver for Oracle [ODBC], error messages
ms.assetid: 150bde1d-adb6-4e77-90e9-4dc93499a746
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: b8bdaf4238bd220987364a77aaa1af837885c6e6
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "81298858"
---
# <a name="messages-returned-by-the-odbc-driver-for-oracle"></a>ODBC Driver for Oracle 所傳回的訊息
> [!IMPORTANT]  
>  這項功能將會在未來的 Windows 版本中移除。 請避免在新的開發工作中使用這項功能，並規劃修改目前使用這項功能的應用程式。 請改用 Oracle 所提供的 ODBC 驅動程式。  
  
 如果有可用的 Oracle 錯誤訊息，則會傳回，並在前面加上 [Microsoft]、[ODBC Driver for Oracle] 和 [Oracle] 標記;否則，會傳回不含 [Oracle] 標記的訊息，如下列範例所示：  
  
## <a name="oracle-error-message"></a>Oracle 錯誤訊息：  
  
```  
[Microsoft][ODBC driver for Oracle][Oracle]ORA-nnnnn message-text  
```  
  
## <a name="odbc-driver-for-oracle-error-message"></a>ODBC Driver for Oracle 錯誤訊息：  
  
```  
[Microsoft][ODBC driver for Oracle]  
```
