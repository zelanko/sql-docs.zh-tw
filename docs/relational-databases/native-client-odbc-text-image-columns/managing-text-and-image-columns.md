---
title: 管理文字與影像列 :微軟文件
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
- data types [ODBC], text
- columns [ODBC]
- ODBC data types, image columns
- data types [ODBC], mapping
- ODBC data types, text columns
- image columns [ODBC]
ms.assetid: 7b543556-ff36-4d35-ac08-de96223d92cd
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: d3ac58e59f66dd107a9523a42f5647c90b4fb737
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81297708"
---
# <a name="managing-text-and-image-columns"></a>管理 Text 和 Image 資料行
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]**文本****、ntext**和**圖像**資料(也稱為長數據)是字元或二進位元字串資料類型,可以儲存資料值太大,無法放入**字元****、varchar、****二進位**或**varbinary**列。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]**文字**資料類型對應到 ODBC SQL_LONGVARCHAR資料類型;**ntext**地圖到SQL_WLONGVARCHAR;和**圖像**映射到SQL_LONGVARBINARY。 某些資料項目 (例如長篇的文件或大型的點陣圖) 可能太大，而無法適當地儲存到記憶體中。 若要從[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]順序零件中檢索長資料,[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]本機客戶端 ODBC 驅動程式使應用程式能夠呼叫[SQLGetData](../../relational-databases/native-client-odbc-api/sqlgetdata.md)。 要依順序元件傳送長資料,應用程式可以呼叫[SQLPutData](../../relational-databases/native-client-odbc-api/sqlputdata.md)。 在執行時間傳送資料所使用的參數就是所謂的資料執行中參數。  
  
 應用程序實際上可以使用**SQLPutData**或**SQLGetData**編寫或檢索任何類型的數據(而不僅僅是長數據),儘管只能分批發送或檢索**字元**和**二進位**數據。 但是,如果數據足夠小,可以容納單個緩衝區,則通常沒有理由使用**SQLPutData**或**SQLGetData**。 針對參數或資料行建立單一緩衝區更為容易。  
  
## <a name="in-this-section"></a>本節內容  
  
-   [繫結與未繫結的 Text 和 Image 資料行](../../relational-databases/native-client-odbc-text-image-columns/bound-vs-unbound-text-and-image-columns.md)  
  
-   [已記錄與未記錄的修改](../../relational-databases/native-client-odbc-text-image-columns/logged-vs-unlogged-modifications.md)  
  
-   [資料執行中和 Text、ntext 或 Image 資料行](../../relational-databases/native-client-odbc-text-image-columns/data-at-execution-and-text-ntext-or-image-columns.md)  
  
## <a name="see-also"></a>另請參閱  
 [SQL Server Native Client &#40;ODBC&#41;](../../relational-databases/native-client/odbc/sql-server-native-client-odbc.md)  
  
  
