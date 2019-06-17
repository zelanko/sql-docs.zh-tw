---
title: 針對 Oracle ODBC 驅動程式所傳回的訊息 |Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 4425c814fb8814ec1ef7822d4642ccf6fcc0dd70
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "63026905"
---
# <a name="messages-returned-by-the-odbc-driver-for-oracle"></a>ODBC Driver for Oracle 所傳回的訊息
> [!IMPORTANT]  
>  Windows 的未來版本將移除這項功能。 請避免在新的開發工作中使用這項功能，並規劃修改目前使用這項功能的應用程式。 相反地，使用所提供的 ODBC 驅動程式。  
  
 如果可用的 Oracle 錯誤訊息，它會傳回前面上的 [Microsoft] [ODBC Driver for Oracle，] 和 [Oracle] 標記;否則，訊息會傳回沒有 [Oracle] 標記，如下列範例所示：  
  
## <a name="oracle-error-message"></a>Oracle 錯誤訊息：  
  
```  
[Microsoft][ODBC driver for Oracle][Oracle]ORA-nnnnn message-text  
```  
  
## <a name="odbc-driver-for-oracle-error-message"></a>Oracle 錯誤訊息的 ODBC 驅動程式：  
  
```  
[Microsoft][ODBC driver for Oracle]  
```
