---
title: 錯誤消息 |微軟文件
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- SQL Server Native Client ODBC driver, errors
- messages [ODBC], types
- ODBC error handling, message types
- errors [ODBC], types
ms.assetid: 46c0c22e-d105-4d5b-bb9d-5694472e8651
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 7d632d1d22cd8439a3d787e22301ec06ec4e0d93
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81291711"
---
# <a name="error-messages"></a>錯誤訊息
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]本機用戶端 ODBC 驅動程式傳回的消息文字放置在**SQLGetDiagRec**的*MessageText*參數中。 錯誤的來源會由訊息的標頭指出：  
  
 [Microsoft][ODBC Driver Manager]  
 這些錯誤是由 ODBC 驅動程式管理員所引發。  
  
 [Microsoft][ODBC Cursor Library]  
 這些錯誤是由 ODBC 資料指標程式庫所引發。  
  
 [Microsoft][SQL Server Native Client]  
 這些錯誤由[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]本機用戶端ODBC驅動程式引發。 如果沒有具有 Net-Library 或 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 名稱的任何其他節點，則驅動程式會發生錯誤。  
  
 [微軟][SQL 伺服器本機用戶端][*淨傳送名稱*】  
 這些錯誤由[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Net-函式庫引發,其中[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]*Net 傳輸名稱*是 用戶端網路傳輸的顯示名稱(例如,命名管道、共用記憶體、TCP/IP 套接字或 VIA)。 錯誤訊息的其餘部份則包含呼叫的 Net-Library 函數，以及由 TDS 函數在基礎網路 API 中所呼叫的函數。 隨這些錯誤返回的*pfNative*錯誤代碼是基礎網路協定堆疊中的錯誤代碼。  
  
 [微軟][SQL 伺服器本機用戶端][ [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]]  
 這些錯誤是由 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 所引發。 錯誤訊息的其餘部分是來自於 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的錯誤訊息文字。 隨這些錯誤返回的*pfNative*代碼是[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]從 中傳回的錯誤編號。 有關 可以[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]返回的錯誤消息清單(及其編號)的詳細資訊,請參閱**master**[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]中 主資料庫中**sysmessages**系統表的說明和錯誤列。  
  
## <a name="see-also"></a>另請參閱  
 [處理錯誤與訊息](../../relational-databases/native-client-odbc-error-messages/handling-errors-and-messages.md)  
  
  
