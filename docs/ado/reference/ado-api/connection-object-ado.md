---
description: Connection 物件 (ADO)
title: " (ADO) 的 Connection 物件 |Microsoft Docs"
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
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
ms.openlocfilehash: 38a28bf434998943b07ef6463970c26510195299
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/27/2020
ms.locfileid: "88974899"
---
# <a name="connection-object-ado"></a>Connection 物件 (ADO)
表示資料來源的開啟連接。  
  
## <a name="remarks"></a>備註  
 **Connection**物件代表與資料來源之間的唯一會話。 在用戶端/伺服器資料庫系統中，它可能相當於與伺服器的實際網路連接。 視提供者支援的功能而定，可能無法使用 **連接** 物件的某些集合、方法或屬性。  
  
 使用 **連接** 物件的集合、方法和屬性，您可以執行下列動作：  
  
-   在使用 [ConnectionString](./connectionstring-property-ado.md)、 [ConnectionTimeout](./connectiontimeout-property-ado.md)和 [Mode](./mode-property-ado.md) 屬性開啟連接之前，請先設定連線。 **ConnectionString** 是 **連接** 物件的預設屬性。  
  
-   將 [CursorLocation](./cursorlocation-property-ado.md) 屬性設定為 [用戶端]，以叫用 [OLE DB 的 Microsoft 資料指標服務](../../guide/appendixes/microsoft-cursor-service-for-ole-db-ado-service-component.md)，以支援批次更新。  
  
-   使用 [DefaultDatabase](./defaultdatabase-property.md) 屬性設定連接的預設資料庫。  
  
-   使用 [IsolationLevel](./isolationlevel-property.md) 屬性設定連接上開啟之交易的隔離層級。  
  
-   使用 [provider](./provider-property-ado.md) 屬性指定 OLE DB 提供者。  
  
-   使用 [Open](./open-method-ado-connection.md) 和 [Close](./close-method-ado.md) 方法建立及更新資料來源的實體連接。  
  
-   使用 [execute](./execute-method-ado-connection.md) 方法在連接上執行命令，並使用 [CommandTimeout](./commandtimeout-property-ado.md) 屬性來設定執行。  
  
    > [!NOTE]
    >  若要在不使用 Command 物件的情況下執行查詢，請將查詢字串傳遞至**連接**物件的**execute**方法。 但是，當您想要保存命令文字並重新執行它，或使用查詢參數時，需要 [command](./command-object-ado.md) 物件。  
  
-   管理開啟連接上的交易，包括具有 [BeginTrans](./begintrans-committrans-and-rollbacktrans-methods-ado.md)、 [CommitTrans](./begintrans-committrans-and-rollbacktrans-methods-ado.md)和 [RollbackTrans](./begintrans-committrans-and-rollbacktrans-methods-ado.md) 方法和 [Attributes](./attributes-property-ado.md) 屬性之提供者支援的嵌套交易（如果提供者支援的話）。  
  
-   檢查從資料來源傳回的錯誤，以及 [錯誤](./errors-collection-ado.md) 集合。  
  
-   從與 [version](./version-property-ado.md) 屬性搭配使用的 ADO 執行讀取版本。  
  
-   使用 [OpenSchema](./openschema-method.md) 方法取得資料庫的架構資訊。  
  
 您可以建立與任何其他先前定義之物件無關的 **連接** 物件。  
  
 您可以執行指定的命令或預存程式，就像是 **連接** 物件上的原生方法一樣，如下一節所示。 當命名命令的名稱與預存程式的名稱相同時，請在 **連接** 物件上叫用「原生方法呼叫」，一律執行已命名的命令，而不是儲存程式。  
  
> [!NOTE]
>  請勿使用這項功能 (呼叫名為的命令或預存程式，就像是在 Microsoft® .NET Framework 應用程式中) 的 **連接** 物件上的原生方法一樣，因為功能的基礎實與 .NET FRAMEWORK 與 COM 交互操作的方式相衝突。  
  
## <a name="execute-a-command-as-a-native-method-of-a-connection-object"></a>以連線物件的原生方法來執行命令  
 若要執行命令，請使用 [ **命令** 物件 [名稱](./name-property-ado.md) ] 屬性指定命令名稱。 將**命令**物件的**ActiveConnection**屬性設定為連接。 然後發出語句，其中命令名稱會用來當做 **連接** 物件上的方法，後面接著任何參數，而如果傳回任何資料列，則會使用 **記錄集** 物件。 設定 **記錄集** 屬性，以自訂產生的 **記錄集**。 例如：  
  
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
 若要執行預存程式，請發出語句，其使用預存程式名稱，如同 **連接** 物件上的方法，後面接著任何參數。 ADO 將會產生「最佳猜測」的參數類型。 例如：  
  
```  
Dim cnn As New ADODB.Connection  
...  
'Your stored procedure name and any parameters.  
cnn. "parameter"  
```  
  
 **連接**物件可以安全地進行腳本處理。  
  
 本節包含下列主題。  
  
-   [Connection 物件屬性、方法和事件](./connection-object-properties-methods-and-events.md)  
  
## <a name="see-also"></a>另請參閱  
 [ (ADO) 的命令物件 ](./command-object-ado.md)   
 [ (ADO) 收集錯誤 ](./errors-collection-ado.md)   
 [ (ADO) 的屬性集合 ](./properties-collection-ado.md)   
 [ (ADO) 的記錄集物件 ](./recordset-object-ado.md)   
 [附錄 A：提供者](../../guide/appendixes/appendix-a-providers.md)