---
title: Open 方法 （ADO 連接） |Microsoft 文件
ms.prod: sql
ms.prod_service: connectivity
ms.component: ado
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Connection15::raw_Open
- Connection15::Open
- _Connection::Open
helpviewer_keywords:
- Open method [ADO]
ms.assetid: 663defab-5545-4973-9036-24d5882c9737
caps.latest.revision: 13
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 252afc6de9b6cf405fba7ae21a191beef2c198e7
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="open-method-ado-connection"></a>Open 方法 （ADO 連接）
開啟資料來源的連接。  
  
## <a name="syntax"></a>語法  
  
```  
  
connection.Open ConnectionString, UserID, Password, Options  
```  
  
#### <a name="parameters"></a>參數  
 *ConnectionString*  
 選擇性。 A**字串**包含連接資訊的值。 請參閱[ConnectionString](../../../ado/reference/ado-api/connectionstring-property-ado.md)屬性，如需有效的設定詳細資料。  
  
 *使用者識別碼*  
 選擇性。 A**字串**包含使用者名稱以建立連接時使用的值。  
  
 *密碼*  
 選擇性。 A**字串**值，包含要建立連線時所使用的密碼。  
  
 *選項。*  
 選擇性。 A [ConnectOptionEnum](../../../ado/reference/ado-api/connectoptionenum.md)值，決定是否此方法應傳回之後 （同步） 或之前 （非同步） 建立連線。  
  
## <a name="remarks"></a>備註  
 使用**開啟**方法[連接](../../../ado/reference/ado-api/connection-object-ado.md)物件建立資料來源的實體連接。 這個方法順利完成之後，連接即時且您可以針對它發出命令，並處理結果。  
  
 使用選擇性*ConnectionString*引數來指定其中一個連接字串，包含一系列的*引數* *= value*陳述式以分號分隔，或檔案或目錄資源的 url 識別。 **ConnectionString**屬性會自動繼承所使用的值*ConnectionString*引數。 因此，您可以設定**ConnectionString**屬性**連接**物件，然後再開啟它，或使用*ConnectionString*引數來設定或覆寫在目前的連接參數**開啟**方法呼叫。  
  
 如果您要傳入使用者名稱和密碼資訊這兩個*ConnectionString*引數和選擇性*UserID*和*密碼*引數，*使用者識別碼*和*密碼*引數會覆寫中指定的值*ConnectionString*。  
  
 當您透過開啟得到您的作業**連接**，使用[關閉](../../../ado/reference/ado-api/close-method-ado.md)方法來釋放任何相關聯的系統資源。 關閉物件不會將它從記憶體中移除您可以變更其屬性設定，並使用**開啟**方法，以在稍後重新開啟它。 若要完全消除從記憶體物件，設定為物件變數*Nothing*。  
  
> [!NOTE]
>  **遠端資料服務使用量**使用用戶端時**連接**物件**開啟**方法不會實際連接到伺服器，直到[資料錄集](../../../ado/reference/ado-api/recordset-object-ado.md)上開啟**連接**物件。  
  
> [!NOTE]
>  使用 http 配置 Url 將會自動叫用[Microsoft OLE DB Provider for Internet Publishing](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-internet-publishing.md)。 如需詳細資訊，請參閱[絕對和相對 Url](../../../ado/guide/data/absolute-and-relative-urls.md)。  
  
## <a name="applies-to"></a>適用於  
 [Connection 物件 (ADO)](../../../ado/reference/ado-api/connection-object-ado.md)  
  
## <a name="see-also"></a>另請參閱  
 [開啟與關閉方法範例 (VB)](../../../ado/reference/ado-api/open-and-close-methods-example-vb.md)   
 [開啟與關閉方法範例 (VBScript)](../../../ado/reference/ado-api/open-and-close-methods-example-vbscript.md)   
 [開啟與關閉方法範例 （VC + +）](../../../ado/reference/ado-api/open-and-close-methods-example-vc.md)   
 [Open 方法 （ADO 資料錄）](../../../ado/reference/ado-api/open-method-ado-record.md)   
 [Open 方法 （ADO 資料錄集）](../../../ado/reference/ado-api/open-method-ado-recordset.md)   
 [Open 方法 （ADO 資料流）](../../../ado/reference/ado-api/open-method-ado-stream.md)   
 [OpenSchema 方法](../../../ado/reference/ado-api/openschema-method.md)
