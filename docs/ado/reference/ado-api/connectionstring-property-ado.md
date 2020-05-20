---
title: ConnectionString 屬性（ADO） |Microsoft Docs
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
author: rothja
ms.author: jroth
ms.openlocfilehash: 39eb67a98d710e27c051d77aa7843663c853b9e0
ms.sourcegitcommit: 6037fb1f1a5ddd933017029eda5f5c281939100c
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/04/2020
ms.locfileid: "82762629"
---
# <a name="connectionstring-property-ado"></a>ConnectionString 屬性 (ADO)
指出用來建立資料來源連接的資訊。  
  
## <a name="settings-and-return-values"></a>設定和傳回值  
 設定或傳回**字串**值。  
  
## <a name="remarks"></a>備註  
 藉由傳遞詳細的連接字串（包含以分號分隔的一系列*引數* *= 值*語句），即可使用**ConnectionString**屬性來指定資料來源。  
  
 ADO 支援**ConnectionString**屬性的五個引數;任何其他引數會直接傳遞給提供者，而不需要 ADO 處理。 ADO 支援的引數如下所示。  
  
|引數|描述|  
|--------------|-----------------|  
|*提供者 =*|指定要用於連接的提供者名稱。|  
|*檔案名 =*|指定包含預設連接資訊的提供者特定檔案（例如保存的資料來源物件）的名稱。|  
|*遠端提供者 =*|指定開啟用戶端連接時所要使用的提供者名稱。 （僅限遠端資料服務）。|  
|*遠端伺服器 =*|指定要在開啟用戶端連接時使用的伺服器路徑名稱。 （僅限遠端資料服務）。|  
|*URL =*|將連接字串指定為識別資源（例如檔案或目錄）的絕對 URL。|  
  
 設定**ConnectionString**屬性並開啟[連接](../../../ado/reference/ado-api/connection-object-ado.md)物件之後，提供者可能會改變屬性的內容，例如，藉由將 ADO 定義的引數名稱對應至特定提供者的對等專案。  
  
 **Connectionstring**屬性會自動繼承[Open](../../../ado/reference/ado-api/open-method-ado-connection.md)方法的*connectionstring*引數所使用的值，因此您可以在**open**方法呼叫期間覆寫目前的**ConnectionString**屬性。  
  
 因為*檔案名*引數會導致 ADO 載入相關聯的提供者，所以您無法同時傳遞*提供者*和*檔案名*引數。  
  
 當連接關閉時， **ConnectionString**屬性會是讀取/寫入，而在開啟時則為唯讀。  
  
 **ConnectionString**屬性中引數的重複專案會被忽略。 會使用任何引數的最後一個實例。  
  
> [!NOTE]
>  **遠端資料服務使用量**在用戶端**連接**物件上使用時， **ConnectionString**屬性只能包含*遠端提供者*和*遠端伺服器*參數。  
  
 下表列出每個 Windows 作業系統的預設 ADO 提供者：  
  
|預設 ADO 提供者|Windows 作業系統|  
|--------------------------|------------------------------|  
|MSDASQL<br /><br /> （若要改善原始程式碼的可讀性，請在連接字串中明確指定提供者名稱）。|Windows 2000 （32位）<br /><br /> Windows XP (32 位元)<br /><br /> Windows 2003 Server （32位）<br /><br /> Windows Vista (32 位元)<br /><br /> Windows Vista Service Pack 1 或更新版本（32位和64位）<br /><br /> Windows Vista 之後的 windows 版本（32位和64位）|  
|沒有預設值。<br /><br /> 當 ADO 應用程式在下列作業系統上執行，而且未明確指定提供者時，ADO 會傳回下列錯誤：「ADODB。連接：未指定提供者，而且沒有指定的預設提供者」|Windows 2000 （64位）<br /><br /> Windows XP (64 位元)<br /><br /> Windows 2003 Server （64位）<br /><br /> Windows Vista (64 位元)|  
  
## <a name="applies-to"></a>套用至  
 [Connection 物件 (ADO)](../../../ado/reference/ado-api/connection-object-ado.md)  
  
## <a name="see-also"></a>另請參閱  
 [ConnectionString、ConnectionTimeout 和 State 屬性範例（VB）](../../../ado/reference/ado-api/connectionstring-connectiontimeout-and-state-properties-example-vb.md)   
 [ConnectionString、ConnectionTimeout 和 State 屬性範例（VC + +）](../../../ado/reference/ado-api/connectionstring-connectiontimeout-and-state-properties-example-vc.md)   
 [附錄 A：提供者](../../../ado/guide/appendixes/appendix-a-providers.md)
