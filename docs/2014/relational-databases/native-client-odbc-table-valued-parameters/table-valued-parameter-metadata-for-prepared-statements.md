---
title: 備妥之語句的資料表值參數中繼資料 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- table-valued parameters (ODBC), metadata for prepared statements
ms.assetid: fd2fc705-2e98-4011-9822-c7e6cca4a535
author: rothja
ms.author: jroth
ms.openlocfilehash: ad1394bd5e5bedc69a98308ba67a98434559c146
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/18/2020
ms.locfileid: "84998900"
---
# <a name="table-valued-parameter-metadata-for-prepared-statements"></a>已備妥之陳述式的資料表值參數中繼資料
  應用程式可以透過 SQLNumParams 和 SQLDescribeParam 取得已備妥之程序呼叫的中繼資料。 若為數據表值參數， *DataTypePtr*會設定為 SQL_SS_TABLE。 SQL_CA_SS_TYPE_NAME、SQL_CA_SS_CATALOG_NAME 和 SQL_CA_SS_SCHEMA_NAME 可以透過 SQLGetDescField 取得額外的中繼資料。  
  
 SQL_CA_SS_TYPE_NAME、SQL_CA_SS_CATALOG_NAME 和 SQL_CA_SS_SCHEMA_NAME 可以與 SQLColumns 搭配使用，以取得與資料表值參數相關聯之資料表類型的資料行中繼資料。 在此情況下，在呼叫 SQLColumns 之前，必須將 SQL_SOPT_SS_NAME_SCOPE 設為 SQL_SS_NAME_SCOPE_TABLE_TYPE。 當應用程式完成資料表值參數資料行中繼資料的擷取時，SQL_SOPT_SS_NAME_SCOPE 應該設回預設值 SQL_SS_NAME_SCOPE_TABLE。  
  
 SQL_CA_SS_TYPE_NAME、SQL_CA_SS_CATALOG_NAME 和 SQL_CA_SS_SCHEMA_NAME 也可以搭配 CLR 使用者定義型別參數使用。  
  
 您無法針對不是預存程序呼叫的已備妥陳述式來取得資料表值參數中繼資料。 如果您嘗試這樣做，應用程式會傳回 SQL_ERROR，其中包含 SQLSTATE 42000 和「語法錯誤或違規存取」訊息。  
  
## <a name="see-also"></a>另請參閱  
 [ODBC&#41;&#40;的資料表值參數](table-valued-parameters-odbc.md)  
  
  
