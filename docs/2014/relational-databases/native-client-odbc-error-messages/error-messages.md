---
title: 錯誤訊息 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- SQL Server Native Client ODBC driver, errors
- messages [ODBC], types
- ODBC error handling, message types
- errors [ODBC], types
ms.assetid: 46c0c22e-d105-4d5b-bb9d-5694472e8651
author: rothja
ms.author: jroth
ms.openlocfilehash: d004ba320b50896b6f57c5de335d7f7b3d33e87a
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/18/2020
ms.locfileid: "85020039"
---
# <a name="error-messages"></a>錯誤訊息
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Native CLIENT ODBC 驅動程式所傳回的訊息文字會放在**SQLGetDiagRec**的*MessageText*參數中。 錯誤的來源會由訊息的標頭指出：  
  
 [Microsoft][ODBC Driver Manager]  
 這些錯誤是由 ODBC 驅動程式管理員所引發。  
  
 [Microsoft][ODBC Cursor Library]  
 這些錯誤是由 ODBC 資料指標程式庫所引發。  
  
 [Microsoft][SQL Server Native Client]  
 這些錯誤是由 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native CLIENT ODBC 驅動程式所引發。 如果沒有具有 Net-Library 或 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 名稱的任何其他節點，則驅動程式會發生錯誤。  
  
 Microsoft[SQL Server Native Client][*Net-net-transportname*]  
 這些錯誤是由網路連結 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 庫引發，其中*net net-transportname*是 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 用戶端網路傳輸的顯示名稱（例如，具名管道、共用記憶體、TCP/IP 通訊端或 VIA）。 錯誤訊息的其餘部份則包含呼叫的 Net-Library 函數，以及由 TDS 函數在基礎網路 API 中所呼叫的函數。 這些錯誤所傳回的*pfNative*錯誤碼是來自基礎網路通訊協定堆疊的錯誤碼。  
  
 [Microsoft][SQL Server Native Client][[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]]  
 這些錯誤是由 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 所引發。 錯誤訊息的其餘部分是來自於 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的錯誤訊息文字。 這些錯誤所傳回的*pfNative*程式碼是中的錯誤號碼 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 。 如需可傳回之錯誤訊息（和其數位）清單的詳細資訊 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ，請參閱中**master**資料庫內**sysmessages**系統資料表的 description 和 error 資料行 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 。  
  
## <a name="see-also"></a>另請參閱  
 [處理錯誤與訊息](handling-errors-and-messages.md)  
  
  
