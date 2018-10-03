---
title: ConnectionString 屬性 (ADO) |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Connection15::ConnectionString
helpviewer_keywords:
- ConnectionString property [ADO]
ms.assetid: 3be75b75-4d36-4479-ab64-9a456869252a
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 01a930bc571e84c6ecfd38ce8415493c90ebd377
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47828894"
---
# <a name="connectionstring-property-ado"></a>ConnectionString 屬性 (ADO)
表示用來連接到資料來源的資訊。  
  
## <a name="settings-and-return-values"></a>設定和傳回值  
 設定或傳回**字串**值。  
  
## <a name="remarks"></a>備註  
 使用**ConnectionString**屬性來指定資料來源，藉由傳遞詳細的連接字串，包含一系列*引數* *= value*陳述式分隔分號。  
  
 ADO 支援五個引數**ConnectionString**屬性; 直接與提供者，而不進行任何處理 ADO 的任何其他引數傳遞。 引數 ADO 支援如下所示。  
  
|引數|描述|  
|--------------|-----------------|  
|*提供者 =*|指定要用於連線提供者的名稱。|  
|*檔名 =*|指定提供者特定檔案名稱 （例如，保存的資料來源物件） 包含預設的連接資訊。|  
|*遠端提供者 =*|指定開啟用戶端連接時使用的提供者的名稱。 （僅限遠端資料服務。）|  
|*遠端伺服器 =*|指定要開啟用戶端連線時所使用的伺服器的路徑名稱。 （僅限遠端資料服務。）|  
|*URL=*|指定的連接字串做為識別的資源，例如檔案或目錄的絕對 URL。|  
  
 在設定後**ConnectionString**屬性，並開啟[連線](../../../ado/reference/ado-api/connection-object-ado.md)物件，提供者可能會改變內容的屬性，比方說，藉由對應至 ADO 定義的引數名稱及其對等項目特定的提供者。  
  
 **ConnectionString**屬性會自動繼承所使用的值*ConnectionString*引數[開啟](../../../ado/reference/ado-api/open-method-ado-connection.md)方法，所以您可以覆寫目前**ConnectionString**期間的屬性**開啟**方法呼叫。  
  
 因為*檔名*引數會導致載入相關聯的提供者的 ADO 中，您無法將兩者都傳遞*提供者*並*檔案名稱*引數。  
  
 **ConnectionString**屬性是讀取/寫入，當連接已關閉，且為唯讀狀態開啟時。  
  
 中的引數的重複項目**ConnectionString**屬性會被忽略。 使用任何引數的最後一個執行個體。  
  
> [!NOTE]
>  **遠端資料服務使用量**用戶端上使用時**連接**物件**ConnectionString**屬性可以只包含*遠端提供者*並*遠端伺服器*參數。  
  
 下表列出每個 Windows 作業系統的預設 ADO 提供者：  
  
|預設 ADO 提供者|Windows 作業系統|  
|--------------------------|------------------------------|  
|MSDASQL<br /><br /> （若要改善原始程式碼的可讀性，明確指定的提供者名稱的連接字串中）。|Windows 2000 （32 位元）<br /><br /> Windows XP （32 位元）<br /><br /> Windows 2003 Server （32 位元）<br /><br /> Windows Vista （32 位元）<br /><br /> Windows Vista Service Pack 1 或更新版本 （32 位元和 64 位元）<br /><br /> Windows Vista （32 位元和 64 位元） 之後的 Windows 版本|  
|沒有預設值。<br /><br /> 當 ADO 應用程式會在下列作業系統上執行，並不會明確地指定提供者時，ADO 會傳回下列錯誤: 「 ADODB。連接： 未指定提供者，而且沒有指定的預設提供者 」|Windows 2000 （64 位元）<br /><br /> Windows XP （64 位元）<br /><br /> Windows 2003 Server （64 位元）<br /><br /> Windows Vista （64 位元）|  
  
## <a name="applies-to"></a>適用於  
 [Connection 物件 (ADO)](../../../ado/reference/ado-api/connection-object-ado.md)  
  
## <a name="see-also"></a>另請參閱  
 [ConnectionString、 ConnectionTimeout 和 State 屬性範例 (VB)](../../../ado/reference/ado-api/connectionstring-connectiontimeout-and-state-properties-example-vb.md)   
 [ConnectionString、 ConnectionTimeout 和狀態的屬性範例 （VC + +）](../../../ado/reference/ado-api/connectionstring-connectiontimeout-and-state-properties-example-vc.md)   
 [附錄 A：提供者](../../../ado/guide/appendixes/appendix-a-providers.md)
