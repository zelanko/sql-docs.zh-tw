---
title: 使用檔案資料來源連線 :微軟文件
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 8c752fc3b09c06c68dcc216cacac63744dc3101b
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81287408"
---
# <a name="connecting-using-file-data-sources"></a>使用檔案資料來源進行連線
檔案資料來源的連線資訊儲存在 .dsn 檔中。 因此,連接字串可以由單個用戶重複使用,也可以在多個用戶之間共用(如果他們安裝了適當的驅動程式)。 這個檔案包含驅動程式名稱(或無法分享檔案資料來源時的另一個資料來源名稱),以及可選擇的連接字串,該字串可用於**SQLDriverConnect**。 驅動程式管理員從 .dsn 檔案中的關鍵字建構對**SQLDriverConnect**呼叫的連接字串。  
  
 檔案資料來源允許應用程式指定連接選項,而無需建構用於**SQLDriverConnect**的連接字串。 檔案資料來源通常是透過指定**SAVEFILE**關鍵字建立的,該關鍵字會導致驅動程式管理員儲存由呼叫**SQLDriverConnect**到 .dsn 檔案的輸出連接字串。 可以通過使用**FILEDSN**關鍵字調用**SQLDriverConnect**來重複使用該連接字串。 這簡化了連接過程,並提供了連接字串的持久源。  
  
 還可以通過在安裝程式 DLL 中調用**SQLCreateDataSource**來創建檔案數據來源。 資訊可以通過調用**SQLWriteFileDSN**寫入 .dsn 檔,並透過呼叫**SQLReadFileDSN**從 .dsn 檔中讀取;這兩個函數也在安裝程式 DLL 中。 有關安裝程式 DLL 的資訊,請參考[設定資料來源](../../../odbc/reference/install/configuring-data-sources.md)。  
  
 用於連接資訊的關鍵字位於 .dsn 檔的 [ODBC] 部分。 可分享 .dsn 檔案在 [ODBC] 部分中將具有的最小資訊是 DRIVER 關鍵字:  
  
```  
DRIVER = SQL Server  
```  
  
 可分享的 .dsn 檔案通常包含連接字串,如下所示:  
  
```  
DRIVER = SQL Server  
UID = Larry  
DATABASE = MyDB  
```  
  
 當檔案資料來源不可分享時,.dsn 檔僅包含**DSN**關鍵字。 當驅動程式管理員在不可共用的文件數據來源中發送資訊時,它將根據需要連接到**DSN**關鍵字指示的數據來源。 無法分享的 .dsn 檔案將包含以下關鍵字:  
  
```  
DSN = MyDataSource  
```  
  
 用於檔案資料來源的連接字串是 .dsn 檔中指定的關鍵字和調用**SQLDriverConnect**中的連接字串中指定的關鍵字的合併。 如果 .dsn 檔中的任何關鍵字與連接字串中的關鍵字衝突,驅動程式管理器將決定應使用哪個關鍵字值。 有關詳細資訊,請參閱[SQLDriverConnect](../../../odbc/reference/syntax/sqldriverconnect-function.md)。  
  
## <a name="see-also"></a>另請參閱  
 [https://support.microsoft.com/kb/165866](https://support.microsoft.com/kb/165866)
