---
title: 使用檔案資料來源連線 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- connecting to driver [ODBC], file data sources
- SQLDriverConnect function [ODBC], connecting using file data sources
- connecting to data source [ODBC], SQLDriverConnect
- connecting to driver [ODBC], SQLDriverConnect
- connecting to data source [ODBC], file data sources
- file data sources [ODBC]
ms.assetid: 3003f8c2-8be6-41cc-8d9c-612e9bd0f3ae
author: MightyPen
ms.author: genemi
ms.openlocfilehash: aa340c64f6eb92d803d8918bc99ecf112b19f1e7
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/15/2019
ms.locfileid: "68083110"
---
# <a name="connecting-using-file-data-sources"></a>使用檔案資料來源進行連線
檔案資料來源的連接資訊儲存在.dsn 檔案。 如此一來，連接字串可以是一位使用者重複使用或有適當的驅動程式安裝數個使用者共用。 檔案包含驅動程式名稱 （或在自檔案資料來源的情況下的另一個資料來源名稱） 和 （選擇性） 連接字串，可供**SQLDriverConnect**。 驅動程式管理員建置呼叫的連接字串**SQLDriverConnect**從.dsn 檔案中的關鍵字。  
  
 檔案資料來源可讓應用程式指定連接選項，而不需要建置搭配使用的連接字串**SQLDriverConnect**。 檔案建立資料來源通常是藉由指定**SAVEFILE**關鍵字，這會導致驅動程式管理員，若要儲存的呼叫所建立的輸出連接字串**SQLDriverConnect** .dsn 檔案。 連接字串可以重複使用藉由呼叫**SQLDriverConnect**具有**FILEDSN**關鍵字。 這可簡化連線程序，並提供持續性來源的連接字串。  
  
 檔案資料來源也可以建立藉由呼叫**SQLCreateDataSource**安裝程式 DLL 中。 藉由呼叫資訊寫入至.dsn 檔案**SQLWriteFileDSN**，並藉由呼叫讀取.dsn 檔案**SQLReadFileDSN**; 兩個函數也會在安裝程式 DLL。 如需安裝程式 DLL 的資訊，請參閱[設定資料來源](../../../odbc/reference/install/configuring-data-sources.md)。  
  
 輸入連接資訊所用的關鍵字是.dsn 檔案的 [ODBC] 區段中。 可共用.dsn 檔案會有 [ODBC] 區段中的最少資訊是 DRIVER 關鍵字：  
  
```  
DRIVER = SQL Server  
```  
  
 可共用.dsn 檔案通常包含連接字串，如下：  
  
```  
DRIVER = SQL Server  
UID = Larry  
DATABASE = MyDB  
```  
  
 .Dsn 檔案是非共用檔案資料來源時，只包含**DSN**關鍵字。 當驅動程式管理員會將資訊傳送自檔案資料來源中時，連接視所指示的資料來源**DSN**關鍵字。 留駐.dsn 檔案會包含下列關鍵字：  
  
```  
DSN = MyDataSource  
```  
  
 用於檔案資料來源的連接字串是.dsn 檔案中指定的關鍵字和連接字串，在呼叫中指定關鍵字的等位**SQLDriverConnect**。 如果任何.dsn 檔案中的關鍵字衝突與連接字串中的關鍵字，驅動程式管理員會決定應該使用哪一個關鍵字值。 如需詳細資訊，請參閱 < [SQLDriverConnect](../../../odbc/reference/syntax/sqldriverconnect-function.md)。  
  
## <a name="see-also"></a>另請參閱  
 [https://support.microsoft.com/kb/165866](https://support.microsoft.com/kb/165866)
