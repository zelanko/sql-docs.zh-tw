---
description: Open 方法 (ADO Connection)
title: " (ADO Connection) 的 Open 方法 |Microsoft Docs"
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
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
author: rothja
ms.author: jroth
ms.openlocfilehash: c3691f6b7b86d7f48ea570a542f85af75c53d017
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/27/2020
ms.locfileid: "88990329"
---
# <a name="open-method-ado-connection"></a>Open 方法 (ADO Connection)
開啟與資料來源的連接。  
  
## <a name="syntax"></a>語法  
  
```  
  
connection.Open ConnectionString, UserID, Password, Options  
```  
  
#### <a name="parameters"></a>參數  
 *ConnectionString*  
 選擇性。 包含連接資訊的 **字串** 值。 如需有效設定的詳細資訊，請參閱 [ConnectionString](./connectionstring-property-ado.md) 屬性。  
  
 *UserID*  
 選擇性。 包含建立連接時所要使用之使用者名稱的 **字串** 值。  
  
 *密碼*  
 選擇性。 **字串**值，包含建立連接時所要使用的密碼。  
  
 *選項*  
 選擇性。 [ConnectOptionEnum](./connectoptionenum.md)值，這個值會判斷此方法是否應該在 (同步) 之後，或在建立連接 (非同步) 之前傳回。  
  
## <a name="remarks"></a>備註  
 在[連接](./connection-object-ado.md)物件上使用**Open**方法，可建立與資料來源的實體連接。 在這個方法成功完成之後，連接就會上線，您可以對其發出命令並處理結果。  
  
 使用選擇性 *ConnectionString* 引數來指定連接字串，其中包含一系列以分號分隔的 *argument* *= VALUE* 語句，或是以 URL 識別的檔案或目錄資源。 **Connectionstring**屬性會自動繼承用於*ConnectionString*引數的值。 因此，您可以在開啟**連接**物件之前先設定它的**connectionstring**屬性，或在**Open**方法呼叫期間使用*ConnectionString*引數來設定或覆寫目前的連接參數。  
  
 如果您在 *connectionstring* 引數和選擇性 *UserID* 和 *password* 引數中傳遞使用者和密碼資訊， *UserID* 和 *password* 引數將會覆寫 *connectionstring*中指定的值。  
  
 當您已 **完成開啟連線的作業**時，請使用 [Close](./close-method-ado.md) 方法釋放任何相關聯的系統資源。 關閉物件並不會將它從記憶體中移除;您可以變更其屬性設定，並使用 **open** 方法，稍後再重新開啟。 若要完全消除記憶體中的物件，請將物件變數設定為 *Nothing*。  
  
> [!NOTE]
>  **遠端資料服務使用量**使用於用戶端**連接**物件時， **Open**方法實際上並不會建立與伺服器的連接，除非在**連接**物件上開啟[記錄集](./recordset-object-ado.md)。  
  
> [!NOTE]
>  使用 HTTP 配置的 Url 會自動叫用 [Microsoft OLE DB 提供者進行網際網路發佈](../../guide/appendixes/microsoft-ole-db-provider-for-internet-publishing.md)。 如需詳細資訊，請參閱 [絕對和相對 url](../../guide/data/absolute-and-relative-urls.md)。  
  
## <a name="applies-to"></a>套用至  
 [Connection 物件 (ADO)](./connection-object-ado.md)  
  
## <a name="see-also"></a>另請參閱  
 [ (VB 的 Open 和 Close 方法範例) ](./open-and-close-methods-example-vb.md)   
 [ (VBScript) 的開啟和關閉方法範例 ](./open-and-close-methods-example-vbscript.md)   
 [Open 和 Close 方法範例 (VC + +) ](./open-and-close-methods-example-vc.md)   
 [ (ADO 記錄) 的 Open 方法 ](./open-method-ado-record.md)   
 [ (ADO 記錄集的 Open 方法) ](./open-method-ado-recordset.md)   
 [ (ADO Stream 的 Open 方法) ](./open-method-ado-stream.md)   
 [OpenSchema 方法](./openschema-method.md)