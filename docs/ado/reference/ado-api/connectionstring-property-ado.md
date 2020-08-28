---
description: ConnectionString 屬性 (ADO)
title: " (ADO) 的 ConnectionString 屬性 |Microsoft Docs"
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
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
author: rothja
ms.author: jroth
ms.openlocfilehash: 2add76a640e89bebe8a941afa5896bb2300750a9
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/27/2020
ms.locfileid: "88974769"
---
# <a name="connectionstring-property-ado"></a>ConnectionString 屬性 (ADO)
表示用來建立資料來源連接的資訊。  
  
## <a name="settings-and-return-values"></a>設定和傳回值  
 設定或傳回 **字串** 值。  
  
## <a name="remarks"></a>備註  
 您可以使用 **ConnectionString** 屬性來指定資料來源，方法是傳遞包含一連串 *引數* *= value* 語句的詳細連接字串（以分號分隔）。  
  
 ADO 支援 **ConnectionString** 屬性的五個引數;任何其他引數都會直接傳遞給提供者，而不會由 ADO 處理。 ADO 支援的引數如下所示。  
  
|引數|描述|  
|--------------|-----------------|  
|*提供者 =*|指定連接所要使用之提供者的名稱。|  
|*檔案名 =*|指定提供者特定檔案的名稱 (例如，保存的資料來源物件) 包含預設的連接資訊。|  
|*遠端提供者 =*|指定開啟用戶端連接時要使用的提供者名稱。  (僅限遠端資料服務。 ) |  
|*遠端伺服器 =*|指定開啟用戶端連接時要使用之伺服器的路徑名稱。  (僅限遠端資料服務。 ) |  
|*URL =*|將連接字串指定為識別資源的絕對 URL，例如檔案或目錄。|  
  
 設定 **ConnectionString** 屬性並開啟 [連接](./connection-object-ado.md) 物件之後，提供者可以改變屬性的內容，例如，將 ADO 定義的引數名稱對應至特定提供者的對等專案。  
  
 **Connectionstring**屬性會自動繼承[Open](./open-method-ado-connection.md)方法的*ConnectionString*引數所使用的值，因此您可以在**open**方法呼叫期間覆寫目前的**ConnectionString**屬性。  
  
 因為 *檔案名* 引數會導致 ADO 載入關聯的提供者，所以您無法同時傳遞 *提供者* 和 *檔案名* 引數。  
  
 當連線關閉時，會讀取/寫入 **ConnectionString** 屬性，而當連接開啟時，則為唯讀屬性。  
  
 **ConnectionString**屬性中的引數重複專案會被忽略。 使用任何引數的最後一個實例。  
  
> [!NOTE]
>  **遠端資料服務使用量** 使用於用戶端 **連接** 物件時， **ConnectionString** 屬性只能包含 *遠端提供者* 和 *遠端伺服器* 參數。  
  
 下表列出每個 Windows 作業系統的預設 ADO 提供者：  
  
|預設 ADO 提供者|Windows 作業系統|  
|--------------------------|------------------------------|  
|MSDASQL<br /><br />  (若要改善原始程式碼的可讀性，請在連接字串中明確指定提供者名稱。 ) |Windows 2000 (32 位) <br /><br /> Windows XP (32 位元)<br /><br /> Windows 2003 Server (32 位) <br /><br /> Windows Vista (32 位元)<br /><br /> Windows Vista Service Pack 1 或更新版本 (32 位和64位) <br /><br /> Windows Vista (32 位和64位) 之後的 windows 版本|  
|沒有預設值。<br /><br /> 當 ADO 應用程式在下列作業系統上執行且未明確指定提供者時，ADO 會傳回下列錯誤：「ADODB。連接：未指定提供者，而且沒有指定的預設提供者」|Windows 2000 (64 位) <br /><br /> Windows XP (64 位元)<br /><br /> Windows 2003 Server (64 位) <br /><br /> Windows Vista (64 位元)|  
  
## <a name="applies-to"></a>套用至  
 [Connection 物件 (ADO)](./connection-object-ado.md)  
  
## <a name="see-also"></a>另請參閱  
 [ConnectionString、ConnectionTimeout 和 State 屬性範例 (VB) ](./connectionstring-connectiontimeout-and-state-properties-example-vb.md)   
 [ConnectionString、ConnectionTimeout 和 State 屬性範例 (VC + +) ](./connectionstring-connectiontimeout-and-state-properties-example-vc.md)   
 [附錄 A：提供者](../../guide/appendixes/appendix-a-providers.md)