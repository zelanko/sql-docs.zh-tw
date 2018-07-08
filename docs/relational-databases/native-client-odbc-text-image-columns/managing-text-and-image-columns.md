---
title: 管理 Text 和 Image 資料行 |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.suite: sql
ms.technology: native-client
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- text columns [ODBC]
- SQL Server Native Client ODBC driver, image columns
- SQL Server Native Client ODBC driver, text columns
- data types [ODBC], text
- columns [ODBC]
- ODBC data types, image columns
- data types [ODBC], mapping
- ODBC data types, text columns
- image columns [ODBC]
ms.assetid: 7b543556-ff36-4d35-ac08-de96223d92cd
author: MightyPen
ms.author: genemi
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: f17ef47c7d6653f6389ace37d2a4f3f39f006b76
ms.sourcegitcommit: f8ce92a2f935616339965d140e00298b1f8355d7
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/03/2018
ms.locfileid: "37432557"
---
# <a name="managing-text-and-image-columns"></a>管理 Text 和 Image 資料行
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **文字**， **ntext**，以及**映像**資料 （也稱為 long 資料） 是字元或二進位字串資料類型，可保留資料值太大而無法放入**char**， **varchar**，**二進位**，或**varbinary**資料行。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **文字**資料類型會對應到 ODBC SQL_LONGVARCHAR 資料類型;**ntext**對應到 SQL_WLONGVARCHAR; 並**映像**對應到 SQL_LONGVARBINARY。 某些資料項目 (例如長篇的文件或大型的點陣圖) 可能太大，而無法適當地儲存到記憶體中。 若要擷取 long 資料，從[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]循序分批[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Native Client ODBC 驅動程式可讓應用程式呼叫[SQLGetData](../../relational-databases/native-client-odbc-api/sqlgetdata.md)。 若要傳送循序部分的 long 資料，應用程式可以呼叫[SQLPutData](../../relational-databases/native-client-odbc-api/sqlputdata.md)。 在執行時間傳送資料所使用的參數就是所謂的資料執行中參數。  
  
 應用程式可以實際寫入或擷取任何類型的資料 （不只是 long 資料） 與**SQLPutData**或是**SQLGetData**，但只有**字元**和**二進位**可傳送或擷取部分資料。 不過，如果資料夠小，無法放入單一緩衝區中，有通常是使用沒有理由**SQLPutData**或是**SQLGetData**。 針對參數或資料行建立單一緩衝區更為容易。  
  
## <a name="in-this-section"></a>本節內容  
  
-   [繫結與未繫結的 Text 和 Image 資料行](../../relational-databases/native-client-odbc-text-image-columns/bound-vs-unbound-text-and-image-columns.md)  
  
-   [已記錄與未記錄的修改](../../relational-databases/native-client-odbc-text-image-columns/logged-vs-unlogged-modifications.md)  
  
-   [資料執行中和 Text、ntext 或 Image 資料行](../../relational-databases/native-client-odbc-text-image-columns/data-at-execution-and-text-ntext-or-image-columns.md)  
  
## <a name="see-also"></a>另請參閱  
 [SQL Server Native Client &#40;ODBC&#41;](../../relational-databases/native-client/odbc/sql-server-native-client-odbc.md)  
  
  
