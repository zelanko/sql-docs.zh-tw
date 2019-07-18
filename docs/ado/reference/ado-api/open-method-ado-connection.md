---
title: Open 方法 (ADO Connection) |Microsoft Docs
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
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/15/2019
ms.locfileid: "67931935"
---
# <a name="open-method-ado-connection"></a>Open 方法 (ADO Connection)
開啟資料來源的連接。  
  
## <a name="syntax"></a>語法  
  
```  
  
connection.Open ConnectionString, UserID, Password, Options  
```  
  
#### <a name="parameters"></a>參數  
 *ConnectionString*  
 選擇性。 A**字串**包含連接資訊的值。 請參閱[ConnectionString](../../../ado/reference/ado-api/connectionstring-property-ado.md)屬性，如需有關有效的設定。  
  
 *UserID*  
 選擇性。 A**字串**值，其中包含要建立連接時使用的使用者名稱。  
  
 *密碼*  
 選擇性。 A**字串**值，其中包含要建立連線時所使用的密碼。  
  
 *選項。*  
 選擇性。 A [ConnectOptionEnum](../../../ado/reference/ado-api/connectoptionenum.md)值，決定是否此方法應傳回之後 （同步） 或之前 （非同步） 建立連線。  
  
## <a name="remarks"></a>備註  
 使用**開放**方法[連線](../../../ado/reference/ado-api/connection-object-ado.md)物件建立與資料來源的實體連接。 這個方法成功完成後，連線即時且您可以對它發出命令，並處理結果。  
  
 使用選擇性*ConnectionString*引數來指定連接字串包含一系列*引數* *= value*以分號分隔的陳述式或識別具有 URL 的檔案或目錄資源。 **ConnectionString**屬性會自動繼承所使用的值*ConnectionString*引數。 因此，您可以設定**ConnectionString**屬性**連線**物件，然後再開啟它，或使用*ConnectionString*引數來設定或覆寫在目前的連接參數**開啟**方法呼叫。  
  
 如果您傳遞的使用者名稱和密碼資訊這兩個*ConnectionString*引數和選擇性*UserID*並*密碼*引數， *UserID*並*密碼*引數會覆寫中指定的值*ConnectionString*。  
  
 當您透過開啟完成您的作業**連接**，使用[關閉](../../../ado/reference/ado-api/close-method-ado.md)方法來釋放任何相關聯的系統資源。 關閉物件不會將它從記憶體中; 中移除您可以變更其屬性設定，並使用**開啟**稍後再重新開啟它的方法。 若要完全排除記憶體中的物件，設定為物件變數*Nothing*。  
  
> [!NOTE]
>  **遠端資料服務使用量**用戶端上使用時**連接**物件**開啟**方法並不實際連接到伺服器之前[資料錄集](../../../ado/reference/ado-api/recordset-object-ado.md)上開啟**連線**物件。  
  
> [!NOTE]
>  使用 http 配置 Url 將會自動叫用[Microsoft OLE DB Provider for Internet Publishing](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-internet-publishing.md)。 如需詳細資訊，請參閱 <<c0> [ 絕對和相對 Url](../../../ado/guide/data/absolute-and-relative-urls.md)。  
  
## <a name="applies-to"></a>適用於  
 [Connection 物件 (ADO)](../../../ado/reference/ado-api/connection-object-ado.md)  
  
## <a name="see-also"></a>另請參閱  
 [Open 和 Close 方法範例 (VB)](../../../ado/reference/ado-api/open-and-close-methods-example-vb.md)   
 [Open 和 Close 方法範例 (VBScript)](../../../ado/reference/ado-api/open-and-close-methods-example-vbscript.md)   
 [Open 和 Close 方法範例 （VC + +）](../../../ado/reference/ado-api/open-and-close-methods-example-vc.md)   
 [Open 方法 （ADO 記錄）](../../../ado/reference/ado-api/open-method-ado-record.md)   
 [Open 方法 (ADO Recordset)](../../../ado/reference/ado-api/open-method-ado-recordset.md)   
 [Open 方法 (ADO Stream)](../../../ado/reference/ado-api/open-method-ado-stream.md)   
 [OpenSchema 方法](../../../ado/reference/ado-api/openschema-method.md)
