---
title: Open 方法（ADO Connection） |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Connection15::raw_Open
- Connection15::Open
- _Connection::Open
helpviewer_keywords:
- Open method [ADO]
ms.assetid: 663defab-5545-4973-9036-24d5882c9737
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 15115313613ea8f86dd2267c6be3c231cab92503
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "67931935"
---
# <a name="open-method-ado-connection"></a>Open 方法 (ADO Connection)
開啟與資料來源的連接。  
  
## <a name="syntax"></a>語法  
  
```  
  
connection.Open ConnectionString, UserID, Password, Options  
```  
  
#### <a name="parameters"></a>參數  
 *ConnectionString*  
 選擇性。 包含連接資訊的**字串**值。 如需有效設定的詳細資訊，請參閱[ConnectionString](../../../ado/reference/ado-api/connectionstring-property-ado.md)屬性。  
  
 *UserID*  
 選擇性。 **字串**值，其中包含建立連接時所要使用的使用者名稱。  
  
 *密碼*  
 選擇性。 **字串**值，其中包含建立連接時所要使用的密碼。  
  
 *選項*  
 選擇性。 [ConnectOptionEnum](../../../ado/reference/ado-api/connectoptionenum.md)值，判斷這個方法是否應在建立連接之後（同步）或之前（非同步）傳回。  
  
## <a name="remarks"></a>備註  
 在[連接](../../../ado/reference/ado-api/connection-object-ado.md)物件上使用**Open**方法，會建立與資料來源的實體連接。 這個方法順利完成之後，連接就會上線，您可以對它發出命令並處理結果。  
  
 使用選擇性的*ConnectionString*引數來指定包含一連串*argument* *= 值*語句（以分號分隔）的連接字串，或是以 URL 識別的檔案或目錄資源。 **Connectionstring**屬性會自動繼承用於*ConnectionString*引數的值。 因此，您可以在開啟**連接**物件之前先設定它的**connectionstring**屬性，或是在**Open**方法呼叫期間使用*ConnectionString*引數來設定或覆寫目前的連接參數。  
  
 如果您在*connectionstring*引數和選擇性*UserID*和*password*引數中傳遞使用者和密碼資訊， *UserID*和*password*引數將會覆寫*ConnectionString*中指定的值。  
  
 當您已透過開啟的連線結束作業時，請使用[Close](../../../ado/reference/ado-api/close-method-ado.md)方法來釋放任何相關**聯的系統**資源。 關閉物件並不會將它從記憶體中移除;您可以變更其屬性設定，並使用**open**方法，稍後再重新開啟它。 若要完全排除記憶體中的物件，請將物件變數設為 [*無*]。  
  
> [!NOTE]
>  **遠端資料服務使用量**在用戶端**連接**物件上使用時，在**連接**物件上開啟[記錄集](../../../ado/reference/ado-api/recordset-object-ado.md)之前， **Open**方法實際上不會建立與伺服器的連接。  
  
> [!NOTE]
>  使用 HTTP 配置的 Url 會自動叫用[Microsoft OLE DB 提供者以進行網際網路發佈](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-internet-publishing.md)。 如需詳細資訊，請參閱[絕對和相對 url](../../../ado/guide/data/absolute-and-relative-urls.md)。  
  
## <a name="applies-to"></a>套用至  
 [Connection 物件 (ADO)](../../../ado/reference/ado-api/connection-object-ado.md)  
  
## <a name="see-also"></a>另請參閱  
 [Open 和 Close 方法範例（VB）](../../../ado/reference/ado-api/open-and-close-methods-example-vb.md)   
 [Open 和 Close 方法範例（VBScript）](../../../ado/reference/ado-api/open-and-close-methods-example-vbscript.md)   
 [Open 和 Close 方法範例（VC + +）](../../../ado/reference/ado-api/open-and-close-methods-example-vc.md)   
 [Open 方法（ADO Record）](../../../ado/reference/ado-api/open-method-ado-record.md)   
 [Open 方法（ADO Recordset）](../../../ado/reference/ado-api/open-method-ado-recordset.md)   
 [Open 方法（ADO Stream）](../../../ado/reference/ado-api/open-method-ado-stream.md)   
 [OpenSchema 方法](../../../ado/reference/ado-api/openschema-method.md)
