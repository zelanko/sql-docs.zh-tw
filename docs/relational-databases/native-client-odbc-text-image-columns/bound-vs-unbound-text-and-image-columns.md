---
title: 繫結與Text 和 Image 資料行解除繫結 |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
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
- image columns [ODBC]
ms.assetid: ffd3442e-d880-46e9-b848-2365a09a2406
author: MightyPen
ms.author: genemi
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 4e760707c97b9ac45d30b2d94163561324e60db5
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47790969"
---
# <a name="bound-vs-unbound-text-and-image-columns"></a>繫結與未繫結的 Text 和 Image 資料行
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  使用伺服器資料指標，當[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Native Client ODBC 驅動程式已最佳化，不傳送未繫結資料**文字**， **ntext**，或**映像**於資料行時間**SQLFetch**會執行。 **文字**， **ntext**，或**映像**不會實際擷取資料從伺服器應用程式問題直到[SQLGetData](../../relational-databases/native-client-odbc-api/sqlgetdata.md)的資料行。  
  
 可以撰寫許多應用程式，讓沒有**文字**， **ntext**，或**映像**使用者只要向上和向下捲動資料指標中時，會顯示資料。 當使用者選取的資料列，以取得詳細資料時，應用程式可以接著呼叫**SQLGetData**來擷取**文字**， **ntext**，或**映像**資料。 這將會阻止傳送**文字**， **ntext**，或**映像**資料的任何資料列的使用者未選取，並因此可以阻止傳送非常大大量的資料。  
  
## <a name="see-also"></a>另請參閱  
 [管理 Text 和 Image 資料行](../../relational-databases/native-client-odbc-text-image-columns/managing-text-and-image-columns.md)   
 [資料指標行為](../../relational-databases/native-client-odbc-cursors/cursor-behaviors.md)  
  
  
