---
description: SQLParamData
title: SQLParamData |Microsoft Docs
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
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: f1e81c4e02d0c16caa0cf46d99f731347a639960
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88424000"
---
# <a name="sqlparamdata"></a>SQLParamData
[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

  當 SQLParamData 傳回與資料表值參數相關聯的 *ValuePtrPtr* 時，應用程式應該使用 *StrLen_Or_Ind*來呼叫 SQLPutData。 如果 *StrLen_Or_Ind* 具有大於0的值，則表示應用程式已準備好供 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 原生用戶端收集下一個資料表值參數資料列的參數資料。 如果 *StrLen_Or_Ind* 的值為0，表示資料表值參數沒有其他資料列。 如需詳細資訊，請參閱 [資料表值參數和資料行值的系結和資料傳輸](../../relational-databases/native-client-odbc-table-valued-parameters/binding-and-data-transfer-of-table-valued-parameters-and-column-values.md)。  
  
 如需資料表值參數的詳細資訊，請參閱 [&#40;ODBC&#41;的資料表值參數 ](../../relational-databases/native-client-odbc-table-valued-parameters/table-valued-parameters-odbc.md)。  
  
## <a name="see-also"></a>另請參閱  
 [SQLParamData](https://go.microsoft.com/fwlink/?LinkId=80706)   
 [ODBC API 實作詳細資料](../../relational-databases/native-client-odbc-api/odbc-api-implementation-details.md)  
  
  
