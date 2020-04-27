---
title: SQLSTATE （ODBC 錯誤碼） |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
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
ms.openlocfilehash: 253841e26ab7ecbeafb2cfeeed8c090c91650d14
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/26/2020
ms.locfileid: "62805862"
---
# <a name="sqlstate-odbc-error-codes"></a>SQLSTATE (ODBC 錯誤碼)
  SQLSTATE 會提供警告或錯誤原因的詳細資訊。 對於偵測到並傳回的資料來源發生的錯誤[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client ODBC 驅動程式會將傳回的原生錯誤號碼對應至適當的 SQLSTATE。 如果原生錯誤號碼沒有要對應的 ODBC 錯誤碼， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] NATIVE Client ODBC 驅動程式會傳回 SQLSTATE 42000 （「語法錯誤或存取違規」）。 對於驅動程式所偵測到的錯誤， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] NATIVE Client ODBC 驅動程式會產生適當的 SQLSTATE。  
  
 如需有關狀態錯誤碼的詳細資訊，請查看下列主題：  
  
-   [附錄 A：ODBC 錯誤碼](https://go.microsoft.com/fwlink/?LinkId=89356)  
  
-   [SQLSTATE 對應](https://go.microsoft.com/fwlink/?LinkId=89355)  
  
## <a name="see-also"></a>另請參閱  
 [處理錯誤與訊息](handling-errors-and-messages.md)  
  
  
