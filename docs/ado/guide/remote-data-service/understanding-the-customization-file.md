---
description: 了解自訂檔案
title: 瞭解自訂檔案 |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 11/09/2018
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- customization file in RDS [ADO]
ms.assetid: 136f74bf-8d86-4a41-be66-c86cbcf81548
author: rothja
ms.author: jroth
ms.openlocfilehash: 18c7d09707a69967560765f880a3c6563de1506e
ms.sourcegitcommit: c4d564435c008e2c92035efd2658172f20f07b2b
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/24/2020
ms.locfileid: "88759866"
---
# <a name="understanding-the-customization-file"></a>了解自訂檔案
自訂檔案中的每個區段標頭都是由方括弧 (**[]**) 包含型別和參數所組成。 這四個區段類型是由常值字串 **connect**、 **sql**、 **userlist**或 **logs**表示。 參數是常值字串、預設值、使用者指定的識別碼或 nothing。  
  
> [!IMPORTANT]
>  從 Windows 8 和 Windows Server 2012 開始，Windows 作業系統中不再包含 RDS 伺服器元件 (如需詳細) 資訊，請參閱 Windows 8 和 [Windows server 2012 相容性操作手冊](https://www.microsoft.com/download/details.aspx?id=27416) 。 未來的 Windows 版本將移除 RDS 用戶端元件。 請避免在新的開發工作中使用這項功能，並規劃修改目前使用這項功能的應用程式。 使用 RDS 的應用程式應該遷移至 [WCF 資料服務](https://go.microsoft.com/fwlink/?LinkId=199565)。  
  
 因此，每個區段都會以下列其中一個區段標頭標示：  
  
```console
  
[ connect default ] [ connect    
identifier   
] [ sql  default ] [ sql    
identifier   
] [ userlist    
identifier   
] [ logs ]  
  
```  
  
 區段標頭具有下列部分。  
  
|部分|描述|  
|----------|-----------------|  
|**connect**|修改連接字串的常值字串。|  
|**sql**|修改命令字串的常值字串。|  
|**userlist**|常值字串，可修改特定使用者的存取權限。|  
|**日誌**|常值字串，指定記錄操作錯誤的記錄檔。|  
|**預設值**|如果未指定或找不到任何識別碼，則會使用常值字串。|  
|*識別碼*|符合 **連接** 或 **命令** 字串中字串的字串。<br /><br /> -如果區段標頭包含 **connect** ，而且在連接字串中找到識別碼字串，請使用此區段。<br />-如果區段標頭包含 **sql** ，且在命令字串中找到識別碼字串，請使用此區段。<br />-如果區段標頭包含 **userlist** ，且識別碼字串符合 **connect** 區段識別碼，請使用此區段。|  
  
 **DataFactory**會呼叫處理常式，並傳遞用戶端參數。 此處理程式會在用戶端參數中搜尋符合適當區段標頭中識別碼的整個字串。 如果找到相符的，則會將該區段的內容套用至用戶端參數。  
  
 在下列情況下，會使用特定區段：  
  
-   如果用戶端連接字串關鍵字 "**Data Source =**_value_" 的值部分符合**connect**區段識別碼，就會使用**connect**區段。 
  
-   如果用戶端命令字串包含符合**sql**區段識別碼的字串，則會使用**sql**區段。  
  
-   如果沒有相符的識別碼，則會使用具有預設參數的 **connect** 或 **sql** 區段。  
  
-   如果**userlist**區段識別碼符合**connect**區段識別碼，就會使用**userlist**區段。 如果有相符的內容， **userlist** 區段的內容會套用至 **connect** 區段所控管的連接。  
  
-   如果連接或命令字串中的字串不符合任何 **connect** 或 **sql** 區段標頭中的識別碼，而且沒有具有預設參數的 **connect** 或 **sql** 區段標頭，則會使用用戶端字串而不進行修改。  
  
-   每當**DataFactory**正在運作時，就會使用**logs**區段。  
  
## <a name="see-also"></a>另請參閱  
 [自訂檔案連接區段](./customization-file-connect-section.md)   
 [自訂檔案記錄區段](./customization-file-logs-section.md)   
 [自訂檔案 SQL 區段](./customization-file-sql-section.md)   
 [自訂檔案 UserList 區段](./customization-file-userlist-section.md)   
 [DataFactory 自訂](./datafactory-customization.md)   
 [必要的用戶端設定](./required-client-settings.md)   
 [撰寫您自己的自訂處理常式](./writing-your-own-customized-handler.md)