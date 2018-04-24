---
title: 絕對和相對 Url |Microsoft 文件
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: ado
ms.technology:
- drivers
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- relative URLs [ADO]
- absolute URLs [ADO]
- URLs [ADO]
ms.assetid: 6a34a7ef-50cc-4c3d-82f7-106b9a8f3caf
caps.latest.revision: 12
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 2482386f131b7e49134b5fdcbfaae7d0ec339b74
ms.sourcegitcommit: bb044a48a6af9b9d8edb178dc8c8bd5658b9ff68
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/18/2018
---
# <a name="absolute-and-relative-urls"></a>絕對和相對 Url
URL 指定的位置儲存在本機或網路的電腦上的目標。 目標可以是檔案、 目錄、 HTML 網頁、 影像、 程式及等等*。*  
  
 *絕對 URL*包含要尋找的資源所需的所有資訊。  
  
 A*相對 URL*找出使用絕對 URL 做為起點的資源。 作用中，「 完整的 URL 」 的目標是由指定串連絕對和相對 Url。  
  
 *絕對 URL*使用下列格式： *scheme://server/path/resource*  
  
 相對的 URL 通常只包含*路徑*，並選擇性地*資源*，但沒有*配置*或*伺服器*。 下表定義完整的 URL 格式的各個部分。  
  
 *scheme*  
 指定如何*資源*存取。  
  
 *伺服器*  
 指定的電腦名稱其中*資源*所在。  
  
 *path*  
 指定連至目標目錄序列。 如果*資源*已省略，目標是中的最後一個目錄*路徑*。  
  
 *resource*  
 如果包含，*資源*是目標，且通常是檔案的名稱。 它可能是*簡單的檔案，*包含單一的二進位資料流的位元組，或*結構化文件，*包含一或多個儲存體和二進位資料流的位元組。  
  
## <a name="url-scheme-registration"></a>URL 配置註冊  
 如果提供者支援的 Url，提供者將會註冊一個或多個 URL 配置。 註冊表示，任何使用結構描述的 Url 會自動叫用已註冊的提供者。 例如， *http*配置已向[Microsoft OLE DB Provider for Internet Publishing](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-internet-publishing.md)。 ADO 假設所有 Url 中加上 「 http 」 都代表 Web 資料夾或檔案，可與網際網路發行的提供者。 註冊您的提供者結構描述的相關資訊，請參閱您的提供者文件。  
  
## <a name="defining-context-with-a-url"></a>定義內容的 url  
 開啟的連接所代表的函式[連接](../../../ado/reference/ado-api/connection-object-ado.md)物件，來限制資料來源的後續作業由該連接。 也就是說，連線會定義後續作業的內容。  
  
 使用 ADO 2.7 或更新版本時，絕對的 URL 也可以定義內容。 例如，當[記錄](../../../ado/reference/ado-api/record-object-ado.md)絕對 URL，以開啟物件**連接**物件會隱含地建立以代表由 URL 指定的資源。  
  
 中可以指定定義內容的絕對 URL *ActiveConnection*參數**記錄**物件[開啟](../../../ado/reference/ado-api/open-method-ado-record.md)方法。 絕對 URL 也可以指定的值為"URL**=**」 中的關鍵字**連接**物件[開啟](../../../ado/reference/ado-api/open-method-ado-connection.md)方法*ConnectionString*參數，而[資料錄集](../../../ado/reference/ado-api/recordset-object-ado.md)物件[開啟](../../../ado/reference/ado-api/open-method-ado-recordset.md)方法*ActiveConnection*參數。  
  
 內容也可以定義開啟**記錄**或**資料錄集**物件，代表目錄，因為這些物件已經有隱含或明確宣告**連線**物件，指定內容。  
  
## <a name="scoped-operations"></a>已設定領域的作業  
 內容也會定義範圍 — 也就是目錄和後續作業可以參與及其子目錄。 **記錄**物件擁有的目錄運作的數個已設定領域的方法和其所有子目錄。 這些方法包括[CopyRecord](../../../ado/reference/ado-api/copyrecord-method-ado.md)， [MoveRecord](../../../ado/reference/ado-api/moverecord-method-ado.md)，和[DeleteRecord](../../../ado/reference/ado-api/deleterecord-method-ado.md)。  
  
## <a name="relative-urls-as-command-text"></a>為命令文字的相對 Url  
 您可以指定要透過輸入字串中的，資料來源上執行的命令*CommandText*參數**連接**物件的[Execute](../../../ado/reference/ado-api/execute-method-ado-connection.md)方法，並在*來源*參數**資料錄集**物件的[開啟](../../../ado/reference/ado-api/open-method-ado-recordset.md)方法。  
  
 中可以指定相對的 URL *CommandText*或*來源*參數。 相對 URL 未實際代表命令，例如 SQL 命令。它只是指定的參數。 使用中連接的內容必須是絕對 URL，而*選項*參數必須設定為**adCmdTableDirect**。  
  
 例如，下列程式碼範例示範如何開啟**資料錄集**Readme25.txt 檔案的 Winnt/system32 目錄：  
  
```  
recordset.Open "system32/Readme25.txt", "URL=http://YourServer/Winnt/",,,adCmdTableDirect  
```  
  
 連接字串中的絕對 URL 指定的伺服器 (`YourServer`) 和路徑 (`Winnt`)。 此 URL 也可定義的內容。  
  
 命令文字中的相對 URL 做為起點使用的絕對 URL，且會指定路徑的其餘部分 (`system32`) 和開啟檔案 (`Readme25.txt`)。  
  
 [選項] 欄位 (`adCmdTableDirect`) 表示的命令類型為相對 URL。  
  
 下列程式碼將會開啟另一個例子，**資料錄集**的內容`Winnt`目錄：  
  
```  
recordset.Open "", "URL=http://YourServer/Winnt/",,,adCmdTableDirect  
```  
  
## <a name="ole-db-provider-supplied-url-schemes"></a>OLE DB 提供者提供的 URL 結構描述  
 完整的 URL 的前置部分是*配置*用來存取 URL 的其餘部分所識別的資源。 範例包括 HTTP （超文字傳輸通訊協定） 和 FTP （檔案傳輸通訊協定）。  
  
 ADO 支援辨識其本身的 URL 結構描述的 OLE DB 提供者。 例如， [Microsoft OLE DB Provider for Internet Publishing](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-internet-publishing.md)*，*存取 「 發行 」 的 Windows 2000 檔案會辨識現有 HTTP 配置。  
  
## <a name="see-also"></a>另請參閱  
 [連接物件 (ADO)](../../../ado/reference/ado-api/connection-object-ado.md)   
 [記錄物件 (ADO)](../../../ado/reference/ado-api/record-object-ado.md)   
 [Recordset 物件 (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)
