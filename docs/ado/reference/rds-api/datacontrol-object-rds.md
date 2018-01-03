---
title: "DataControl 物件 (RDS) |Microsoft 文件"
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: ado
ms.technology: drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
apitype: COM
f1_keywords:
- DataControl
- RDS.DataControl
helpviewer_keywords: DataControl object [ADO]
ms.assetid: d85ea4fc-451c-436e-97b8-58f92b149dd0
caps.latest.revision: "15"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 4921e2895aeeede12f161b31a5dac83e0276822a
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/21/2017
---
# <a name="datacontrol-object-rds"></a>DataControl 物件 (RDS)
將繫結的資料查詢[資料錄集](../../../ado/reference/ado-api/recordset-object-ado.md)至一或多個控制項 （例如，文字方塊中，方格控制項或下拉式方塊） 顯示**資料錄集**網頁上的資料。  
  
> [!IMPORTANT]
>  從 Windows 8 和 Windows Server 2012 開始，RDS 伺服器元件已不再包含在 Windows 作業系統中 (請參閱 < Windows 8 和[Windows Server 2012 相容性手冊](https://www.microsoft.com/en-us/download/details.aspx?id=27416)如需詳細資訊)。 Windows 的未來版本將移除 RDS 用戶端元件。 請避免在新的開發工作中使用這項功能，並規劃修改目前使用這項功能的應用程式。 使用 RDS 的應用程式應該移轉到[WCF 資料服務](http://go.microsoft.com/fwlink/?LinkId=199565)。  
  
## <a name="syntax"></a>語法  
  
```  
  
<OBJECT CLASSID="clsid:BD96C556-65A3-11D0-983A-00C04FC29E33" ID="DataControl"  
   <PARAM NAME="Connect" VALUE="DSN=DSNName;UID=MyUserID;PWD=MyPassword;">  
   <PARAM NAME="Server" VALUE="http://awebsrvr">  
   <PARAM NAME="SQL" VALUE="QueryText">  
</OBJECT>  
```  
  
## <a name="remarks"></a>備註  
 類別識別碼**.RDSDataControl**物件是 BD96C556-65A3-11 D 0 983A 00C04FC29E33。  
  
> [!NOTE]
>  如果您收到錯誤， [.RDSDataSpace](../../../ado/reference/rds-api/dataspace-object-rds.md)或**.RDSDataControl**物件不會載入，請確定您使用正確的類別識別碼。 類別這些物件的識別碼已從版本 1.0 和 1.1 版。 此外，請注意當您使用時，必須將甚至可為 null 的資料行**RDS DataControl**物件。  
  
 對於基本案例中，您需要只設定**SQL**，**連接**，和**伺服器**屬性**.RDSDataControl**物件，會自動呼叫預設的商務物件， [RDSServer.DataFactory](../../../ado/reference/rds-api/datafactory-object-rdsserver.md)。  
  
 中的所有屬性**.RDSDataControl**是選擇性的因為自訂商務物件可取代的功能。  
  
> [!NOTE]
>  如果您查詢多個結果，只有第一個[資料錄集](../../../ado/reference/ado-api/recordset-object-ado.md)傳回。 如果需要多個結果集，將每個指派到其自有**DataControl**。 針對多個結果查詢的範例可能包括：`"Select * from Authors, Select * from Topics"`  
  
 新增 「 DFMode = 20; 」 到您的連接字串使用時**.RDSDataControl**物件可以改善伺服器效能，當您更新資料。 使用此設定， **RDSServer.DataFactory**伺服器上的物件會使用大量的資源模式。 不過，下列功能不適用於這項設定：  
  
-   使用參數化的查詢。  
  
-   取得參數或資料行的資訊，然後再呼叫**Execute**方法。  
  
-   設定**Transact 更新**至**True**。  
  
-   取得資料列狀態。  
  
-   呼叫[重新同步處理](../../../ado/reference/ado-api/resync-method.md)方法。  
  
-   透過重新整理 （明確或自動）[重新同步處理更新](../../../ado/reference/ado-api/update-resync-property-dynamic-ado.md)屬性。  
  
-   設定**命令**或[資料錄集](../../../ado/reference/rds-api/recordset-sourcerecordset-properties-rds.md)屬性。  
  
-   使用**adCmdTableDirect**。  
  
 **.RDSDataControl**物件依預設以非同步模式執行。 如果您需要同步執行您的應用程式時，設定[ExecuteOptions](../../../ado/reference/rds-api/executeoptions-property-rds.md)參數等於**adcExecSync**和[FetchOptions](../../../ado/reference/rds-api/fetchoptions-property-rds.md)參數等於**adcFetchUpFront**，如下列範例所示。  
  
```  
<OBJECT CLASSID="clsid:BD96C556-65A3-11D0-983A-00C04FC29E33"   
    ID="DataControl"  
   <PARAM NAME="Connect" VALUE="DSN=DSNName;UID=MyUserID;PWD=MyPassword;">  
   <PARAM NAME="Server" VALUE="http://awebsrvr">  
   <PARAM NAME="SQL" VALUE="QueryText">  
   <PARAM NAME="ExecuteOptions" VALUE="1">   <PARAM NAME="FetchOptions" VALUE="1">  
</OBJECT>  
```  
  
 使用其中一個**.RDSDataControl**物件，以連結至一個或多個視覺控制項的單一查詢的結果。 例如，假設您的程式碼查詢要求客戶資料，例如名稱、 居住地、 位置的生日、 年齡和優先順序客戶狀態。 您可以使用單一**.RDSDataControl**物件，以顯示客戶的名稱、 年齡和區域中的三個個別文字。優先權客戶狀態核取方塊。和方格控制項中的所有資料。  
  
 使用不同**.RDSDataControl**連結多個查詢的結果不同的視覺控制項的物件。 例如，假設您使用一個查詢來取得有關客戶和第二個查詢，以便取得客戶已購買的商品的相關資訊。 您想要顯示三個文字方塊和一個核取方塊，以及方格控制項中的第二個查詢的結果中的第一個查詢的結果。 如果您使用預設的商務物件 (**RDSServer.DataFactory**)，您必須執行下列動作：  
  
-   加入兩個**.RDSDataControl**網頁的物件。  
  
-   寫入兩個查詢時，每一個**SQL**兩個屬性**.RDSDataControl**物件。 一個**.RDSDataControl**物件將包含要求客戶資訊的 SQL 查詢，則為第二個會包含查詢要求一份客戶已購買的商品。  
  
-   在每個繫結的控制項物件標籤中，指定 DATAFLD 值來設定您想要顯示每個視覺控制項中的資料值。  
  
 沒有任何數目的計數限制**.RDSDataControl**物件，您可以內嵌在單一網頁上使用物件標記。  
  
 當您定義**.RDSDataControl**物件在網頁上，請使用非零**高度**和**寬度**例如 1 （以避免包含額外的空間） 的值。  
  
 遠端資料服務用戶端元件已包含在 Internet Explorer 4.0;因此，您不需要包含中的程式碼基底參數您**.RDSDataControl**標記的物件。  
  
 Internet Explorer 4.0 或更新版本，您可以使用繫結至資料 HTML 控制項和 ActiveX® 控制項才被標示為 apartment 模型的控制項。  
  
> [!NOTE]
>  **Microsoft Visual Basic 使用者** **.RDSDataControl**會安全地以編寫指令碼，而且只適用於 Web 應用程式。 Visual Basic 的用戶端應用程式已不需要。  
  
 本章節包含下列主題。  
  
-   [DataControl 物件 (RDS) 屬性、方法和事件](../../../ado/reference/rds-api/datacontrol-object-rds-properties-methods-and-events.md)  
  
## <a name="see-also"></a>請參閱  
 [DataControl 物件範例 (VBScript)](../../../ado/reference/rds-api/datacontrol-object-example-vbscript.md)






















