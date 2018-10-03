---
title: 已記錄與未修改記錄 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- text columns [ODBC]
- SQL Server Native Client ODBC driver, image columns
- SQL Server Native Client ODBC driver, text columns
- data types [ODBC], image
- data types [ODBC], text
- logged vs. nonlogged modifications [SQL Server Native Client]
- columns [ODBC]
- ODBC data types, image columns
- nonlogged vs. logged modifications
- ODBC data types, text columns
- image columns [ODBC]
ms.assetid: 20aa5b27-4a2c-46e7-8356-beb0eebf4b7e
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: c722d5360ad01e7e95508c2219ceb674de381286
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/02/2018
ms.locfileid: "48143908"
---
# <a name="logged-vs-unlogged-modifications"></a>已記錄與未記錄的修改
  應用程式可以要求[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Native Client ODBC 驅動程式不要記錄**文字**， **ntext**，和**映像**修改。 但是在使用這個選項時，應該要特別小心。 它應該僅適用於這兩種情況其中**文字**， **ntext**，或**映像**資料並不重要，而且資料擁有者願意能夠復原資料的取捨較高的效能。  
  
 記錄的記錄**文字**， **ntext**，並**映像**修改會受到呼叫[SQLSetStmtAttr](../native-client-odbc-api/sqlsetstmtattr.md)使用*屬性*參數設定為 SQL_SOPT_SS_ TEXTPTR_LOGGING 以及*ValuePtr*設定為 SQL_TL_ON 或 sql_tl_off 所控制。  
  
## <a name="see-also"></a>另請參閱  
 [管理 Text 和 Image 資料行](managing-text-and-image-columns.md)  
  
  
