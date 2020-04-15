---
title: 繫結與未結合文字與影像列 |微軟文件
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
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 0cfa05f7019342d63ab6f3092c3b6df5ae6e8daa
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81297730"
---
# <a name="bound-vs-unbound-text-and-image-columns"></a>繫結與未繫結的 Text 和 Image 資料行
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  使用伺服器游標時,[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]本機用戶端 ODBC 驅動程式經過最佳化,以在執行**SQLFetch**時不傳輸未綁定**文本****、ntext**或**圖像**列的數據。 在應用程式為列發出[SQLGetData](../../relational-databases/native-client-odbc-api/sqlgetdata.md)之前,實際上不會從伺服器檢索**文本****、ntext**或**圖像**數據。  
  
 可以編寫許多應用程式,以便在使用者只是在游標中上下滾動時不顯示**文本****、ntext**或**圖像**資料。 當用戶選擇一行以獲取更多詳細資訊時,應用程式可以調用**SQLGetData**來檢索**文本****、ntext**或**圖像**數據。 這將防止為使用者未選擇的任何行傳輸**文本****、ntext**或**圖像**數據,因此可以防止傳輸大量數據。  
  
## <a name="see-also"></a>另請參閱  
 [管理文字與影像欄位](../../relational-databases/native-client-odbc-text-image-columns/managing-text-and-image-columns.md)   
 [資料指標行為](../../relational-databases/native-client-odbc-cursors/cursor-behaviors.md)  
  
  
