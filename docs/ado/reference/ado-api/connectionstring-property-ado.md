---
title: "ConnectionString 屬性 (ADO) |Microsoft 文件"
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
- Connection15::ConnectionString
helpviewer_keywords:
- ConnectionString property [ADO]
ms.assetid: 3be75b75-4d36-4479-ab64-9a456869252a
caps.latest.revision: 18
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 34db69d25ff835de4f8c81d252c99017ae4acbb5
ms.contentlocale: zh-tw
ms.lasthandoff: 09/09/2017

---
# <a name="connectionstring-property-ado"></a>ConnectionString 屬性 (ADO)
表示用來連接到資料來源的資訊。  
  
## <a name="settings-and-return-values"></a>設定和傳回值  
 設定或傳回**字串**值。  
  
## <a name="remarks"></a>備註  
 使用**ConnectionString**屬性來指定資料來源，藉由傳遞詳細的連接字串，包含一系列的*引數* *= value*陳述式隔開分號。  
  
 ADO 支援五個引數的**ConnectionString**屬性; 直接到而不進行任何處理由 ADO 提供者的其他引數傳遞。 引數 ADO 支援如下所示。  
  
|引數|Description|  
|--------------|-----------------|  
|*提供者 =*|指定要用於連接的提供者的名稱。|  
|*檔案名稱 =*|指定的提供者特定的檔案 （例如，保存的資料來源物件） 包含預設的連接資訊的名稱。|  
|*遠端提供者 =*|指定開啟用戶端連接時使用的提供者的名稱。 （僅限遠端資料服務。）|  
|*遠端伺服器 =*|指定要開啟的用戶端連接時使用的伺服器的路徑名稱。 （僅限遠端資料服務。）|  
|*URL =*|指定的連接字串，以做為識別的資源，例如檔案或目錄的絕對 URL。|  
  
 設定之後**ConnectionString**屬性，並開啟[連接](../../../ado/reference/ado-api/connection-object-ado.md)物件，提供者可能會改變屬性的內容，例如藉由對應至 ADO 定義引數名稱及其對等項目特定的提供者。  
  
 **ConnectionString**屬性會自動繼承所使用的值*ConnectionString*引數的[開啟](../../../ado/reference/ado-api/open-method-ado-connection.md)方法，所以您可以覆寫目前**ConnectionString**屬性期間**開啟**方法呼叫。  
  
 因為*檔案名稱*引數可讓 ADO 載入相關聯的提供者，您不可以同時傳送*提供者*和*檔案名稱*引數。  
  
 **ConnectionString**屬性是讀取/寫入，當連接已關閉，且為唯讀模式開啟時。  
  
 中的引數的重複項目**ConnectionString**屬性會被忽略。 會使用任何引數的最後一個執行個體。  
  
> [!NOTE]
>  **遠端資料服務使用量**使用用戶端時**連接**物件**ConnectionString**屬性只可包含*遠端提供者*和*遠端伺服器*參數。  
  
 下表列出每個 Windows 作業系統的預設 ADO 提供者：  
  
|預設 ADO 提供者|Windows 作業系統|  
|--------------------------|------------------------------|  
|MSDASQL<br /><br /> （若要改善原始碼的可讀性，明確指定的提供者名稱的連接字串中。）|Windows 2000 （32 位元）<br /><br /> Windows XP （32 位元）<br /><br /> Windows 2003 Server （32 位元）<br /><br /> Windows Vista （32 位元）<br /><br /> Windows Vista Service Pack 1 或更新版本 （32 位元和 64 位元）<br /><br /> 在 Windows Vista （32 位元和 64 位元） 後的 Windows 版本|  
|沒有預設值。<br /><br /> 當 ADO 應用程式會在下列作業系統上執行，且未明確指定提供者時，ADO 會傳回下列錯誤: 「 ADODB。連線： 未指定提供者並沒有指定的預設提供者 」|Windows 2000 （64 位元）<br /><br /> Windows XP （64 位元）<br /><br /> Windows 2003 Server （64 位元）<br /><br /> Windows Vista （64 位元）|  
  
## <a name="applies-to"></a>適用於  
 [連接物件 (ADO)](../../../ado/reference/ado-api/connection-object-ado.md)  
  
## <a name="see-also"></a>另請參閱  
 [ConnectionString、 ConnectionTimeout 和 State 屬性範例 (VB)](../../../ado/reference/ado-api/connectionstring-connectiontimeout-and-state-properties-example-vb.md)   
 [ConnectionString、 ConnectionTimeout 和 State 屬性範例 （VC + +）](../../../ado/reference/ado-api/connectionstring-connectiontimeout-and-state-properties-example-vc.md)   
 [附錄 a： 提供者](../../../ado/guide/appendixes/appendix-a-providers.md)

