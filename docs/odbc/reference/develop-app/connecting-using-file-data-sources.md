---
description: 使用檔案資料來源進行連線
title: 使用檔案資料來源連接 |Microsoft Docs
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
ms.openlocfilehash: 0ab210a77d1d6516b6b54ba25767d859ff9102fb
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88476760"
---
# <a name="connecting-using-file-data-sources"></a>使用檔案資料來源進行連線
檔案資料來源的連接資訊會儲存在 dsn 檔案中。 如此一來，如果使用者已安裝適當的驅動程式，則單一使用者可以重複使用連接字串，或在數個使用者之間共用連接字串。 檔案包含驅動程式名稱 (或另一個資料來源名稱（如果是 unshareable 檔案資料來源) ），並選擇性地包含可供 **SQLDriverConnect**使用的連接字串。 驅動程式管理員會從 dsn 檔案中的關鍵字，建立呼叫 **SQLDriverConnect** 的連接字串。  
  
 檔案資料來源可讓應用程式指定連接選項，而不需要建立連接字串來與 **SQLDriverConnect**搭配使用。 檔案資料來源通常是藉由指定 **SAVEFILE** 關鍵字來建立的，這會導致驅動程式管理員將 **SQLDriverConnect** 呼叫所建立的輸出連接字串儲存至 .dsn 檔。 您可以使用**FILEDSN**關鍵字來呼叫**SQLDriverConnect** ，以重複使用該連接字串。 這可簡化連接程式，並提供連接字串的持續性來源。  
  
 您也可以在安裝程式 DLL 中呼叫 **SQLCreateDataSource** 來建立檔案資料來源。 您可以藉由呼叫 **SQLWriteFileDSN**來將資訊寫入至 dsn 檔案，並藉由呼叫 **SQLReadFileDSN**來讀取該 dsn 檔案;這兩個函式也都在安裝程式 DLL 中。 如需安裝程式 DLL 的詳細資訊，請參閱設定 [資料來源](../../../odbc/reference/install/configuring-data-sources.md)。  
  
 連接資訊所使用的關鍵字位於 dsn 檔案的 [ODBC] 區段中。 在 [ODBC] 區段中，可共用的 .dsn 檔案所含的最小資訊是 DRIVER 關鍵字：  
  
```  
DRIVER = SQL Server  
```  
  
 可共用的 .dsn 檔案通常包含連接字串，如下所示：  
  
```  
DRIVER = SQL Server  
UID = Larry  
DATABASE = MyDB  
```  
  
 當檔案資料來源為 unshareable 時，該 dsn 檔案只會包含 **dsn** 關鍵字。 當驅動程式管理員將資訊傳送至 unshareable 檔案資料來源時，它會視需要連接到 **DSN** 關鍵字所指示的資料來源。 Unshareable 的 dsn 檔會包含下列關鍵字：  
  
```  
DSN = MyDataSource  
```  
  
 用於檔案資料來源的連接字串是在 dsn 檔案中指定之關鍵字的聯集，以及在呼叫 **SQLDriverConnect**的連接字串中指定的關鍵字。 如果 .dsn 檔中的任何關鍵字與連接字串中的關鍵字發生衝突，驅動程式管理員會決定應該使用哪一個關鍵字值。 如需詳細資訊，請參閱 [SQLDriverConnect](../../../odbc/reference/syntax/sqldriverconnect-function.md)。  
  
## <a name="see-also"></a>另請參閱  
 [https://support.microsoft.com/kb/165866](https://support.microsoft.com/kb/165866)
