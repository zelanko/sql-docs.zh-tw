---
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 81a73044c1ab413fb2b49286814f3e6b3951c6c9
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "67921963"
---
# <a name="understanding-the-customization-file"></a>了解自訂檔案
自訂檔案中的每個區段標頭都是由包含型別和參數的方括弧（**[]**）所組成。 四個區段類型會以常值字串**connect**、 **sql**、 **userlist**或**logs**來表示。 參數是文字字串、預設值、使用者指定的識別碼，或不是任何內容。  
  
> [!IMPORTANT]
>  從 Windows 8 和 Windows Server 2012 開始，Windows 作業系統不再包含 RDS 伺服器元件（如需詳細資訊，請參閱 Windows 8 和[Windows Server 2012 相容性操作手冊](https://www.microsoft.com/download/details.aspx?id=27416)）。 RDS 用戶端元件將會在未來的 Windows 版本中移除。 請避免在新的開發工作中使用這項功能，並規劃修改目前使用這項功能的應用程式。 使用 RDS 的應用程式應該遷移至[WCF 資料服務](https://go.microsoft.com/fwlink/?LinkId=199565)。  
  
 因此，每個區段都會標記下列其中一個區段標頭：  
  
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
|**server**|修改命令字串的常值字串。|  
|**userlist**|修改特定使用者存取權限的常值字串。|  
|**退出**|指定記錄檔記錄操作錯誤的常值字串。|  
|**預設**|如果未指定或找不到識別碼，則會使用常值字串。|  
|*標識*|字串，符合**connect**或**命令**字串中的字串。<br /><br /> -如果區段標頭包含**connect** ，而且在連接字串中找到識別碼字串，請使用此區段。<br />-如果區段標頭包含**sql** ，而且在命令字串中找到識別碼字串，請使用此區段。<br />-如果區段標頭包含**userlist** ，而且識別碼字串符合**connect**區段識別碼，請使用此區段。|  
  
 **DataFactory**會呼叫處理常式，並傳遞用戶端參數。 處理常式會在用戶端參數中搜尋與適當區段標頭中的識別碼相符的整個字串。 如果找到相符的，該區段的內容就會套用至用戶端參數。  
  
 在下列情況下，會使用特定的區段：  
  
-   如果用戶端連接字串關鍵字「**資料來源 =**_值_」的值部分符合**connect**區段識別碼，則會使用**connect**區段。 
  
-   如果用戶端命令字串包含符合**sql**區段識別碼的字串，則會使用**sql**區段。  
  
-   如果沒有相符的識別碼，則會使用含有 default 參數的**connect**或**sql**區段。  
  
-   如果**userlist**區段識別碼符合**connect**區段識別碼，則會使用**userlist**區段。 如果有相符的結果， **userlist**區段的內容就會套用至 [**連接]** 區段所控制的連接。  
  
-   如果連接或命令字串中的字串不符合任何**connect**或**sql**區段標頭中的識別碼，而且沒有具有預設參數的**connect**或**sql**區段標頭，則會在不修改的情況下使用用戶端字串。  
  
-   每當**DataFactory**進行時，就會使用**logs**區段。  
  
## <a name="see-also"></a>另請參閱  
 [自訂檔案連接區段](../../../ado/guide/remote-data-service/customization-file-connect-section.md)   
 [自訂檔案記錄區段](../../../ado/guide/remote-data-service/customization-file-logs-section.md)   
 [自訂檔案 SQL 區段](../../../ado/guide/remote-data-service/customization-file-sql-section.md)   
 [自訂檔案 UserList 區段](../../../ado/guide/remote-data-service/customization-file-userlist-section.md)   
 [DataFactory 自訂](../../../ado/guide/remote-data-service/datafactory-customization.md)   
 [必要的用戶端設定](../../../ado/guide/remote-data-service/required-client-settings.md)   
 [撰寫您自己的自訂處理常式](../../../ado/guide/remote-data-service/writing-your-own-customized-handler.md)

