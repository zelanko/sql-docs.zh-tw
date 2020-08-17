---
description: 資料執行中和 Text、ntext 或 Image 資料行
title: 資料執行中和 Text、Ntext、Image
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- text columns [ODBC]
- SQL Server Native Client ODBC driver, image columns
- SQL Server Native Client ODBC driver, text columns
- data types [ODBC], image
- data types [ODBC], text
- columns [ODBC]
- ODBC data types, image columns
- ODBC data types, text columns
- data-at-execution
- ODBC data-at-execution
- image columns [ODBC]
ms.assetid: 67ffb1a6-f38d-4712-ba64-96bdd41ec2b2
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 9f0faef2097287e026023afe30c379a2f08f3d82
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88381834"
---
# <a name="data-at-execution-and-text-ntext-or-image-columns"></a>資料執行中和 Text、ntext 或 Image 資料行
[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

  ODBC 資料執行中是一種功能，可讓應用程式針對繫結的資料行或參數使用相當大量的資料。 當抓取非常大的 **text**、 **Ntext**或 **image** 資料行時，應用程式可能無法只配置大型緩衝區、將資料行系結至緩衝區，以及提取資料列。 更新非常大的 **text**、 **Ntext**或 **image** 資料行時，應用程式可能無法只配置大型緩衝區、將它系結至 SQL 語句中的參數標記，然後執行語句。 在這些情況下，應用程式必須使用 [SQLGetData](../../relational-databases/native-client-odbc-api/sqlgetdata.md) 或 [SQLPutData](../../relational-databases/native-client-odbc-api/sqlputdata.md) ，以及其資料執行中選項。  
  
## <a name="see-also"></a>另請參閱  
 [管理 Text 和 Image 資料行](../../relational-databases/native-client-odbc-text-image-columns/managing-text-and-image-columns.md)  
  
  
