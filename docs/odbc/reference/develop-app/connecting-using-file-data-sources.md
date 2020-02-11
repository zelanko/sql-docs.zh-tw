---
title: 使用檔案資料來源進行連接 |Microsoft Docs
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
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "68083110"
---
# <a name="connecting-using-file-data-sources"></a>使用檔案資料來源進行連線
檔案資料來源的連接資訊會儲存在 .dsn 檔案中。 因此，單一使用者可以重複使用連接字串，或在多個使用者之間共用（如果已安裝適當的驅動程式）。 檔案包含驅動程式名稱（如果是 unshareable 檔資料來源，則為其他資料來源名稱），並選擇性地包含可供**SQLDriverConnect**使用的連接字串。 驅動程式管理員會針對從. dsn 檔案中的關鍵字呼叫**SQLDriverConnect** ，建立連接字串。  
  
 檔案資料來源可讓應用程式指定連接選項，而不需要建立連接字串以與**SQLDriverConnect**搭配使用。 檔案資料來源通常是藉由指定**SAVEFILE**關鍵字來建立，這會導致驅動程式管理員將**SQLDriverConnect**呼叫所建立的輸出連接字串儲存至 .dsn 檔案。 藉由呼叫**SQLDriverConnect**與**FILEDSN**關鍵字，可以重複使用該連接字串。 這會簡化連接程式，並提供連接字串的持續性來源。  
  
 您也可以在安裝程式 DLL 中呼叫**SQLCreateDataSource**來建立檔案資料來源。 您可以藉由呼叫**SQLWriteFileDSN**，將資訊寫入至 .dsn 檔案，並藉由呼叫**SQLReadFileDSN**從該 dsn 檔案讀取。這兩個函數也都在安裝程式 DLL 中。 如需安裝程式 DLL 的詳細資訊，請參閱設定[資料來源](../../../odbc/reference/install/configuring-data-sources.md)。  
  
 用於連接資訊的關鍵字位於 .dsn 檔案的 [ODBC] 區段中。 可共用的 .dsn 檔案在 [ODBC] 區段中的最小資訊是 DRIVER 關鍵字：  
  
```  
DRIVER = SQL Server  
```  
  
 可共用的 .dsn 檔案通常包含連接字串，如下所示：  
  
```  
DRIVER = SQL Server  
UID = Larry  
DATABASE = MyDB  
```  
  
 當 unshareable 檔案資料來源時，此 .dsn 檔案只會包含一個**dsn**關鍵字。 當驅動程式管理員傳送 unshareable 檔資料來源中的資訊時，它會視需要連接到**DSN**關鍵字所指示的資料來源。 Unshareable 的 dsn 檔案會包含下列關鍵字：  
  
```  
DSN = MyDataSource  
```  
  
 檔案資料來源所使用的連接字串，是在**SQLDriverConnect**的呼叫中，于 dsn 檔案中指定的關鍵字與連接字串中指定之關鍵字的聯集。 如果您的 dsn 檔案中有任何關鍵字與連接字串中的關鍵字發生衝突，驅動程式管理員會決定應該使用哪個關鍵字值。 如需詳細資訊，請參閱[SQLDriverConnect](../../../odbc/reference/syntax/sqldriverconnect-function.md)。  
  
## <a name="see-also"></a>另請參閱  
 [https://support.microsoft.com/kb/165866](https://support.microsoft.com/kb/165866)
