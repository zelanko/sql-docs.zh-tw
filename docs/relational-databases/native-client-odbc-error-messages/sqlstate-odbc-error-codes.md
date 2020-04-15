---
title: SQLSTATE (ODBC 錯誤代碼) |微軟文件
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
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
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 8c7f3fbdf690989830cff2a41028ee0c1e2c9f37
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81291496"
---
# <a name="sqlstate-odbc-error-codes"></a>SQLSTATE (ODBC 錯誤碼)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  SQLSTATE 會提供警告或錯誤原因的詳細資訊。 對於在偵測到與[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]傳回的資料來源中發生[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]的錯誤, 本機客戶端 ODBC 驅動程式將傳回的本機錯誤編號映射到相應的 SQLSTATE。 如果本機錯誤編號沒有要映射到的 ODBC 錯誤[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]代碼, 本機用戶端 ODBC 驅動程式將返回 SQLSTATE 42000("語法錯誤或存取衝突」。 對於驅動程式偵測到的錯誤[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], 本機用戶端 ODBC 驅動程式將生成相應的 SQLSTATE。  
  
 如需有關狀態錯誤碼的詳細資訊，請查看下列主題：  
  
-   [附錄 A：ODBC 錯誤碼](https://go.microsoft.com/fwlink/?LinkId=89356)  
  
-   [SQLSTATE 對應](https://go.microsoft.com/fwlink/?LinkId=89355)  
  
## <a name="see-also"></a>另請參閱  
 [處理錯誤與訊息](../../relational-databases/native-client-odbc-error-messages/handling-errors-and-messages.md)  
  
  
