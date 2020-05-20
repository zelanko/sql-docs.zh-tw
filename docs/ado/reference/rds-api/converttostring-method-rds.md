---
title: ConvertToString 方法（RDS） |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
helpviewer_keywords:
- ConvertToString method [ADO]
ms.assetid: b3f36bc8-6f69-49b0-83cd-2ccd3afebfbe
author: rothja
ms.author: jroth
ms.openlocfilehash: 6eff6ae54dc5cc0b901cfb1da61244e30d963615
ms.sourcegitcommit: 6037fb1f1a5ddd933017029eda5f5c281939100c
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/04/2020
ms.locfileid: "82764839"
---
# <a name="converttostring-method-rds"></a>ConvertToString 方法 (RDS)
將[記錄集](../../../ado/reference/ado-api/recordset-object-ado.md)轉換成代表記錄集資料的 MIME 字串。  
  
> [!IMPORTANT]
>  從 Windows 8 和 Windows Server 2012 開始，Windows 作業系統不再包含 RDS 伺服器元件（如需詳細資訊，請參閱 Windows 8 和[Windows Server 2012 相容性操作手冊](https://www.microsoft.com/download/details.aspx?id=27416)）。 RDS 用戶端元件將會在未來的 Windows 版本中移除。 請避免在新的開發工作中使用這項功能，並規劃修改目前使用這項功能的應用程式。 使用 RDS 的應用程式應該遷移至[WCF 資料服務](https://go.microsoft.com/fwlink/?LinkId=199565)。  
  
## <a name="syntax"></a>語法  
  
```  
  
DataFactory.ConvertToString(Recordset)  
```  
  
#### <a name="parameters"></a>參數  
 *DataFactory*  
 代表[RDSServer DataFactory](../../../ado/reference/rds-api/datafactory-object-rdsserver.md)物件的物件變數。  
  
 *Recordset*  
 代表**記錄集**物件的物件變數。  
  
## <a name="remarks"></a>備註  
 若使用 .asp 檔案，請使用**ConvertToString**將**記錄集**內嵌在伺服器上產生的 HTML 頁面中，以將其傳輸至用戶端電腦。  
  
 **ConvertToString**會先將**記錄集**載入至資料指標服務資料表，然後產生 MIME 格式的資料流程。  
  
 在用戶端上，遠端資料服務可以將 MIME 字串轉換回完整運作的**記錄集**。 這適用于處理少於400個數據列，且每個資料列不超過1024個位元組。 您不應該使用它來串流處理 BLOB 資料和透過 HTTP 的大型結果集。 不會在字串上執行任何網路壓縮，因此，相較于遠端資料服務所定義及部署的雙向傳輸通訊協定格式，非常大型的資料集會花相當長的時間透過 HTTP 傳輸。  
  
> [!NOTE]
>  如果您使用 Active Server Pages 將產生的 MIME 字串內嵌在用戶端 HTML 頁面中，請注意2.0 版之前的 VBScript 版本會將字串的大小限制為32K。 如果超過此限制，則會傳回錯誤。 使用透過 .asp 檔案的 MIME 內嵌時，讓查詢範圍保持相對較小。 若要修正此問題，請從 Microsoft Windows Script 技術網站下載最新版本的 VBScript。  
  
## <a name="applies-to"></a>套用至  
 [DataFactory 物件 (RDSServer)](../../../ado/reference/rds-api/datafactory-object-rdsserver.md)  
  
## <a name="see-also"></a>另請參閱  
 [ConvertToString 方法範例（VB）](../../../ado/reference/ado-api/converttostring-method-example-vb.md)   
 [ConvertToString 方法範例 (VBScript)](../../../ado/reference/rds-api/converttostring-method-example-vbscript.md)


