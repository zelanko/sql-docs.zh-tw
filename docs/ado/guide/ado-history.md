---
description: 每個版本的 ADO 功能
title: ADO 歷程記錄 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2019
ms.reviewer: ''
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- ADO, what's new
ms.assetid: 667673f2-3151-432b-894a-3fc60b704ea4
author: rothja
ms.author: jroth
ms.openlocfilehash: 9f76f816f03d1b7ba8e8d186104dc235762739f9
ms.sourcegitcommit: 33e774fbf48a432485c601541840905c21f613a0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/25/2020
ms.locfileid: "88805514"
---
# <a name="ado-features-for-each-release"></a>每個版本的 ADO 功能

本主題列出每個 ADO、ADO MD 和 ADOX 版本所引進的新功能。

## <a name="ado-60"></a>ADO 6。0

ADO 6.0 包含在 windows Vista 中， (Windows DAC) 6.0 中的 Windows 資料存取元件的一部分。 ADO 6.0 的功能相當於 ADO 2.8。

## <a name="ado-28"></a>ADO 2。8

ADO 2.8 隨附于 Windows XP 和 Windows Server 2003，這是 Microsoft Data Access 元件的一部分 (MDAC) 2.8。 您也可以使用 MDAC 2.8 的可轉散發版本;請注意，此可轉散發版本只能安裝在 Windows 2000 上。 ADO 2.8 解決了幾個與安全性相關的考慮：

*受信任的區域外部不允許存取硬碟。*
在牽涉到非信任網站的跨網域腳本中，會停用下列作業： **SaveToFile**、 **LoadFromFile**、 **記錄集儲存**和 **記錄集。開啟**，搭配 **AdCmdFile** 旗標或 Microsoft OLE DB 持續性提供者 (MSPersist) 使用。

**Recordset. Open** _、_  **recordset. Save** _、_  **SaveToFile** _和_  **stream。 LoadFromFile**  _只會在實體檔案上運作。_
這些方法現在會確認檔案控制代碼只指向實體檔案。

**ActiveCommand**  _從 HTML/ASP 頁面叫用時發生錯誤。_
這可防止 **命令** 物件被誤用。

_嵌套_**圖形**命令所傳回的**記錄集**_數目__有上限。_        
嵌套圖形命令現在最多會傳回512個 **記錄集**。 這表示 **Shape** 命令無法再以任何深度進行嵌套。 相反地，如果每個命令都產生單一 (子) **記錄集**，則最大層級深度為512。 如果在任何層級上， **Shape** 命令會傳回多個 **記錄集**，最大深度層級將小於512。

## <a name="ado-27"></a>ADO 2。7

*64 位平臺支援* ADO 2.7 引進64位處理器的支援。

## <a name="ado-26"></a>ADO 2。6

**CubDef. GetSchemaObject**  _方法_ 從 ADO 2.6 開始，可以使用唯一的名稱來抓取 ADO MD 的物件，如 [UniqueName 屬性所指定 (ADO MD) ](../reference/ado-md-api/uniquename-property-ado-md.md)。 父物件的名稱不需要是已知的，且不需要填入父集合來取出架構物件。 請參閱 [GetSchemaObject 方法 (ADO MD) ](../reference/ado-md-api/getschemaobject-method-ado-md.md)。

*命令資料流程***命令**物件以資料流程格式支援命令，做為使用**CommandText**屬性的替代方法。 [ (ADO) 的 CommandStream 屬性](../reference/ado-api/commandstream-property-ado.md)可用來指定 XML 範本或 updategram 做為 SQL Server 的 Microsoft OLE DB 提供者的**命令**輸入。

**方言**_屬性_ 
 [方言](../reference/ado-api/dialect-property.md)是新的屬性，可定義提供者用來剖析字串或資料流程的語法和一般規則。  

**Command.Exe刻意**的_方法_，ADO **Command**物件的[Execute 方法](../reference/ado-api/execute-method-ado-command.md)已經過增強，可使用資料流程進行輸入和輸出。  

*欄位 statusvalues*如果使用者在修改**記錄集**的**欄位**時遇到 DB_E_ERRORSOCCURRED 錯誤，則 ADO 現在會在 [**狀態**] 屬性中填入適當的狀態資訊，讓使用者能夠取得錯誤的詳細資訊。 請參閱 [狀態屬性 (ADO 欄位) ](../reference/ado-api/status-property-ado-field.md)。

**NamedParameters**_屬性_ 
 [NamedParameters](../reference/ado-api/namedparameters-property-ado.md)是**命令**物件的新屬性，指出提供者應該使用具名引數。  

*資料流程中的結果* 集ADO 可以從 **資料流程**中的資料來源傳回結果集，而不是從 **記錄集** 物件傳回。 使用最新版本的 Microsoft OLE DB Provider for SQL Server，您可以藉由執行 "For XML" 查詢，從提供者取得 XML 結果。 接收結果集的 **資料流程** 可以用 "For XML" 命令作為來源來開啟。 請參閱 [將結果集取出至資料流程](./data/retrieving-resultsets-into-streams.md)。

*單一資料列結果集*您現在可以在命令字串或**命令**物件上開啟 ADO**記錄**物件，該物件會從提供者傳回一列資料。 這會導致 MDAC 2.6 提供者的效能提升。 請參閱 [Open Method (ADO 記錄) ](../reference/ado-api/open-method-ado-record.md)。

## <a name="ado-25"></a>ADO 2。5

**記錄**_物件_ADO 2.5 引進了**記錄**物件來代表和管理**記錄集**或資料提供者的資料列，或是封裝半結構化資料的物件，例如檔案或目錄。

**Stream** _物件_ ADO 2.5 也引進了 *和*stream * * 物件來代表二進位或文字資料的資料流程。

*URL* 系結ADO 2.5 引進了使用 URL 做為連接字串和命令文字的替代方式，以命名資料存放區物件。 URL 可用於現有的 **連接** 和 **記錄集** 物件，以及新的 **記錄** 和 **資料流程** 物件。

*支援 URL 系結的資料提供者* ADO 2.5 支援可辨識 URL 配置的 OLE DB 提供者。 這包括網際網路發佈的 OLE DB 提供者，它會存取 Windows 2000 檔案系統並辨識現有的 HTTP 配置。
