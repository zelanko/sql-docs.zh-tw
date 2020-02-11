---
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: a84ccbb97c26ea92f31212933aac79bde2784b72
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "67927162"
---
# <a name="ado-features-for-each-release"></a>每個版本的 ADO 功能

本主題列出每個 ADO、ADO MD 和 ADOX 版本所引進的新功能。

## <a name="ado-60"></a>ADO 6。0

 ADO 6.0 隨附于 Windows Vista，屬於 Windows Data Access Components （Windows DAC）6.0。 ADO 6.0 在功能上相當於 ADO 2.8。

## <a name="ado-28"></a>ADO 2。8

 ADO 2.8 隨附于 Windows XP 和 Windows Server 2003，做為 Microsoft Data Access Components （MDAC）2.8 的一部分。 也提供可轉散發版本的 MDAC 2.8;請注意，此可轉散發版本應僅安裝在 Windows 2000 上。 ADO 2.8 解決幾個與安全性相關的考慮：

 *不允許在受信任區域外存取硬碟。*
在涉及非信任網站的跨網域腳本中，下列作業已停用： **SaveToFile**、 **LoadFromFile**、**記錄集、儲存**和**記錄集。開啟**時，與**AdCmdFile**旗標或 Microsoft OLE DB 持續性提供者（MSPersist）搭配使用。

 **記錄集。開啟** _、_  **記錄集** _、儲存、_  **SaveToFile** _和_  **資料流程。 LoadFromFile**  _只會在實體檔案上操作。_
這些方法現在會驗證檔案控制代碼僅指向實體檔案。

 **ActiveCommand**會_在從 HTML/ASP 頁面叫用時傳回錯誤。_  
這可防止**命令**物件被誤用。

 「_嵌套_**圖形**」命令所傳回的**記錄集**_數目__具有上限。_        
「嵌套圖形」命令現在會傳回最多512個**記錄集**。 這表示**圖形**命令無法再以任何深度加以嵌套。 相反地，如果每個命令都會產生單一（子）**記錄集**，則最大層級深度為512。 如果任何層級的**Shape**命令傳回多個**記錄集**，則深度的最大層級將會小於512。

## <a name="ado-27"></a>ADO 2。7

 *64 位平臺支援*ADO 2.7 引進64位處理器的支援。

## <a name="ado-26"></a>ADO 2。6

 從 ADO 2.6 開始的**CubDef**_方法_，可以使用唯一的名稱來抓取 ADO MD 物件，如[UniqueName 屬性（ADO MD）](../../ado/reference/ado-md-api/uniquename-property-ado-md.md)所指定。   父物件的名稱不需要是已知的，而且不需要填入父集合來抓取架構物件。 請參閱[GetSchemaObject 方法（ADO MD）](../../ado/reference/ado-md-api/getschemaobject-method-ado-md.md)。

 *命令資料流程***命令**物件支援以資料流程格式表示的命令，做為使用**CommandText**屬性的替代方式。 [CommandStream 屬性（ADO）](../../ado/reference/ado-api/commandstream-property-ado.md)可以用來指定 XML 範本或 updategram 做為適用于 SQL Server 的 Microsoft OLE DB 提供者的**命令**輸入。

 **方言**_屬性_[方言](../../ado/reference/ado-api/dialect-property.md)是新的屬性，可定義提供者用來剖析字串或資料流程的語法和一般規則。  

 **命令。 execute**_方法_已增強 ADO **Command**物件的[Execute 方法](../../ado/reference/ado-api/execute-method-ado-command.md)，以使用資料流程進行輸入和輸出。  

 *欄位 statusvalues*如果使用者在修改**記錄集**的**欄位**時發生 DB_E_ERRORSOCCURRED 錯誤，ADO 現在會將**欄位. status**屬性填入適當的狀態資訊，讓使用者能夠取得錯誤的詳細資訊。 請參閱[Status 屬性（ADO Field）](../../ado/reference/ado-api/status-property-ado-field.md)。

 **NamedParameters**  _屬性_ [NamedParameters](../../ado/reference/ado-api/namedparameters-property-ado.md)是**命令**物件的新屬性，它會指出提供者應該使用具名引數。

 *資料流程中的結果*集ADO 可以從**資料流程**中的資料來源傳回結果集，而不是從**Recordset**物件傳回。 使用適用于 SQL Server 的 Microsoft OLE DB 提供者的最新版本，您可以藉由執行「For XML」查詢，從提供者取得 XML 結果。 接收結果集的**資料流程**可以使用 "For XML" 命令當做來源來開啟。 請參閱將結果集抓取[到資料流程中](../../ado/guide/data/retrieving-resultsets-into-streams.md)。

 *單一資料列結果集*您現在可以在命令字串或**命令**物件上開啟 ADO**記錄**物件，該物件會從提供者傳回一個資料列。 這會導致 MDAC 2.6 提供者的效能提升。 請參閱[Open 方法（ADO Record）](../../ado/reference/ado-api/open-method-ado-record.md)。

## <a name="ado-25"></a>ADO 2。5

 **Record** _物件_ADO 2.5 引進**記錄**物件，以表示和管理**記錄集**或資料提供者中的資料列，或是封裝半結構化資料（例如檔案或目錄）的物件。

 **Stream** _物件_ADO 2.5 也引進**資料流程**物件，以代表二進位或文字資料的資料流程。

 *URL*系結ADO 2.5 引進了 URL 的使用，做為連接字串和命令文字的替代方式，以命名資料存放區物件。 URL 可以與現有的**連接**和**記錄集**物件搭配使用，以及使用新的**記錄**和**資料流程**物件。

 *支援 URL 系結的資料提供者*ADO 2.5 支援可辨識 URL 配置的 OLE DB 提供者。 這包括網際網路發佈的 OLE DB 提供者，它會存取 Windows 2000 檔案系統並辨識現有的 HTTP 配置。
