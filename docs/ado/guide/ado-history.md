---
title: "ADO 記錄 |Microsoft 文件"
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: guide
ms.technology: "“drivers”"
ms.topic: article
helpviewer_keywords:
- ADO, what's new
ms.assetid: 667673f2-3151-432b-894a-3fc60b704ea4
caps.latest.revision: 13
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 1ace4237c41b4a92b62e958970ebb49dcf2156d0
ms.contentlocale: zh-tw
ms.lasthandoff: 09/09/2017

---
# <a name="ado-features-for-each-release"></a>每個版本的 ADO 功能
本主題列出每個版本的 ADO、 ADO MD 和 ADOX 所引進的新功能。

## <a name="ado-60"></a>ADO 6.0
 ADO 6.0 隨附於 Windows Vista、 Windows Data Access Components (Windows DAC) 6.0 的一部分。 ADO 6.0 在功能上等於 ADO 2.8。

## <a name="ado-28"></a>ADO 2.8
 ADO 2.8 隨附在 Windows XP 和 Windows Server 2003 的 Microsoft Data Access Components (MDAC) 2.8 一部分。 MDAC 2.8 的可轉散發套件版本也會提供。請注意，應該只在 Windows 2000 上安裝這個可轉散發套件的版本。 ADO 2.8 解決幾種安全性相關考量：

 *硬碟機存取不允許外部受信任的區域。*
在跨網域指令碼包含信任的網站，會停用下列作業： **Stream.SaveToFile**， **Stream.LoadFromFile**， **Recordset.Save**，和**Recordset.Open**，用來搭配**adCmdFile**旗標或與 Microsoft OLE DB 持續性提供者 (MSPersist)。

 **Recordset.Open** *，***Recordset.Save** *，***Stream.SaveToFile** *，和* **Stream.LoadFromFile***在僅限實體檔案上作業。* 
這些方法現在會確認檔案控制代碼指向實際的檔案。

 **Recordset.ActiveCommand***會傳回錯誤時叫用從 HTML/ASP 網頁。* 
這可防止**命令**誤用物件。

 *數目***資料錄集***傳回巢狀***圖形***命令有上限。* 
巢狀的 shape 命令現在會傳回最多 512 個**資料錄集**。 這表示**圖形**命令不再任意深度巢狀。 相反地，層級的深度上限為 512，每個命令會產生單一 （子系） 如果**資料錄集**。 如果在任何層級，**圖形**命令會傳回多個**資料錄集**，最大的層級的深度會小於 512。

## <a name="ado-27"></a>ADO 2.7
 *64 位元平台支援*ADO 2.7 引進了適用於 64 位元處理器的支援。

## <a name="ado-26"></a>ADO 2.6
 **CubDef.GetSchemaObject***方法*從 ADO 2.6 開始，ADO MD 物件可以擷取使用所指定唯一的名稱， [UniqueName 屬性 (ADO MD)](../../ado/reference/ado-md-api/uniquename-property-ado-md.md)。   父物件的名稱不需要為已知，而且不需要父集合擷取結構描述物件填入。 請參閱[GetSchemaObject 方法 (ADO MD)](../../ado/reference/ado-md-api/getschemaobject-method-ado-md.md)。

 *命令資料流***命令**物件做為使用替代資料流格式支援命令**CommandText**屬性。 [CommandStream 屬性 (ADO)](../../ado/reference/ado-api/commandstream-property-ado.md)可用來指定 XML 範本或 updategram 為**命令**輸入搭配 Microsoft OLE DB Provider for SQL Server。

 **方言***屬性*[方言](../../ado/reference/ado-api/dialect-property.md)是新的屬性，定義的語法和一般規則提供者會使用來剖析字串或資料流。  

 **Command.Execute***方法* [Execute 方法](../../ado/reference/ado-api/execute-method-ado-command.md)的 ADO**命令**物件具有已增強為可使用的輸入和輸出資料流。  

 *欄位 statusvalues*如果修改時，使用者發生 DB_E_ERRORSOCCURRED 錯誤**欄位**的**資料錄集**，現在將會填滿 ADO **Field.Status**適當的狀態資訊的屬性，讓使用者將有何者發生錯誤的詳細資訊。 請參閱[Status 屬性 （ADO 欄位）](../../ado/reference/ado-api/status-property-ado-field.md)。

 **NamedParameters***屬性* [NamedParameters](../../ado/reference/ado-api/namedparameters-property-ado.md)是新的屬性**命令**物件，表示提供者應該使用名為參數。  

 *資料流中的結果集*ADO 可以從資料來源中傳回結果集**資料流**，而非**資料錄集**物件。 使用最新版的 Microsoft OLE DB Provider for SQL Server，您可以取得 XML 結果的提供者執行的"XML"查詢。 A**資料流**接收結果集可以使用做為來源的"XML"命令來開啟。 請參閱[擷取結果集資料流](../../ado/guide/data/retrieving-resultsets-into-streams.md)。

 *單一資料列結果集*ADO**記錄**物件現在可以開啟命令字串或**命令**從提供者會傳回一個資料列的物件。 這會導致與 MDAC 2.6 提供者的改善效能。 請參閱[Open 方法 （ADO 資料錄）](../../ado/reference/ado-api/open-method-ado-record.md)。

## <a name="ado-25"></a>ADO 2.5
 **記錄***物件*ADO 2.5 導入了**記錄**物件來代表，並管理從一個資料列**資料錄集**或資料提供者或物件將半結構化的資料，例如檔案或目錄的封裝。

 **資料流***物件*ADO 2.5 也導入了**資料流**物件以代表二進位或文字資料的資料流。

 *URL 繫結*ADO 2.5 導入了 URL，做為連接字串和命令文字，來命名資料存放區物件的替代方案。 URL 可以使用與現有**連接**和**資料錄集**物件也與新**記錄**和**資料流**物件。

 *支援 URL 繫結的資料提供者*ADO 2.5 支援 OLE DB 提供者所辨識的 URL 配置。 這包括 OLE DB Provider for Internet Publishing，存取 Windows 2000 檔案系統，且可辨識的現有 HTTP 配置。

