---
title: 已備妥的陳述式資料表值參數中繼資料 |Microsoft 文件
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
- table-valued parameters (ODBC), metadata for prepared statements
ms.assetid: fd2fc705-2e98-4011-9822-c7e6cca4a535
caps.latest.revision: 13
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: 8bc66cb8c74a4e256e57f90d6180fc0acdd790b4
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36135379"
---
# <a name="table-valued-parameter-metadata-for-prepared-statements"></a>已備妥之陳述式的資料表值參數中繼資料
  應用程式可以取得透過 SQLNumParams 和 SQLDescribeParam 備妥的程序呼叫的中繼資料。 資料表值參數， *DataTypePtr*設定為 SQL_SS_TABLE。 其他中繼資料可透過 SQL_CA_SS_TYPE_NAME、 SQL_CA_SS_CATALOG_NAME 和 SQL_CA_SS_SCHEMA_NAME 的 SQLGetDescField。  
  
 SQL_CA_SS_TYPE_NAME、 SQL_CA_SS_CATALOG_NAME 和 SQL_CA_SS_SCHEMA_NAME 可以用於 SQLColumns 取得資料表值參數相關聯的資料表類型的資料行中繼資料。 在此情況下，SQL_SOPT_SS_NAME_SCOPE 必須設定為 SQL_SS_NAME_SCOPE_TABLE_TYPE SQLColumns 呼叫之前。 當應用程式完成資料表值參數資料行中繼資料的擷取時，SQL_SOPT_SS_NAME_SCOPE 應該設回預設值 SQL_SS_NAME_SCOPE_TABLE。  
  
 SQL_CA_SS_TYPE_NAME、SQL_CA_SS_CATALOG_NAME 和 SQL_CA_SS_SCHEMA_NAME 也可以搭配 CLR 使用者定義型別參數使用。  
  
 您無法針對不是預存程序呼叫的已備妥陳述式來取得資料表值參數中繼資料。 如果您嘗試這樣做，應用程式會傳回 SQL_ERROR，其中包含 SQLSTATE 42000 和「語法錯誤或違規存取」訊息。  
  
## <a name="see-also"></a>另請參閱  
 [資料表值參數&#40;ODBC&#41;](table-valued-parameters-odbc.md)  
  
  