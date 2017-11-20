---
title: "使用檔案資料來源連接 |Microsoft 文件"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.reviewer: 
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- connecting to driver [ODBC], file data sources
- SQLDriverConnect function [ODBC], connecting using file data sources
- connecting to data source [ODBC], SQLDriverConnect
- connecting to driver [ODBC], SQLDriverConnect
- connecting to data source [ODBC], file data sources
- file data sources [ODBC]
ms.assetid: 3003f8c2-8be6-41cc-8d9c-612e9bd0f3ae
caps.latest.revision: 7
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 5f8a5d949127e7ad87866a0272fbd285fe12ceed
ms.contentlocale: zh-tw
ms.lasthandoff: 09/09/2017

---
# <a name="connecting-using-file-data-sources"></a>使用檔案資料來源連接
檔案資料來源的連接資訊儲存在.dsn 檔案。 如此一來，連接字串可以重複使用由單一使用者，或如果他們已安裝適當的驅動程式，在數個使用者之間共用。 檔案包含驅動程式名稱 （或在自檔案資料來源的情況下的另一個資料來源名稱） 與 （選擇性） 的連接字串，可供**SQLDriverConnect**。 驅動程式管理員建置連接字串呼叫**SQLDriverConnect**從.dsn 檔案中的關鍵字。  
  
 檔案資料來源可讓應用程式指定連接選項，而不需要建立的連接字串，搭配**SQLDriverConnect**。 檔案建立資料來源通常是藉由指定**SAVEFILE**關鍵字，會致使呼叫所建立的輸出連接字串儲存驅動程式管理員在**SQLDriverConnect** .dsn 檔案。 連接字串可以重複使用藉由呼叫**SQLDriverConnect**與**FILEDSN**關鍵字。 這可簡化連線程序，並提供持續性連接字串的來源。  
  
 檔案建立資料來源也可以藉由呼叫**SQLCreateDataSource**安裝程式 DLL 中。 資訊可以藉由呼叫寫入到.dsn 檔案**SQLWriteFileDSN**，並藉由呼叫讀取.dsn 檔案**SQLReadFileDSN**; 這兩個函數也會在安裝程式 DLL。 如需安裝程式 DLL 的資訊，請參閱[設定資料來源](../../../odbc/reference/install/configuring-data-sources.md)。  
  
 連接資訊所用的關鍵字是.dsn 檔案的 [ODBC] 區段中。 可共用.dsn 檔案會有 [ODBC] 區段中的最少資訊是 DRIVER 關鍵字：  
  
```  
DRIVER = SQL Server  
```  
  
 可共用.dsn 檔案通常包含連接字串，如下：  
  
```  
DRIVER = SQL Server  
UID = Larry  
DATABASE = MyDB  
```  
  
 自檔案資料來源時，只包含.dsn 檔案**DSN**關鍵字。 當驅動程式管理員會將資訊傳送自檔案資料來源中時，連接視所指示的資料來源**DSN**關鍵字。 自.dsn 檔案會包含下列關鍵字：  
  
```  
DSN = MyDataSource  
```  
  
 用於檔案資料來源的連接字串是.dsn 檔案中指定的關鍵字和連接字串，在呼叫中指定關鍵字的等位**SQLDriverConnect**。 如果任何.dsn 檔案中的關鍵字衝突與連接字串中的關鍵字，驅動程式管理員會決定要使用的關鍵字值。 如需詳細資訊，請參閱[SQLDriverConnect](../../../odbc/reference/syntax/sqldriverconnect-function.md)。  
  
## <a name="see-also"></a>另請參閱  
 [http://support.microsoft.com/kb/165866](http://support.microsoft.com/kb/165866)

