---
title: SQLParamData | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- SQLParamData function
ms.assetid: 92349482-ea22-4a6a-8484-e9c6566794fa
author: MightyPen
ms.author: genemi
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: d105b09c94f75ee7ab2317c601c63efda405d682
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/15/2019
ms.locfileid: "68131257"
---
# <a name="sqlparamdata"></a>SQLParamData
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  當傳回 SQLParamData *ValuePtrPtr*相關聯的資料表值參數，應用程式應該呼叫與 SQLPutData *Strlen_or_ind&lt*。 如果*Strlen_or_ind&lt*的值大於 0，這表示應用程式可供[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]蒐集下一個資料表值參數資料列的參數資料的原生用戶端。 如果*Strlen_or_ind&lt*其值為 0，表示沒有更多資料列的資料表值參數資料。 如需詳細資訊，請參閱 <<c0> [ 繫結和 Data Transfer of Table-Valued 參數和資料行值](../../relational-databases/native-client-odbc-table-valued-parameters/binding-and-data-transfer-of-table-valued-parameters-and-column-values.md)。  
  
 如需有關資料表值參數的詳細資訊，請參閱 < [Parameters &#40;ODBC&#41;](../../relational-databases/native-client-odbc-table-valued-parameters/table-valued-parameters-odbc.md)。  
  
## <a name="see-also"></a>另請參閱  
 [SQLParamData](https://go.microsoft.com/fwlink/?LinkId=80706)   
 [ODBC API 實作詳細資料](../../relational-databases/native-client-odbc-api/odbc-api-implementation-details.md)  
  
  
