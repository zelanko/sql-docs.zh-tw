---
title: ADO 歷程記錄 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- ADO, what's new
ms.assetid: 667673f2-3151-432b-894a-3fc60b704ea4
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: e00a1ff652e3f1463d37e2cd5457965968b4ba4c
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47709556"
---
# <a name="ado-features-for-each-release"></a>針對每個發行項 ADO 功能
本主題列出每個 ADO、 ADO MD 和 ADOX 版本所引進的新功能。

## <a name="ado-60"></a>ADO 6.0
 ADO 6.0 會包含在 Windows Vista、 Windows Data Access Components (Windows DAC) 6.0 的一部分。 ADO 6.0 是功能上相當於 ADO 2.8。

## <a name="ado-28"></a>ADO 2.8
 ADO 2.8 已包含在 Windows XP 和 Windows Server 2003，做為一部分的 Microsoft Data Access Components (MDAC) 2.8。 MDAC 2.8 轉散發版本也會提供;請注意，應該只在 Windows 2000 上安裝這個可轉散發套件的版本。 ADO 2.8 解決數個安全性相關考量：

 *硬碟機的存取不允許外部受信任的區域。*
在跨網域指令碼包含不受信任的網站，會停用下列作業： **Stream.SaveToFile**， **Stream.LoadFromFile**， **Recordset.Save**，及**Recordset.Open**搭配使用， **adCmdFile**旗標或使用 Microsoft OLE DB 持續性提供者 (MSPersist)。

 **Recordset.Open** *，***Recordset.Save** *，***Stream.SaveToFile** *，以及***Stream.LoadFromFile***作用於實體的檔案。* 
這些方法現在會驗證檔案控制代碼會指向實體的檔案。

 **Recordset.ActiveCommand***會傳回錯誤時叫用從 HTML/ASP 網頁。* 
這可防止**命令**誤用物件。

 *數目***資料錄集***傳回巢狀***圖形***命令有上限。* 
巢狀的 shape 命令現在會傳回最多 512**資料錄集**。 這表示**圖形**命令不再任意深度巢狀。 相反地，層級的深度上限為 512，每個命令會產生單一 （子系），如果**資料錄集**。 如果任何層級**圖形**命令會傳回多個**資料錄集**，深度最大程度會小於 512。

## <a name="ado-27"></a>ADO 2.7
 *64 位元平台支援*ADO 2.7 引進了適用於 64 位元處理器的支援。

## <a name="ado-26"></a>ADO 2.6
 **CubDef.GetSchemaObject***方法*從 ADO 2.6 開始，ADO MD 物件可以擷取使用唯一的名稱，必須按照[UniqueName 屬性 (ADO MD)](../../ado/reference/ado-md-api/uniquename-property-ado-md.md)。   不需要知道，父物件的名稱和父集合不需要填入，以擷取結構描述物件。 請參閱[GetSchemaObject 方法 (ADO MD)](../../ado/reference/ado-md-api/getschemaobject-method-ado-md.md)。

 *命令資料流***命令**物件使用的替代方式為資料流格式支援命令**CommandText**屬性。 [CommandStream 屬性 (ADO)](../../ado/reference/ado-api/commandstream-property-ado.md)可用來指定 XML 範本或 updategram 做**命令**輸入 Microsoft OLE DB provider for SQL Server。

 **方言***屬性*[方言](../../ado/reference/ado-api/dialect-property.md)是新的屬性，定義的語法和一般規則提供者會使用來剖析字串或資料流。  

 **Command.Execute***方法* [Execute 方法](../../ado/reference/ado-api/execute-method-ado-command.md)的 ADO**命令**已增強用於輸入和輸出資料流的物件。  

 *欄位 statusvalues*如果使用者修改時，發生 DB_E_ERRORSOCCURRED 錯誤**欄位**的**資料錄集**，現在將會填滿 ADO **Field.Status**適當的狀態資訊的屬性，讓使用者將會有何問題的詳細資訊。 請參閱[Status 屬性 (ADO Field)](../../ado/reference/ado-api/status-property-ado-field.md)。

 **NamedParameters***屬性* [NamedParameters](../../ado/reference/ado-api/namedparameters-property-ado.md)是新的屬性**命令**物件，表示提供者應該使用名為參數。  

 *資料流中的結果集*ADO 可以從資料來源中傳回結果集**Stream**，而非**資料錄集**物件。 您可以使用最新版本的 Microsoft OLE DB provider for SQL Server，您可以取得 XML 結果從提供者所執行的"XML"的查詢。 A **Stream**接收結果集可以使用做為來源的"XML"命令來開啟。 請參閱[將資料流結果集擷取](../../ado/guide/data/retrieving-resultsets-into-streams.md)。

 *單一資料列結果集*ADO**記錄**物件現在已可開啟上一個命令字串或**命令**從提供者會傳回一個資料列的物件。 這會導致使用 MDAC 2.6 提供者的改善效能。 請參閱[Open 方法 (ADO Record)](../../ado/reference/ado-api/open-method-ado-record.md)。

## <a name="ado-25"></a>ADO 2.5
 **資料錄***物件*ADO 2.5 引進了**記錄**物件來表示和管理的資料列**資料錄集**或資料提供者，或物件的封裝半結構化的資料，例如檔案或目錄。

 **Stream** *物件*ADO 2.5 也導入了**Stream**物件來代表二進位或文字資料流。

 *URL 繫結*ADO 2.5 引進了使用的 URL，做為連接字串和命令的文字，來命名的資料存放區物件的替代方案。 URL 可以搭配現有**連接**並**資料錄集**物件，以及使用新**記錄**和**Stream**物件。

 *支援 URL 繫結的資料提供者*ADO 2.5 支援 OLE DB 提供者所辨識的 URL 配置。 這包括 OLE DB Provider for Internet Publishing，存取 Windows 2000 檔案系統，並識別現有的 HTTP 配置時。
