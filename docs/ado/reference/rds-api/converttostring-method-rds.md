---
title: ConvertToString 方法 (RDS) |Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 426fd1fdcd3931981037b346b048de816e8596d0
ms.sourcegitcommit: 63b4f62c13ccdc2c097570fe8ed07263b4dc4df0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/13/2018
ms.locfileid: "51600288"
---
# <a name="converttostring-method-rds"></a>ConvertToString 方法 (RDS)
將轉換[資料錄集](../../../ado/reference/ado-api/recordset-object-ado.md)MIME 字串，表示資料錄集資料。  
  
> [!IMPORTANT]
>  從 Windows 8 和 Windows Server 2012 開始，RDS 伺服器元件不會再包含在 Windows 作業系統中 (請參閱 Windows 8 和[Windows Server 2012 相容性操作手冊](https://www.microsoft.com/download/details.aspx?id=27416)如需詳細資訊)。 RDS 用戶端元件將會在 Windows 的未來版本中移除。 請避免在新的開發工作中使用這項功能，並規劃修改目前使用這項功能的應用程式。 使用 RDS 的應用程式應該移轉至[WCF 資料服務](https://go.microsoft.com/fwlink/?LinkId=199565)。  
  
## <a name="syntax"></a>語法  
  
```  
  
DataFactory.ConvertToString(Recordset)  
```  
  
#### <a name="parameters"></a>參數  
 *DataFactory*  
 物件變數，表示[RDSServer.DataFactory](../../../ado/reference/rds-api/datafactory-object-rdsserver.md)物件。  
  
 *Recordset*  
 物件變數，表示**資料錄集**物件。  
  
## <a name="remarks"></a>備註  
 .Asp 檔案時，使用**ConvertToString**內嵌**資料錄集**產生伺服器傳輸至用戶端電腦上的 HTML 網頁中。  
  
 **ConvertToString**第一次載入**資料錄集**指標服務至資料表，並接著 MIME 格式產生資料流。  
  
 在用戶端，遠端資料服務可以 MIME 將字串轉換回正常運作**資料錄集**。 它非常適合處理少於 400 以不超過 1024 個位元組寬，每個資料列的資料列。 您不應該將它用於資料流處理 BLOB 資料，並透過 HTTP 將大型結果集。 沒有連線壓縮會對字串中，因此非常大型資料集需要相當長的時間來傳輸 over HTTP 相較於定義和做為其原生傳輸通訊協定格式的遠端資料服務所部署的網路最佳化 tablegram 格式。  
  
> [!NOTE]
>  如果您使用 Active Server Pages 將產生的 MIME 字串內嵌在用戶端 HTML 頁面中，請注意，2.0 版之前的 VBScript 版本字串的大小限制為 32 K。 如果超過此限制，則會傳回錯誤。 使用 MIME 內嵌透過.asp 檔案時，請查詢範圍相對較小。 若要修正此問題，請從 Microsoft Windows 指令碼技術網站下載最新版的 VBScript。  
  
## <a name="applies-to"></a>適用於  
 [DataFactory 物件 (RDSServer)](../../../ado/reference/rds-api/datafactory-object-rdsserver.md)  
  
## <a name="see-also"></a>另請參閱  
 [ConvertToString 方法範例 (VB)](../../../ado/reference/ado-api/converttostring-method-example-vb.md)   
 [ConvertToString 方法範例 (VBScript)](../../../ado/reference/rds-api/converttostring-method-example-vbscript.md)


