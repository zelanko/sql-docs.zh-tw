---
title: DataControl 物件（RDS） |Microsoft Docs
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
author: rothja
ms.author: jroth
ms.openlocfilehash: 7bc9482c6626de36d9e45b2a2968b504b0793746
ms.sourcegitcommit: 6037fb1f1a5ddd933017029eda5f5c281939100c
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/04/2020
ms.locfileid: "82746112"
---
# <a name="datacontrol-object-rds"></a>DataControl 物件 (RDS)
將資料查詢[記錄集](../../../ado/reference/ado-api/recordset-object-ado.md)系結至一或多個控制項（例如文字方塊、方格控制項或下拉式方塊），以顯示網頁上的**記錄集**資料。  
  
> [!IMPORTANT]
>  從 Windows 8 和 Windows Server 2012 開始，Windows 作業系統不再包含 RDS 伺服器元件（如需詳細資訊，請參閱 Windows 8 和[Windows Server 2012 相容性操作手冊](https://www.microsoft.com/download/details.aspx?id=27416)）。 RDS 用戶端元件將會在未來的 Windows 版本中移除。 請避免在新的開發工作中使用這項功能，並規劃修改目前使用這項功能的應用程式。 使用 RDS 的應用程式應該遷移至[WCF 資料服務](https://go.microsoft.com/fwlink/?LinkId=199565)。  
  
## <a name="syntax"></a>語法  
  
```  
  
<OBJECT CLASSID="clsid:BD96C556-65A3-11D0-983A-00C04FC29E33" ID="DataControl"  
   <PARAM NAME="Connect" VALUE="DSN=DSNName;UID=MyUserID;PWD=MyPassword;">  
   <PARAM NAME="Server" VALUE="https://awebsrvr">  
   <PARAM NAME="SQL" VALUE="QueryText">  
</OBJECT>  
```  
  
## <a name="remarks"></a>備註  
 RDS 的類別識別碼 **。DataControl**物件是 BD96C556-65A3-11D0-983A-00C04FC29E33。  
  
> [!NOTE]
>  如果您收到 RDS 的錯誤[。[空間](../../../ado/reference/rds-api/dataspace-object-rds.md)] 或 [ **RDS]。DataControl**物件未載入，請確定您使用的是正確的類別識別碼。 這些物件的類別識別碼已從版本1.0 和1.1 變更。 此外，請注意，當您使用**RDS DataControl**物件時，必須設定可為 null 的資料行。  
  
 在基本案例中，您只需要設定 RDS 的**SQL**、 **Connect**和**伺服器**屬性 **。DataControl**物件，它會自動呼叫預設的商務物件[RDSServer. DataFactory](../../../ado/reference/rds-api/datafactory-object-rdsserver.md)。  
  
 RDS 中的所有屬性 **。DataControl**是選擇性的，因為自訂商務物件可以取代其功能。  
  
> [!NOTE]
>  如果您查詢多個結果，則只會傳回第一個[記錄集](../../../ado/reference/ado-api/recordset-object-ado.md)。 如果需要多個結果集，請將每個都指派給它自己的**DataControl**。 下列為多個結果的查詢範例：`"Select * from Authors, Select * from Topics"`  
  
 當您使用 RDS 時，將 "DFMode = 20;" 加入至您的連接字串 **。** 當您更新資料時，DataControl 物件可以提升伺服器的效能。 使用此設定時，伺服器上的**RDSServer. DataFactory**物件會使用較不耗費資源的模式。 不過，此設定無法使用下列功能：  
  
-   使用參數化查詢。  
  
-   呼叫**Execute**方法之前，取得參數或資料行資訊。  
  
-   將**交易更新**設定為**True**。  
  
-   正在取得資料列狀態。  
  
-   呼叫重新[同步](../../../ado/reference/ado-api/resync-method.md)處理方法。  
  
-   透過[更新重新同步](../../../ado/reference/ado-api/update-resync-property-dynamic-ado.md)處理屬性重新整理（明確或自動）。  
  
-   設定**命令**或[記錄集](../../../ado/reference/rds-api/recordset-sourcerecordset-properties-rds.md)屬性。  
  
-   使用**adCmdTableDirect**。  
  
 **RDS。DataControl**物件預設會以非同步模式執行。 如果您的應用程式需要同步執行，請將[ExecuteOptions](../../../ado/reference/rds-api/executeoptions-property-rds.md)參數設為等於**adcExecSync** ，並將[FetchOptions](../../../ado/reference/rds-api/fetchoptions-property-rds.md)參數設定為等於**adcFetchUpFront**，如下列範例所示。  
  
```  
<OBJECT CLASSID="clsid:BD96C556-65A3-11D0-983A-00C04FC29E33"   
    ID="DataControl"  
   <PARAM NAME="Connect" VALUE="DSN=DSNName;UID=MyUserID;PWD=MyPassword;">  
   <PARAM NAME="Server" VALUE="https://awebsrvr">  
   <PARAM NAME="SQL" VALUE="QueryText">  
   <PARAM NAME="ExecuteOptions" VALUE="1">   <PARAM NAME="FetchOptions" VALUE="1">  
</OBJECT>  
```  
  
 使用一個**RDS。DataControl**物件，可將單一查詢的結果連結至一個或多個視覺控制項。 例如，假設您撰寫了要求客戶資料的查詢程式碼，例如姓名、居住、生日、年齡和優先順序客戶狀態。 您可以使用單一**RDS。DataControl**物件，以在三個不同的文字方塊中顯示客戶的名稱、年齡和區域;核取方塊中的客戶狀態優先順序;和方格控制項中的所有資料。  
  
 使用不同**的 RDS。DataControl**物件，以將多個查詢的結果連結至不同的視覺控制項。 例如，假設您使用一個查詢來取得客戶的相關資訊，而第二個查詢則是用來取得客戶已購買商品的相關資訊。 您想要在三個文字方塊和一個核取方塊中顯示第一個查詢的結果，並在方格控制項中顯示第二個查詢的結果。 如果您使用預設的商務物件（**RDSServer. DataFactory**），您必須執行下列動作：  
  
-   加入兩個**RDS。** 將物件 DataControl 至您的網頁。  
  
-   撰寫兩個查詢，分別用於兩個 RDS 的每個**SQL**屬性 **。DataControl**物件。 一個**RDS。DataControl**物件將包含要求客戶資訊的 SQL 查詢;第二個會包含一個查詢，要求客戶已購買的商品清單。  
  
-   在每個繫結控制項的物件標記中，指定 DATAFLD 值，以設定您想要在每個視覺效果控制項中顯示之資料的值。  
  
 RDS 的數目沒有計數限制 **。DataControl**物件，您可以在單一網頁上使用物件標記加以內嵌。  
  
 當您定義**RDS 時。** 網頁上的 DataControl 物件，請使用非零**高度**和**寬度**值（例如1）（以避免包含額外的空間）。  
  
 遠端資料服務用戶端元件已包含在 Internet Explorer 4.0 中;因此，您不需要在 RDS 中包含程式碼基底參數 **。DataControl**物件標記。  
  
 使用 Internet Explorer 4.0 或更新版本時，只有在標記為「單元模型控制項」的情況下，才可以使用 HTML 控制項和 ActiveX®控制項來系結至資料。  
  
> [!NOTE]
>  **Microsoft Visual Basic 使用者****RDS。DataControl**可安全地進行腳本處理，而且只能在 Web 應用程式中使用。 Visual Basic 的用戶端應用程式不需要它。  
  
 本章節包含下列主題。  
  
-   [DataControl 物件 (RDS) 屬性、方法和事件](../../../ado/reference/rds-api/datacontrol-object-rds-properties-methods-and-events.md)  
  
## <a name="see-also"></a>另請參閱  
 [DataControl 物件範例 (VBScript)](../../../ado/reference/rds-api/datacontrol-object-example-vbscript.md)






















