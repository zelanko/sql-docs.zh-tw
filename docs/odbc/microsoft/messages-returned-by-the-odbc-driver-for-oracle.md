---
title: 由 Oracle 的 ODBC 驅動程式傳回的消息 |微軟文件
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
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81298858"
---
# <a name="messages-returned-by-the-odbc-driver-for-oracle"></a>ODBC Driver for Oracle 所傳回的訊息
> [!IMPORTANT]  
>  此功能將在將來版本的 Windows 中刪除。 請避免在新的開發工作中使用這項功能，並規劃修改目前使用這項功能的應用程式。 而是使用 Oracle 提供的 ODBC 驅動程式。  
  
 如果 Oracle 錯誤訊息可用,則將在 [Microsoft]、[Oracle 的 ODBC 驅動程式]和 [Oracle] 標記之前返回該錯誤消息;否則,返回消息時沒有 [Oracle] 標記,如以下範例所示:  
  
## <a name="oracle-error-message"></a>Oracle 錯誤訊息:  
  
```  
[Microsoft][ODBC driver for Oracle][Oracle]ORA-nnnnn message-text  
```  
  
## <a name="odbc-driver-for-oracle-error-message"></a>Oracle 錯誤訊息的 ODBC 驅動程式:  
  
```  
[Microsoft][ODBC driver for Oracle]  
```
