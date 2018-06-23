---
title: SQLSTATE （ODBC 錯誤碼） |Microsoft 文件
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- SQL Server Native Client ODBC driver, errors
- ODBC error handling, cause information
- messages [ODBC], cause information
- SQLSTATEs
- errors [ODBC], cause information
ms.assetid: 84cce528-edb0-473f-a85f-3eb87fbe2cf3
author: MightyPen
ms.author: genemi
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 6fd38e5eb03e99ad1b2e9385cc3680c227065862
ms.sourcegitcommit: a78fa85609a82e905de9db8b75d2e83257831ad9
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/18/2018
ms.locfileid: "35697169"
---
# <a name="sqlstate-odbc-error-codes"></a>SQLSTATE (ODBC 錯誤碼)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  SQLSTATE 會提供警告或錯誤原因的詳細資訊。 資料中發生的錯誤來源偵測到並傳回由[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client ODBC 驅動程式將傳回的自發性錯誤號碼對應至適當的 SQLSTATE。 如果自發性錯誤號碼沒有要對應至，ODBC 錯誤碼[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Native Client ODBC 驅動程式會傳回 SQLSTATE 42000 （「 語法錯誤或存取違規 」）。 驅動程式時，所偵測到錯誤[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Native Client ODBC 驅動程式會產生適當的 SQLSTATE。  
  
 如需有關狀態錯誤碼的詳細資訊，請查看下列主題：  
  
-   [附錄 A：ODBC 錯誤碼](http://go.microsoft.com/fwlink/?LinkId=89356)  
  
-   [SQLSTATE 對應](http://go.microsoft.com/fwlink/?LinkId=89355)  
  
## <a name="see-also"></a>另請參閱  
 [處理錯誤與訊息](../../relational-databases/native-client-odbc-error-messages/handling-errors-and-messages.md)  
  
  
