---
title: 連接物件 (ADO) |Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 701ced4f5e0ad511f4a1c5b39c9775e285d1f751
ms.sourcegitcommit: 074d44994b6e84fe4552ad4843d2ce0882b92871
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/05/2019
ms.locfileid: "66695785"
---
# <a name="connection-object-ado"></a>Connection 物件 (ADO)
表示資料來源的開啟連接。  
  
## <a name="remarks"></a>備註  
 A**連線**物件都代表資料來源的唯一工作階段。 在用戶端/伺服器資料庫系統中，它可能會相當於實際的網路連線至伺服器程式碼。 根據提供者、 某些集合、 方法或屬性所支援的功能**連線**物件可能無法使用。  
  
 使用集合、 方法和屬性的**連線**物件時，您可以執行下列動作：  
  
-   設定的連接，再開啟它[ConnectionString](../../../ado/reference/ado-api/connectionstring-property-ado.md)， [ConnectionTimeout](../../../ado/reference/ado-api/connectiontimeout-property-ado.md)，並[模式](../../../ado/reference/ado-api/mode-property-ado.md)屬性。 **ConnectionString**是預設屬性**連線**物件。  
  
-   設定[CursorLocation](../../../ado/reference/ado-api/cursorlocation-property-ado.md)屬性，以叫用的用戶端[Microsoft OLE DB 的資料指標服務](../../../ado/guide/appendixes/microsoft-cursor-service-for-ole-db-ado-service-component.md)，也支援以批次更新。  
  
-   設定與連線的預設資料庫[DefaultDatabase](../../../ado/reference/ado-api/defaultdatabase-property.md)屬性。  
  
-   集合的交易隔離層級開啟連接[IsolationLevel](../../../ado/reference/ado-api/isolationlevel-property.md)屬性。  
  
-   指定具有 OLE DB 提供者[提供者](../../../ado/reference/ado-api/provider-property-ado.md)屬性。  
  
-   建立此項目，並稍後中斷與資料來源的實體連線[開放](../../../ado/reference/ado-api/open-method-ado-connection.md)並[關閉](../../../ado/reference/ado-api/close-method-ado.md)方法。  
  
-   連接上執行命令[Execute](../../../ado/reference/ado-api/execute-method-ado-connection.md)方法，並設定與執行[CommandTimeout](../../../ado/reference/ado-api/commandtimeout-property-ado.md)屬性。  
  
    > [!NOTE]
    >  若要執行查詢，而不需使用命令物件，將傳遞查詢字串，以**Execute**方法**連線**物件。 不過，[命令](../../../ado/reference/ado-api/command-object-ado.md)物件時，需要您想要保存的命令文字和重新執行，或使用查詢參數。  
  
-   管理開啟的連接，包括巢狀的交易，如果提供者所支援的是，使用上的交易[BeginTrans](../../../ado/reference/ado-api/begintrans-committrans-and-rollbacktrans-methods-ado.md)， [CommitTrans](../../../ado/reference/ado-api/begintrans-committrans-and-rollbacktrans-methods-ado.md)，並[RollbackTrans](../../../ado/reference/ado-api/begintrans-committrans-and-rollbacktrans-methods-ado.md)方法和[屬性](../../../ado/reference/ado-api/attributes-property-ado.md)屬性。  
  
-   檢查是否有與資料來源傳回的錯誤[錯誤](../../../ado/reference/ado-api/errors-collection-ado.md)集合。  
  
-   從 ADO 實作搭配讀取版本[版本](../../../ado/reference/ado-api/version-property-ado.md)屬性。  
  
-   取得有關您的資料庫結構描述資訊[OpenSchema](../../../ado/reference/ado-api/openschema-method.md)方法。  
  
 您可以建立**連線**獨立於任何其他先前定義的物件的物件。  
  
 您可以執行的具名的命令或預存程序如同他們先前所在的原生方法**連線**物件下, 一節中所示。 當具名的命令具有相同名稱的預存程序時，叫用 「 原生方法呼叫 」 上**連線**物件一定會執行具名的命令，而不是預存程序。  
  
> [!NOTE]
>  不使用此功能 (呼叫具名的命令或預存程序，它就彷彿的原生方法上**連線**物件) 中的 Microsoft®.NET Framework 應用程式，因為基礎實作的功能衝突方法在.NET Framework 交互操作 com。  
  
## <a name="execute-a-command-as-a-native-method-of-a-connection-object"></a>執行命令做為連接物件的原生方法  
 若要執行命令時，提供的命令名稱，使用**命令**物件[名稱](../../../ado/reference/ado-api/name-property-ado.md)屬性。 設定**ActiveConnection**屬性**命令**連接的物件。 接著發出的命令名稱使用，就好像方法上的陳述式**連接**物件，後面接著任何參數，以及**資料錄集**物件如果會傳回任何資料列。 設定**Recordset**屬性，以自訂產生**資料錄集**。 例如：  
  
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
  
## <a name="execute-a-stored-procedure-as-a-native-method-of-a-connection-object"></a>執行預存程序做為連接物件的原生方法  
 若要執行預存程序，會發出陳述式，就好像方法上會使用預存程序名稱的地方**連線**物件，後面接著任何參數。 ADO 將參數類型的 「 最佳猜測"。 例如：  
  
```  
Dim cnn As New ADODB.Connection  
...  
'Your stored procedure name and any parameters.  
cnn. "parameter"  
```  
  
 **連線**物件而言是安全的指令碼。  
  
 本章節包含下列主題。  
  
-   [連接物件屬性、 方法和事件](../../../ado/reference/ado-api/connection-object-properties-methods-and-events.md)  
  
## <a name="see-also"></a>另請參閱  
 [Command 物件 (ADO)](../../../ado/reference/ado-api/command-object-ado.md)   
 [Errors 集合 (ADO)](../../../ado/reference/ado-api/errors-collection-ado.md)   
 [屬性集合 (ADO)](../../../ado/reference/ado-api/properties-collection-ado.md)   
 [資料錄集物件 (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)   
 [附錄 A：提供者](../../../ado/guide/appendixes/appendix-a-providers.md)
