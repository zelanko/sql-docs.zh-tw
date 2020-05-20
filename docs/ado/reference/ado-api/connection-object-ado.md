---
title: Connection 物件（ADO） |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Connection
helpviewer_keywords:
- Connection object [ADO]
ms.assetid: ef6b1824-5b12-43db-89d7-8f3d13896d4d
author: rothja
ms.author: jroth
ms.openlocfilehash: 49a270f143e57c1e093ac94732b67b6424c88607
ms.sourcegitcommit: 6037fb1f1a5ddd933017029eda5f5c281939100c
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/04/2020
ms.locfileid: "82760294"
---
# <a name="connection-object-ado"></a>Connection 物件 (ADO)
表示資料來源的開啟連接。  
  
## <a name="remarks"></a>備註  
 **Connection**物件代表具有資料來源的唯一會話。 在用戶端/伺服器資料庫系統中，它可能相當於與伺服器的實際網路連接。 視提供者支援的功能而定，可能無法使用**連接**物件的某些集合、方法或屬性。  
  
 使用**連接**物件的集合、方法和屬性，您可以執行下列動作：  
  
-   在使用[ConnectionString](../../../ado/reference/ado-api/connectionstring-property-ado.md)、 [ConnectionTimeout](../../../ado/reference/ado-api/connectiontimeout-property-ado.md)和[Mode](../../../ado/reference/ado-api/mode-property-ado.md)屬性開啟連接之前，請先進行設定。 **ConnectionString**是**Connection**物件的預設屬性。  
  
-   將 [ [CursorLocation](../../../ado/reference/ado-api/cursorlocation-property-ado.md) ] 屬性設定為 [用戶端]，以叫用支援批次更新之[OLE DB 的 Microsoft 資料指標服務](../../../ado/guide/appendixes/microsoft-cursor-service-for-ole-db-ado-service-component.md)。  
  
-   使用[DefaultDatabase](../../../ado/reference/ado-api/defaultdatabase-property.md)屬性來設定連接的預設資料庫。  
  
-   使用[IsolationLevel](../../../ado/reference/ado-api/isolationlevel-property.md)屬性，設定在連接上開啟之交易的隔離層級。  
  
-   使用[provider](../../../ado/reference/ado-api/provider-property-ado.md)屬性指定 OLE DB 提供者。  
  
-   使用[Open](../../../ado/reference/ado-api/open-method-ado-connection.md)和[Close](../../../ado/reference/ado-api/close-method-ado.md)方法建立資料來源的實體連接，並于稍後中斷。  
  
-   使用[execute](../../../ado/reference/ado-api/execute-method-ado-connection.md)方法在連接上執行命令，並使用[CommandTimeout](../../../ado/reference/ado-api/commandtimeout-property-ado.md)屬性設定執行。  
  
    > [!NOTE]
    >  若要在不使用 Command 物件的情況下執行查詢，請將查詢字串傳遞至**連接**物件的**execute**方法。 不過，當您想要保存命令文字並重新執行它，或使用查詢參數時，需要[command](../../../ado/reference/ado-api/command-object-ado.md)物件。  
  
-   使用[BeginTrans](../../../ado/reference/ado-api/begintrans-committrans-and-rollbacktrans-methods-ado.md)、 [CommitTrans](../../../ado/reference/ado-api/begintrans-committrans-and-rollbacktrans-methods-ado.md)和[RollbackTrans](../../../ado/reference/ado-api/begintrans-committrans-and-rollbacktrans-methods-ado.md)方法以及[Attributes](../../../ado/reference/ado-api/attributes-property-ado.md)屬性，管理開啟連接的交易，包括有提供者支援的嵌套交易。  
  
-   檢查從資料來源傳回的錯誤與[錯誤](../../../ado/reference/ado-api/errors-collection-ado.md)集合。  
  
-   從與[version](../../../ado/reference/ado-api/version-property-ado.md)屬性搭配使用的 ADO 執行中，讀取版本。  
  
-   使用[OpenSchema](../../../ado/reference/ado-api/openschema-method.md)方法取得資料庫的架構資訊。  
  
 您可以建立與任何其他先前定義之物件無關的**連接**物件。  
  
 您可以執行已命名的命令或預存程式，就像是**連接**物件上的原生方法一樣，如下一節所示。 當名為的命令與預存程式的名稱相同時，請在**連接**物件上叫用「原生方法呼叫」，一律執行已命名的命令，而不是 store 程式。  
  
> [!NOTE]
>  請勿在 Microsoft® .NET Framework 應用程式中使用這項功能（呼叫名為命令或預存程式，如同**連接**物件上的原生方法），因為功能的基礎執行與 .NET FRAMEWORK 與 COM 互通的方式相衝突。  
  
## <a name="execute-a-command-as-a-native-method-of-a-connection-object"></a>以連線物件的原生方法執行命令  
 若要執行命令，請使用**命令**物件[名稱](../../../ado/reference/ado-api/name-property-ado.md)屬性提供命令名稱。 將**命令**物件的**ActiveConnection**屬性設定為連接。 然後發出語句，其中的命令名稱會如同**連接**物件上的方法，後面接著任何參數，以及如果傳回任何資料列，則會使用**記錄集**物件。 設定**記錄集**屬性，以自訂產生的**記錄集**。 例如：  
  
```  
Dim cnn As New ADODB.Connection  
Dim cmd As New ADODB.Command  
Dim rst As New ADODB.Recordset  
...  
cnn.Open "..."  
cmd.Name = "yourCommandName"  
cmd.ActiveConnection = cnn  
...  
'Your command name, any parameters, and an optional Recordset.  
cnn. "parameter", rst  
```  
  
## <a name="execute-a-stored-procedure-as-a-native-method-of-a-connection-object"></a>以連線物件的原生方法執行預存程式  
 若要執行預存程式，請發出語句，其中預存程式名稱會用來當做**連接**物件上的方法，後面接著任何參數。 ADO 會對參數類型進行「最佳猜測」。 例如：  
  
```  
Dim cnn As New ADODB.Connection  
...  
'Your stored procedure name and any parameters.  
cnn. "parameter"  
```  
  
 **連接**物件可安全地進行腳本處理。  
  
 本章節包含下列主題。  
  
-   [Connection 物件屬性、方法和事件](../../../ado/reference/ado-api/connection-object-properties-methods-and-events.md)  
  
## <a name="see-also"></a>另請參閱  
 [Command 物件（ADO）](../../../ado/reference/ado-api/command-object-ado.md)   
 [Errors 集合（ADO）](../../../ado/reference/ado-api/errors-collection-ado.md)   
 [Properties 集合（ADO）](../../../ado/reference/ado-api/properties-collection-ado.md)   
 [Recordset 物件（ADO）](../../../ado/reference/ado-api/recordset-object-ado.md)   
 [附錄 A：提供者](../../../ado/guide/appendixes/appendix-a-providers.md)
