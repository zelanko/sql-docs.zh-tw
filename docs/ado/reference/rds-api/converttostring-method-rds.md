---
description: ConvertToString 方法 (RDS)
title: " (RDS) 的 ConvertToString 方法 |Microsoft Docs"
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
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
ms.openlocfilehash: 6f0d262e3ffeee6b5c5fecf32a12f89a5b5b8c12
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/27/2020
ms.locfileid: "88982619"
---
# <a name="converttostring-method-rds"></a>ConvertToString 方法 (RDS)
將 [記錄集](../ado-api/recordset-object-ado.md) 轉換為代表記錄集資料的 MIME 字串。  
  
> [!IMPORTANT]
>  從 Windows 8 和 Windows Server 2012 開始，Windows 作業系統中不再包含 RDS 伺服器元件 (如需詳細) 資訊，請參閱 Windows 8 和 [Windows server 2012 相容性操作手冊](https://www.microsoft.com/download/details.aspx?id=27416) 。 未來的 Windows 版本將移除 RDS 用戶端元件。 請避免在新的開發工作中使用這項功能，並規劃修改目前使用這項功能的應用程式。 使用 RDS 的應用程式應該遷移至 [WCF 資料服務](https://go.microsoft.com/fwlink/?LinkId=199565)。  
  
## <a name="syntax"></a>語法  
  
```  
  
DataFactory.ConvertToString(Recordset)  
```  
  
#### <a name="parameters"></a>參數  
 *DataFactory*  
 代表 [RDSServer. DataFactory](./datafactory-object-rdsserver.md) 物件的物件變數。  
  
 *Recordset*  
 代表 **記錄集** 物件的物件變數。  
  
## <a name="remarks"></a>備註  
 使用 .asp 檔案時，請使用 **ConvertToString** 在伺服器上產生的 HTML 網頁中內嵌 **記錄集** ，以將其傳輸至用戶端電腦。  
  
 **ConvertToString** 會先將 **記錄集** 載入至資料指標服務資料表，然後以 MIME 格式產生資料流程。  
  
 在用戶端上，遠端資料服務可以將 MIME 字串轉換回功能完整的 **記錄集**。 它很適合用來處理少於400個數據列的資料，而且每個資料列不能超過1024個位元組的寬度。 您不應該將它用於串流 BLOB 資料和透過 HTTP 的大型結果集。 在字串上不會執行任何網路壓縮，因此相較于遠端資料服務所定義和部署的網路優化 tablegram 格式（其原生傳輸通訊協定格式），非常大型的資料集將需要相當長的時間，透過 HTTP 進行傳輸。  
  
> [!NOTE]
>  如果您使用 Active Server Pages 將產生的 MIME 字串內嵌在用戶端 HTML 網頁中，請注意早于2.0 版的 VBScript 版本會將字串的大小限制為32K。 如果超過此限制，則會傳回錯誤。 透過 .asp 檔案使用 MIME 內嵌時，讓查詢範圍保持相對較小。 若要修正此問題，請從 Microsoft Windows 腳本技術網站下載最新版本的 VBScript。  
  
## <a name="applies-to"></a>套用至  
 [DataFactory 物件 (RDSServer)](./datafactory-object-rdsserver.md)  
  
## <a name="see-also"></a>另請參閱  
 [ (VB) 的 ConvertToString 方法範例 ](../ado-api/converttostring-method-example-vb.md)   
 [ConvertToString 方法範例 (VBScript)](./converttostring-method-example-vbscript.md)