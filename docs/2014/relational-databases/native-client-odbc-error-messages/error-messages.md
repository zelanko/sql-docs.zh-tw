---
title: 錯誤訊息 |Microsoft 文件
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- SQL Server Native Client ODBC driver, errors
- messages [ODBC], types
- ODBC error handling, message types
- errors [ODBC], types
ms.assetid: 46c0c22e-d105-4d5b-bb9d-5694472e8651
caps.latest.revision: 33
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: 2ba9c50f600caf23a6948752ce34e816e493a41b
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36030523"
---
# <a name="error-messages"></a>錯誤訊息
  所傳回的訊息文字[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Native Client ODBC 驅動程式放在*MessageText*參數**SQLGetDiagRec**。 錯誤的來源會由訊息的標頭指出：  
  
 [Microsoft][ODBC Driver Manager]  
 這些錯誤是由 ODBC 驅動程式管理員所引發。  
  
 [Microsoft][ODBC Cursor Library]  
 這些錯誤是由 ODBC 資料指標程式庫所引發。  
  
 [Microsoft][SQL Server Native Client]  
 這些錯誤所引發[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Native Client ODBC 驅動程式。 如果沒有具有 Net-Library 或 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 名稱的任何其他節點，則驅動程式會發生錯誤。  
  
 [Microsoft][SQL Server Native Client][*Net-transportname*]  
 這些錯誤所引發[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]網路程式庫，其中*Net-transportname*是顯示名稱[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]用戶端網路傳輸 （例如，具名管道、 共用記憶體、 TCP/IP 通訊端或 VIA）。 錯誤訊息的其餘部份則包含呼叫的 Net-Library 函數，以及由 TDS 函數在基礎網路 API 中所呼叫的函數。 *PfNative*傳回這些錯誤的錯誤程式碼為基礎的網路通訊協定堆疊的錯誤程式碼。  
  
 [Microsoft][SQL Server Native Client][[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]]  
 這些錯誤是由 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 所引發。 錯誤訊息的其餘部分是來自於 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的錯誤訊息文字。 *PfNative*傳回這些錯誤的程式碼是錯誤中的編號[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。 如需有關的錯誤訊息 （和其數字） 可以傳回的清單[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，請參閱的描述和錯誤資料行**sysmessages**系統資料表中的**主要**資料庫中[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。  
  
## <a name="see-also"></a>另請參閱  
 [處理錯誤與訊息](handling-errors-and-messages.md)  
  
  