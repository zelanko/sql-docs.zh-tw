---
title: "連接物件 (ADO) |Microsoft 文件"
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
apitype: COM
f1_keywords:
- Connection
helpviewer_keywords:
- Connection object [ADO]
ms.assetid: ef6b1824-5b12-43db-89d7-8f3d13896d4d
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: be2ba43e34c56e19dcb6eee03368ab1b3bc442a1
ms.contentlocale: zh-tw
ms.lasthandoff: 09/09/2017

---
# <a name="connection-object-ado"></a>連接物件 (ADO)
代表資料來源的開啟連接。  
  
## <a name="remarks"></a>備註  
 A**連接**物件都代表資料來源的唯一工作階段。 在用戶端/伺服器資料庫系統中，可能相當於實際的網路連線到伺服器。 根據提供者、 某些集合、 方法或屬性所支援的功能**連接**物件可能無法使用。  
  
 使用集合、 方法和屬性的**連接**物件，您可以執行下列：  
  
-   設定的連接，再開啟它與[ConnectionString](../../../ado/reference/ado-api/connectionstring-property-ado.md)， [ConnectionTimeout](../../../ado/reference/ado-api/connectiontimeout-property-ado.md)，和[模式](../../../ado/reference/ado-api/mode-property-ado.md)屬性。 **ConnectionString**是預設屬性**連接**物件。  
  
-   設定[CursorLocation](../../../ado/reference/ado-api/cursorlocation-property-ado.md)屬性給要叫用戶端[Microsoft OLE DB 的資料指標服務](../../../ado/guide/appendixes/microsoft-cursor-service-for-ole-db-ado-service-component.md)，它支援以批次更新。  
  
-   設定與連線的預設資料庫[DefaultDatabase](../../../ado/reference/ado-api/defaultdatabase-property.md)屬性。  
  
-   設定與連接開啟的交易隔離等級[IsolationLevel](../../../ado/reference/ado-api/isolationlevel-property.md)屬性。  
  
-   指定 OLE DB 提供者與[提供者](../../../ado/reference/ado-api/provider-property-ado.md)屬性。  
  
-   建立及稍後中斷與資料來源的實體連線[開啟](../../../ado/reference/ado-api/open-method-ado-connection.md)和[關閉](../../../ado/reference/ado-api/close-method-ado.md)方法。  
  
-   連接上執行命令[Execute](../../../ado/reference/ado-api/execute-method-ado-connection.md)方法和設定與執行[CommandTimeout](../../../ado/reference/ado-api/commandtimeout-property-ado.md)屬性。  
  
    > [!NOTE]
    >  若要執行查詢，而不使用命令物件，將傳遞查詢字串以**Execute**方法**連接**物件。 不過，[命令](../../../ado/reference/ado-api/command-object-ado.md)物件時，需要您想要保存的命令文字，並重新執行它，或使用查詢參數。  
  
-   管理開啟連線時，如果提供者支援，包括巢狀的交易的交易[BeginTrans](../../../ado/reference/ado-api/begintrans-committrans-and-rollbacktrans-methods-ado.md)， [CommitTrans](../../../ado/reference/ado-api/begintrans-committrans-and-rollbacktrans-methods-ado.md)，和[RollbackTrans](../../../ado/reference/ado-api/begintrans-committrans-and-rollbacktrans-methods-ado.md)方法和[屬性](../../../ado/reference/ado-api/attributes-property-ado.md)屬性。  
  
-   檢查與資料來源傳回的錯誤[錯誤](../../../ado/reference/ado-api/errors-collection-ado.md)集合。  
  
-   讀取版本搭配使用 ADO 實作[版本](../../../ado/reference/ado-api/version-property-ado.md)屬性。  
  
-   取得與資料庫的結構描述資訊[OpenSchema](../../../ado/reference/ado-api/openschema-method.md)方法。  
  
 您可以建立**連接**獨立於任何其他先前定義的物件的物件。  
  
 您如同原生方法上可執行具名的命令或預存程序**連接**物件下, 一節所示。 當具名的命令有相同的預存程序名稱時，叫用 「 原生方法呼叫 」 上**連接**物件一律會執行具名的命令，而不是預存程序。  
  
> [!NOTE]
>  不使用此功能 (就好像原生方法上呼叫的具名的命令或預存程序**連接**物件) 在 Microsoft®.NET Framework 應用程式，因為基礎實作的功能衝突方式與.NET Framework 可與 COM 互通  
  
## <a name="execute-a-command-as-a-native-method-of-a-connection-object"></a>以原生連接物件的方法中執行命令  
 若要執行命令時，提供的命令名稱，使用**命令**物件[名稱](../../../ado/reference/ado-api/name-property-ado.md)屬性。 設定**ActiveConnection**屬性**命令**連接物件。 接著發出命令名稱使用，就好像方法上的陳述式**連接**物件，後面接著任何參數，而**資料錄集**如果會傳回任何資料列的物件。 設定**資料錄集**屬性，以自訂產生**資料錄集**。 例如：  
  
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
  
## <a name="execute-a-stored-procedure-as-a-native-method-of-a-connection-object"></a>執行預存程序為原生連接物件的方法  
 若要執行預存程序，會發出陳述式的預存程序名稱使用，就好像方法上**連接**物件，後面接著任何參數。 ADO 可以將參數類型的 「 最佳猜測"。 例如：  
  
```  
Dim cnn As New ADODB.Connection  
...  
'Your stored procedure name and any parameters.  
cnn. "parameter"  
```  
  
 **連接**物件而言是安全的指令碼。  
  
 本章節包含下列主題。  
  
-   [連接物件屬性、 方法和事件](../../../ado/reference/ado-api/connection-object-properties-methods-and-events.md)  
  
## <a name="see-also"></a>另請參閱  
 [命令物件 (ADO)](../../../ado/reference/ado-api/command-object-ado.md)   
 [錯誤集合 (ADO)](../../../ado/reference/ado-api/errors-collection-ado.md)   
 [屬性集合 (ADO)](../../../ado/reference/ado-api/properties-collection-ado.md)   
 [資料錄集物件 (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)   
 [附錄 a： 提供者](../../../ado/guide/appendixes/appendix-a-providers.md)

