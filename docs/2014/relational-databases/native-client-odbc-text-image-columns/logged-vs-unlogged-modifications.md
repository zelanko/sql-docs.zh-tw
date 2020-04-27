---
title: 已記錄與未記錄的修改 |Microsoft Docs
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
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/26/2020
ms.locfileid: "63195141"
---
# <a name="logged-vs-unlogged-modifications"></a>已記錄與未記錄的修改
  應用程式[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]可以要求 NATIVE Client ODBC 驅動程式不會記錄**text**、 **Ntext**和**image**修改。 但是在使用這個選項時，應該要特別小心。 只有當**text**、 **Ntext**或**image**資料不重要，而且資料擁有者願意將復原資料的能力視為較高的效能時，才應該使用此功能。  
  
 **Text**、 **Ntext**和**image**修改的記錄是藉由呼叫[SQLSetStmtAttr](../native-client-odbc-api/sqlsetstmtattr.md) ，並將*Attribute*參數設定為 SQL_SOPT_SS_ TEXTPTR_LOGGING，並將*valueptr 是*設定為 SQL_TL_ON 或 SQL_TL_OFF 來控制。  
  
## <a name="see-also"></a>另請參閱  
 [管理 Text 和 Image 資料行](managing-text-and-image-columns.md)  
  
  
