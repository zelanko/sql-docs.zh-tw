---
title: "ConvertToString 方法 (RDS) |Microsoft 文件"
ms.prod: sql-non-specified
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
apitype: COM
helpviewer_keywords:
- ConvertToString method [ADO]
ms.assetid: b3f36bc8-6f69-49b0-83cd-2ccd3afebfbe
caps.latest.revision: 16
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: b910522edc20c73164d03fd5f7f313c1eaffabd7
ms.contentlocale: zh-tw
ms.lasthandoff: 09/09/2017

---
# <a name="converttostring-method-rds"></a>ConvertToString 方法 (RDS)
將轉換[資料錄集](../../../ado/reference/ado-api/recordset-object-ado.md)MIME 字串，代表資料錄集資料。  
  
> [!IMPORTANT]
>  從 Windows 8 和 Windows Server 2012 開始，RDS 伺服器元件已不再包含在 Windows 作業系統中 (請參閱 < Windows 8 和[Windows Server 2012 相容性手冊](https://www.microsoft.com/en-us/download/details.aspx?id=27416)如需詳細資訊)。 Windows 的未來版本將移除 RDS 用戶端元件。 請避免在新的開發工作中使用這項功能，並規劃修改目前使用這項功能的應用程式。 使用 RDS 的應用程式應該移轉到[WCF 資料服務](http://go.microsoft.com/fwlink/?LinkId=199565)。  
  
## <a name="syntax"></a>語法  
  
```  
  
DataFactory.ConvertToString(Recordset)  
```  
  
#### <a name="parameters"></a>參數  
 *DataFactory*  
 物件變數，表示[RDSServer.DataFactory](../../../ado/reference/rds-api/datafactory-object-rdsserver.md)物件。  
  
 *資料錄集*  
 物件變數，表示**資料錄集**物件。  
  
## <a name="remarks"></a>備註  
 .Asp 檔案時，使用**ConvertToString**內嵌**資料錄集**傳輸至用戶端電腦在伺服器上產生的 HTML 網頁中。  
  
 **ConvertToString**第一次載入**資料錄集**指標服務至資料表，並會以 MIME 格式產生資料流。  
  
 在用戶端，遠端資料服務可以 MIME 將字串轉換成正常運作**資料錄集**。 它非常適合處理不超過 1024 個位元組寬度，每個資料列的資料超過 400 的資料列。 您不應該將它用於資料流 BLOB 資料，並透過 HTTP 的大型結果集。 沒有連線壓縮不會對字串中，因此非常大型資料集需要相當長的時間來傳輸 over HTTP 相較於定義及部署為其原生傳輸通訊協定格式的遠端資料服務的網路最佳化 tablegram 格式。  
  
> [!NOTE]
>  如果您用來在用戶端 HTML 網頁中內嵌產生的 MIME 字串 Active Server Pages，請注意，2.0 版之前的 VBScript 版本字串的大小限制為 32k。 如果超過此限制時，會傳回錯誤。 使用 MIME 內嵌透過.asp 檔案時，請查詢範圍相對較小。 若要修正此問題，請從 Microsoft Windows 指令碼技術網站下載 VBScript 的最新版本。  
  
## <a name="applies-to"></a>適用於  
 [DataFactory 物件 (RDSServer)](../../../ado/reference/rds-api/datafactory-object-rdsserver.md)  
  
## <a name="see-also"></a>另請參閱  
 [ConvertToString 方法範例 (VB)](../../../ado/reference/ado-api/converttostring-method-example-vb.md)   
 [ConvertToString 方法範例 (VBScript)](../../../ado/reference/rds-api/converttostring-method-example-vbscript.md)



