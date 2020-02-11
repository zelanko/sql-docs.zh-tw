---
title: 錯誤訊息 |Microsoft Docs
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
author: MightyPen
ms.author: genemi
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 10308509004493ba68d23870a70bf878ae05b4a1
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "73783462"
---
# <a name="error-messages"></a>錯誤訊息
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] NATIVE Client ODBC 驅動程式所傳回的訊息文字會放在**SQLGetDiagRec**的*MessageText*參數中。 錯誤的來源會由訊息的標頭指出：  
  
 [Microsoft][ODBC Driver Manager]  
 這些錯誤是由 ODBC 驅動程式管理員所引發。  
  
 [Microsoft][ODBC Cursor Library]  
 這些錯誤是由 ODBC 資料指標程式庫所引發。  
  
 [Microsoft][SQL Server Native Client]  
 這些錯誤是由[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] NATIVE Client ODBC 驅動程式所引發。 如果沒有具有 Net-Library 或 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 名稱的任何其他節點，則驅動程式會發生錯誤。  
  
 Microsoft[SQL Server Native Client][*Net-net-transportname*]  
 這些錯誤是由[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]網路程式庫引發，其中*net net-transportname*是[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]用戶端網路傳輸的顯示名稱（例如，具名管道、共用記憶體、tcp/ip 通訊端或 VIA）。 錯誤訊息的其餘部份則包含呼叫的 Net-Library 函數，以及由 TDS 函數在基礎網路 API 中所呼叫的函數。 這些錯誤所傳回的*pfNative*錯誤碼是來自基礎網路通訊協定堆疊的錯誤碼。  
  
 Microsoft[SQL Server Native Client][ [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]]  
 這些錯誤是由 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 所引發。 錯誤訊息的其餘部分是來自於 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的錯誤訊息文字。 這些錯誤所傳回的*pfNative*程式碼是中[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]的錯誤號碼。 如需可傳回之錯誤訊息（和其數位）清單的詳細資訊[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，請參閱中**master**資料庫內[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **sysmessages**系統資料表的 description 和 error 資料行。  
  
## <a name="see-also"></a>另請參閱  
 [處理錯誤與訊息](../../relational-databases/native-client-odbc-error-messages/handling-errors-and-messages.md)  
  
  
