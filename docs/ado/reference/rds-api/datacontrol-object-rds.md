---
title: DataControl 物件 (RDS) |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- DataControl
- RDS.DataControl
helpviewer_keywords:
- DataControl object [ADO]
ms.assetid: d85ea4fc-451c-436e-97b8-58f92b149dd0
author: MightyPen
ms.author: genemi
ms.openlocfilehash: a571e93a070c3ce07fbaf40a86b762c749042ec1
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/15/2019
ms.locfileid: "67964391"
---
# <a name="datacontrol-object-rds"></a>DataControl 物件 (RDS)
繫結資料的查詢[資料錄集](../../../ado/reference/ado-api/recordset-object-ado.md)至一或多個控制項 （例如，文字方塊中，方格控制項或下拉式方塊） 來顯示**資料錄集**網頁上的資料。  
  
> [!IMPORTANT]
>  從 Windows 8 和 Windows Server 2012 開始，RDS 伺服器元件不會再包含在 Windows 作業系統中 (請參閱 Windows 8 和[Windows Server 2012 相容性操作手冊](https://www.microsoft.com/download/details.aspx?id=27416)如需詳細資訊)。 RDS 用戶端元件將會在 Windows 的未來版本中移除。 請避免在新的開發工作中使用這項功能，並規劃修改目前使用這項功能的應用程式。 使用 RDS 的應用程式應該移轉至[WCF 資料服務](https://go.microsoft.com/fwlink/?LinkId=199565)。  
  
## <a name="syntax"></a>語法  
  
```  
  
<OBJECT CLASSID="clsid:BD96C556-65A3-11D0-983A-00C04FC29E33" ID="DataControl"  
   <PARAM NAME="Connect" VALUE="DSN=DSNName;UID=MyUserID;PWD=MyPassword;">  
   <PARAM NAME="Server" VALUE="https://awebsrvr">  
   <PARAM NAME="SQL" VALUE="QueryText">  
</OBJECT>  
```  
  
## <a name="remarks"></a>備註  
 頇蜞頇**rds。DataControl**物件是 BD96C556-65A3-11 D 0 983A 00C04FC29E33。  
  
> [!NOTE]
>  如果您收到錯誤指出[rds。DataSpace](../../../ado/reference/rds-api/dataspace-object-rds.md)或**rds。DataControl**物件不會載入，請確定您使用的正確的類別識別碼。 類別識別碼，這些物件已從版本 1.0 和 1.1 版。 此外，請注意當您使用時，必須設定甚至可為 null 的資料行**RDS DataControl**物件。  
  
 基本的案例中，您需要設定只**SQL**， **Connect**，和**Server**屬性**rds。DataControl**物件，會自動呼叫預設的商務物件，該物件[RDSServer.DataFactory](../../../ado/reference/rds-api/datafactory-object-rdsserver.md)。  
  
 中的所有屬性**rds。DataControl**是選擇性的因為自訂商務物件，可以取代其功能。  
  
> [!NOTE]
>  如果您查詢中的多個結果，只有第一個[資料錄集](../../../ado/reference/ado-api/recordset-object-ado.md)會傳回。 如果需要多個結果集，將每個指派到其自有**DataControl**。 多個結果的查詢的範例可能包括： `"Select * from Authors, Select * from Topics"`  
  
 新增 「 DFMode = 20; 」 在連接字串，當您使用**rds。DataControl**物件可以改善伺服器的效能，當您更新資料。 使用此設定時， **RDSServer.DataFactory**伺服器上的物件會使用大量的資源模式。 不過，下列功能不適用於此組態：  
  
-   使用參數化的查詢。  
  
-   取得參數或資料行的資訊，然後再呼叫**Execute**方法。  
  
-   設定**Transact 更新**要 **，則為 True**。  
  
-   取得資料列狀態。  
  
-   呼叫[Resync](../../../ado/reference/ado-api/resync-method.md)方法。  
  
-   重新整理 （明確或自動），透過[更新重新同步處理](../../../ado/reference/ado-api/update-resync-property-dynamic-ado.md)屬性。  
  
-   設定**命令**或是[資料錄集](../../../ado/reference/rds-api/recordset-sourcerecordset-properties-rds.md)屬性。  
  
-   使用**adCmdTableDirect**。  
  
 **Rds。DataControl**預設物件會在非同步模式中執行。 如果您需要同步執行您的應用程式時，設定[ExecuteOptions](../../../ado/reference/rds-api/executeoptions-property-rds.md)參數等於**adcExecSync**並[FetchOptions](../../../ado/reference/rds-api/fetchoptions-property-rds.md)參數等於**adcFetchUpFront**，如下列範例所示。  
  
```  
<OBJECT CLASSID="clsid:BD96C556-65A3-11D0-983A-00C04FC29E33"   
    ID="DataControl"  
   <PARAM NAME="Connect" VALUE="DSN=DSNName;UID=MyUserID;PWD=MyPassword;">  
   <PARAM NAME="Server" VALUE="https://awebsrvr">  
   <PARAM NAME="SQL" VALUE="QueryText">  
   <PARAM NAME="ExecuteOptions" VALUE="1">   <PARAM NAME="FetchOptions" VALUE="1">  
</OBJECT>  
```  
  
 使用其中一個**rds。DataControl**物件連結至一或多個視覺控制項的單一查詢的結果。 例如，假設您的程式碼查詢要求客戶資料，例如名稱、 居住地、 位置的生日、 年齡和優先順序客戶狀態。 您可以使用單一**rds。DataControl**物件，以顯示客戶的名稱、 年齡和區域，在上一次個別的三個文字方塊;優先順序客戶狀態 核取方塊;和方格控制項中的所有資料。  
  
 使用不同**rds。DataControl**物件連結至不同的視覺控制項的多個查詢的結果。 例如，假設您使用一個查詢來取得一位客戶的相關資訊和第二個查詢，以便取得客戶已購買的商品的相關資訊。 您想要顯示三個文字方塊和一個核取方塊，以及方格控制項中的第二個查詢的結果中的第一個查詢的結果。 如果您使用預設的商務物件 (**RDSServer.DataFactory**)，您必須執行下列動作：  
  
-   新增兩個**rds。DataControl**到網頁上的物件。  
  
-   寫入兩個查詢，其中每個**SQL**兩個屬性**rds。DataControl**物件。 一個**rds。DataControl**物件會包含要求客戶資訊的 SQL 查詢，第二個會包含查詢要求一份客戶已購買的商品。  
  
-   在每個繫結控制項的物件標記，指定 DATAFLD 值來設定您想要在每個視覺控制項中顯示的資料值。  
  
 沒有任何數目的計數限制**rds。DataControl**物件，您可以使用內嵌物件標記單一 Web 網頁上。  
  
 當您定義**rds。DataControl**物件在網頁上，請使用零**高度**並**寬度**例如 1 （以避免包含額外的空間） 的值。  
  
 遠端資料服務用戶端元件都已包含的 Internet Explorer 4.0;因此，您不需要包含中的程式碼基底參數您**rds。DataControl**物件標記。  
  
 Internet Explorer 4.0 或更新版本，您可以使用繫結至資料 HTML 控制項和 ActiveX® 控制項才被標示為 apartment 模型的控制項。  
  
> [!NOTE]
>  **Microsoft Visual Basic 使用者** **rds。DataControl**而言是安全的指令碼，並只適用於 Web 應用程式。 Visual Basic 的用戶端應用程式有不需要。  
  
 本章節包含下列主題。  
  
-   [DataControl 物件 (RDS) 屬性、方法和事件](../../../ado/reference/rds-api/datacontrol-object-rds-properties-methods-and-events.md)  
  
## <a name="see-also"></a>另請參閱  
 [DataControl 物件範例 (VBScript)](../../../ado/reference/rds-api/datacontrol-object-example-vbscript.md)






















