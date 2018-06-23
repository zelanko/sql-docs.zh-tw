---
title: SQLParamData |Microsoft 文件
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- SQLParamData function
ms.assetid: 92349482-ea22-4a6a-8484-e9c6566794fa
caps.latest.revision: 10
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: bd3fefeaa05f806650b58d1778658fda0ed63fa2
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36036574"
---
# <a name="sqlparamdata"></a>SQLParamData
  當傳回 SQLParamData *ValuePtrPtr*資料表值參數相關聯，應用程式應該呼叫與 SQLPutData *StrLen_Or_Ind*。 如果*StrLen_Or_Ind*的值大於 0，則表示應用程式可供[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Native Client 蒐集下一個資料表值參數資料列的參數資料。 如果*StrLen_Or_Ind*的值為 0，表示沒有多個資料列的資料表值參數資料。 如需詳細資訊，請參閱[繫結和 Data Transfer of Table-Valued 參數和資料行值](../native-client-odbc-table-valued-parameters/binding-and-data-transfer-of-table-valued-parameters-and-column-values.md)。  
  
 如需有關資料表值參數的詳細資訊，請參閱[資料表值參數&#40;ODBC&#41;](../native-client-odbc-table-valued-parameters/table-valued-parameters-odbc.md)。  
  
## <a name="see-also"></a>另請參閱  
 [SQLParamData](http://go.microsoft.com/fwlink/?LinkId=80706)   
 [ODBC API 實作詳細資料](odbc-api-implementation-details.md)  
  
  