---
title: 了解自訂檔案 |Microsoft Docs
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
manager: jroth
ms.openlocfilehash: d58edcfae92c94cfc635d3539f81faf834e382c7
ms.sourcegitcommit: d9c5b9ab3c282775ed61712892eeb3e150ccc808
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/05/2019
ms.locfileid: "67597574"
---
# <a name="understanding-the-customization-file"></a>了解自訂檔案
在自訂檔案中的每個區段標頭包含方括號 ( **[]** ) 包含型別和參數。 四個區段類型會以常值字串**連接**， **sql**， **userlist**，或**記錄**。 參數是常值字串、 預設值、 使用者指定的識別項，或執行任何動作。  
  
> [!IMPORTANT]
>  從 Windows 8 和 Windows Server 2012 開始，RDS 伺服器元件不會再包含在 Windows 作業系統中 (請參閱 Windows 8 和[Windows Server 2012 相容性操作手冊](https://www.microsoft.com/download/details.aspx?id=27416)如需詳細資訊)。 RDS 用戶端元件將會在 Windows 的未來版本中移除。 請避免在新的開發工作中使用這項功能，並規劃修改目前使用這項功能的應用程式。 使用 RDS 的應用程式應該移轉至[WCF 資料服務](https://go.microsoft.com/fwlink/?LinkId=199565)。  
  
 因此，每個區段已標記使用其中一個下列的區段標頭：  
  
```console
  
[ connect default ] [ connect    
identifier   
] [ sql  default ] [ sql    
identifier   
] [ userlist    
identifier   
] [ logs ]  
  
```  
  
 區段標頭有下列的部分。  
  
|部分|描述|  
|----------|-----------------|  
|**connect**|修改連接字串常值字串。|  
|**sql**|可修改命令字串常值的字串。|  
|**userlist**|常值的字串，以修改特定使用者的存取權限。|  
|**logs**|常值的字串，指定記錄作業的錯誤記錄檔。|  
|**default**|如果指定或找到沒有識別項會使用常值字串。|  
|*identifier*|符合的字串的字串**連接**或是**命令**字串。<br /><br /> -使用本節中，如果區段標頭包含**連線**和連接字串中找到的識別項字串。<br />-使用本節中，如果區段標頭包含**sql**和命令字串中找到的識別項字串。<br />-使用本節中，如果區段標頭包含**userlist**和 [識別碼] 字串比對**連線**區段識別項。|  
  
 **DataFactory**呼叫的處理常式中，然後再將用戶端參數傳遞。 處理常式會搜尋比對識別碼在適當的區段標頭中的用戶端參數中的整個字串。 如果找到相符項目，則該區段的內容會套用至用戶端參數。  
  
 在下列情況下，使用特定的區段：  
  
-   A**連接**如果用戶端的值部分連接字串關鍵字，就會使用區段 」**資料來源 =** _值_"，符合**連接**區段識別碼。 
  
-   **Sql**如果用戶端命令字串包含符合的字串，就會使用 區段**sql**區段識別項。  
  
-   A**連接**或是**sql**如果沒有任何相符的識別項，會使用有預設參數區段。  
  
-   A **userlist**一節會使用**userlist**區段識別項相符項目**連接**區段識別項。 如果沒有相符項目的內容**userlist**一節會套用至所控管連接**連線**一節。  
  
-   如果連接或命令字串中的字串不符合任何識別項**連接**或**sql**區段標頭，而且沒有任何**連接**或**sql**區段標頭，使用預設參數，則用戶端會使用字串而不需修改。  
  
-   **記錄檔**區段用每當**DataFactory**正在運作中。  
  
## <a name="see-also"></a>另請參閱  
 [自訂檔案 Connect 區段](../../../ado/guide/remote-data-service/customization-file-connect-section.md)   
 [自訂檔案 Logs 區段](../../../ado/guide/remote-data-service/customization-file-logs-section.md)   
 [自訂檔案 SQL 區段](../../../ado/guide/remote-data-service/customization-file-sql-section.md)   
 [自訂檔案 UserList 區段](../../../ado/guide/remote-data-service/customization-file-userlist-section.md)   
 [DataFactory 自訂](../../../ado/guide/remote-data-service/datafactory-customization.md)   
 [必要的用戶端設定](../../../ado/guide/remote-data-service/required-client-settings.md)   
 [撰寫您自己的自訂處理常式](../../../ado/guide/remote-data-service/writing-your-own-customized-handler.md)

