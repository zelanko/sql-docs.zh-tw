---
description: 絕對和相對 URL
title: 絕對和相對 Url |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- relative URLs [ADO]
- absolute URLs [ADO]
- URLs [ADO]
ms.assetid: 6a34a7ef-50cc-4c3d-82f7-106b9a8f3caf
author: rothja
ms.author: jroth
ms.openlocfilehash: 19ade6a2c9501523e97d30f496249a423445d3c0
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/27/2020
ms.locfileid: "88991789"
---
# <a name="absolute-and-relative-urls"></a>絕對和相對 URL
URL 會指定儲存在本機電腦或網路電腦上的目標位置。 目標可以是檔案、目錄、HTML 網頁、影像、程式等等。  
  
 *絕對 URL*包含找出資源所需的所有資訊。  
  
 *相對 url*會使用絕對 url 做為起點，來尋找資源。 實際上，會串連絕對和相對 Url 來指定目標的「完整 URL」。  
  
 *絕對 URL*會使用下列格式： *scheme://server/path/resource*  
  
 相對 URL 通常只會包含 *路徑*（以及（選擇性） *資源*，但不包含 *配置* 或 *伺服器*。 下表定義完整 URL 格式的個別部分。  
  
 *方案*  
 指定 *資源* 的存取方式。  
  
 *伺服器*  
 指定 *資源* 所在的電腦名稱稱。  
  
 *path*  
 指定導向目標的目錄順序。 如果省略 *資源* ，目標就是 *路徑*中的最後一個目錄。  
  
 *資源*  
 如果包含，則 *資源* 為目標，而且通常是檔案的名稱。 它可能是簡單的檔案 *，* 其中包含單一二進位位元組資料流程或 *結構化檔，* 其中包含一或多個儲存體和二進位資料流程位元組資料流程。  
  
## <a name="url-scheme-registration"></a>URL 配置註冊  
 如果提供者支援 Url，則提供者會註冊一或多個 URL 配置。 註冊表示任何使用配置的 Url 都會自動叫用已註冊的提供者。 例如， *HTTP* 配置會註冊到 [Microsoft OLE DB 提供者進行網際網路發佈](../appendixes/microsoft-ole-db-provider-for-internet-publishing.md)。 ADO 假設所有前面加上 "HTTP" 的 Url 都代表要與網際網路發佈提供者一起使用的 Web 資料夾或檔案。 如需提供者所註冊配置的詳細資訊，請參閱您的提供者檔。  
  
## <a name="defining-context-with-a-url"></a>使用 URL 定義內容  
 以 [連接](../../reference/ado-api/connection-object-ado.md) 物件表示的開啟連接的一個函式，是將後續作業限制為該連接所代表的資料來源。 也就是說，連接會定義後續作業的內容。  
  
 使用 ADO 2.7 或更新版本時，絕對 URL 也可以定義內容。 例如，以絕對 URL 開啟 [記錄](../../reference/ado-api/record-object-ado.md) 物件時，會以隱含方式建立 **連接** 物件來代表 URL 所指定的資源。  
  
 定義內容的絕對 URL 可以在**Record** object [Open](../../reference/ado-api/open-method-ado-record.md)方法的*ActiveConnection*參數中指定。 絕對 URL 也可以指定為 **Connection** 物件 [open](../../reference/ado-api/open-method-ado-connection.md) 方法 *ConnectionString* 參數中 "URL =" 關鍵字的值，以及 [記錄集](../../reference/ado-api/recordset-object-ado.md) 物件 [open](../../reference/ado-api/open-method-ado-recordset.md) method *ActiveConnection* 參數。  
  
 您也可以藉由開啟代表目錄的 **記錄** 或 **記錄集** 物件來定義內容，因為這些物件已經有指定內容的隱含或明確宣告的 **連接** 物件。  
  
## <a name="scoped-operations"></a>範圍作業  
 內容也會定義範圍，也就是可參與後續作業的目錄及其子目錄。 **記錄**物件有數個範圍的方法，可在目錄及其所有子目錄上運作。 這些方法包括 [CopyRecord](../../reference/ado-api/copyrecord-method-ado.md)、 [MoveRecord](../../reference/ado-api/moverecord-method-ado.md)和 [DeleteRecord](../../reference/ado-api/deleterecord-method-ado.md)。  
  
## <a name="relative-urls-as-command-text"></a>相對 Url 作為命令文字  
 您可以指定要在資料來源上執行的命令，方法是在**連接**物件的[Execute](../../reference/ado-api/execute-method-ado-connection.md)方法的*CommandText*參數中輸入字串，然後在**記錄集**物件的[Open](../../reference/ado-api/open-method-ado-recordset.md)方法的*source*參數中輸入字串。  
  
 您可以在 *CommandText* 或 *Source* 參數中指定相對 URL。 相對 URL 實際上不代表命令，例如 SQL 命令;它只會指定參數。 使用中連接的內容必須是絕對 URL，而且 *Option* 參數必須設為 **adCmdTableDirect**。  
  
 例如，下列程式碼範例顯示如何在 Winnt/system32 目錄的 Readme25.txt 檔案上開啟 **記錄集** ：  
  
```  
recordset.Open "system32/Readme25.txt", "URL=https://YourServer/Winnt/",,,adCmdTableDirect  
```  
  
 連接字串中的絕對 URL 會指定伺服器 (`YourServer`) 和路徑 (`Winnt`) 。 此 URL 也會定義內容。  
  
 命令文字中的相對 URL 會使用絕對 URL 做為起點，並指定路徑的其餘部分 (`system32`) ，以及要開啟的檔案 (`Readme25.txt`) 。  
  
 [選項] 欄位 (`adCmdTableDirect`) 表示命令類型是相對 URL。  
  
 另舉一個範例，下列程式碼會在目錄的內容上開啟 **記錄集** `Winnt` ：  
  
```  
recordset.Open "", "URL=https://YourServer/Winnt/",,,adCmdTableDirect  
```  
  
## <a name="ole-db-provider-supplied-url-schemes"></a>OLE DB 提供者提供的 URL 配置  
 完整 URL 的前置部分是用來存取由 URL 其餘部分所識別之資源的 *配置* 。 例如，HTTP (超文字傳輸通訊協定) 和 FTP (檔案傳輸通訊協定) 。  
  
 ADO 支援可辨識自己的 URL 配置的 OLE DB 提供者。 例如， [Microsoft OLE DB Provider for Internet 發佈](../appendixes/microsoft-ole-db-provider-for-internet-publishing.md)*可存取* 「已發佈」的 Windows 2000 檔案，可辨識現有的 HTTP 配置。  
  
## <a name="see-also"></a>另請參閱  
 [ (ADO) 的 Connection 物件 ](../../reference/ado-api/connection-object-ado.md)   
 [ (ADO) 的記錄物件 ](../../reference/ado-api/record-object-ado.md)   
 [Recordset 物件 (ADO)](../../reference/ado-api/recordset-object-ado.md)