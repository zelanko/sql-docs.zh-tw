---
title: SQLParamData | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- SQLParamData function
ms.assetid: 92349482-ea22-4a6a-8484-e9c6566794fa
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 79285523ec83d3f10ad6f23010a7f9a6398e5980
ms.sourcegitcommit: a1adc6906ccc0a57d187e1ce35ab7a7a951ebff8
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/09/2019
ms.locfileid: "68890103"
---
# <a name="sqlparamdata"></a>SQLParamData
  當 SQLParamData 傳回與資料表值參數相關聯的*ValuePtrPtr*時, 應用程式應該使用*StrLen_Or_Ind*呼叫 SQLPutData。 如果*StrLen_Or_Ind*的值大於 0, 則表示應用程式已準備好讓[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client 收集下一個資料表值參數資料列的參數資料。 如果*StrLen_Or_Ind*的值為 0, 表示資料表值參數沒有更多資料列。 如需詳細資訊, 請參閱[資料表值參數和資料行值的系結和資料傳輸](../native-client-odbc-table-valued-parameters/binding-and-data-transfer-of-table-valued-parameters-and-column-values.md)。  
  
 如需資料表值參數的詳細資訊, 請參閱[資料表值參數&#40;ODBC&#41;](../native-client-odbc-table-valued-parameters/table-valued-parameters-odbc.md)。  
  
## <a name="see-also"></a>另請參閱  
 [SQLParamData](/sql/odbc/reference/syntax/sqlparamdata-function)   
 [ODBC API 實作詳細資料](odbc-api-implementation-details.md)  
  
  
