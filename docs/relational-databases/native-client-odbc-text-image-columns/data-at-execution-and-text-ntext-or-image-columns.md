---
title: 資料在執行和 Text、 ntext 或 Image 資料行 |Microsoft 文件
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.component: native-client-odbc-text-image-columns
ms.reviewer: ''
ms.suite: sql
ms.technology: ''
ms.tgt_pltfrm: ''
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
caps.latest.revision: 29
author: MightyPen
ms.author: genemi
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 54889e3ae30bb0fb3d2b7f08dfba542ae771ce24
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="data-at-execution-and-text-ntext-or-image-columns"></a>資料執行中和 Text、ntext 或 Image 資料行
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  ODBC 資料執行中是一種功能，可讓應用程式針對繫結的資料行或參數使用相當大量的資料。 當擷取非常大**文字**， **ntext**，或**映像**資料行，應用程式可能無法只配置大型緩衝區、 資料行繫結到緩衝區，和擷取資料列。 當更新非常大**文字**， **ntext**，或**映像**資料行，應用程式可能無法只配置大型緩衝區、 將它繫結至在 SQL 中的參數標記陳述式，然後執行陳述式。 在這些情況下，應用程式必須使用[SQLGetData](../../relational-databases/native-client-odbc-api/sqlgetdata.md)或[SQLPutData](../../relational-databases/native-client-odbc-api/sqlputdata.md)其資料在執行選項。  
  
## <a name="see-also"></a>另請參閱  
 [管理 Text 和 Image 資料行](../../relational-databases/native-client-odbc-text-image-columns/managing-text-and-image-columns.md)  
  
  
