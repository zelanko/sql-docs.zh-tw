---
title: 自訂檔案 Connect 區段 |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 11/09/2018
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- connect section in RDS [ADO]
- customization file in RDS [ADO]
ms.assetid: d50eb3cc-a822-486f-b80b-65bb50547ecd
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 1de3710590cf49de30ff8e79a6ff829b124c42dd
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/15/2019
ms.locfileid: "67922800"
---
# <a name="customization-file-connect-section"></a>自訂檔案 Connect 區段
處理常式的預設行為是拒絕所有連線。 **連線**區段會指定該行為的例外狀況。 例如，如果要將所有**連線**區段已不存在或空的則預設無法建立任何連線。  
  
 **連線**區段只能包含：  
  
-   預設存取項目，指定預設的讀取和寫入這個連接上允許的作業。 如果區段中沒有任何預設存取項目，將會忽略一節。  
  
-   新的連接字串，它會取代用戶端連接字串。  
  
> [!IMPORTANT]
>  從 Windows 8 和 Windows Server 2012 開始，RDS 伺服器元件不會再包含在 Windows 作業系統中 (請參閱 Windows 8 和[Windows Server 2012 相容性操作手冊](https://www.microsoft.com/download/details.aspx?id=27416)如需詳細資訊)。 RDS 用戶端元件將會在 Windows 的未來版本中移除。 請避免在新的開發工作中使用這項功能，並規劃修改目前使用這項功能的應用程式。 使用 RDS 的應用程式應該移轉至[WCF 資料服務](https://go.microsoft.com/fwlink/?LinkId=199565)。  
  
## <a name="syntax"></a>語法  
 預設存取項目屬於表單：  
  
```console
  
Access=  
accessRight  
  
```  
  
 取代連接字串項目屬於表單：  
  
```console
  
Connect=  
connectionString  
  
```  
  
## <a name="remarks"></a>備註  
  
|部分|描述|  
|----------|-----------------|  
|**[連接]**|常值字串，表示這是連接字串項目。|  
|**_connectionString_**|字串，取代整個用戶端連接字串。|  
|**存取**|常值字串，表示這是存取項目。|  
|**_accessRight_**|其中一個下列的存取權限：<br /><br /> -   **NoAccess** -使用者無法存取資料來源。<br />-   **ReadOnly** -使用者可以讀取的資料來源。<br />-   **ReadWrite** -使用者可以讀取或寫入至資料來源。|  
  
 如果您想要允許任何連線 （以影響，停用預設處理常式的行為），請在中設定的存取項目**連接預設值** 區段`Access=ReadWrite`，並刪除或取消註解的任何其他**連接**_識別碼_一節。  
  
## <a name="see-also"></a>另請參閱  
 [自訂檔案 Logs 區段](../../../ado/guide/remote-data-service/customization-file-logs-section.md)   
 [自訂檔案 SQL 區段](../../../ado/guide/remote-data-service/customization-file-sql-section.md)   
 [自訂檔案 UserList 區段](../../../ado/guide/remote-data-service/customization-file-userlist-section.md)   
 [DataFactory 自訂](../../../ado/guide/remote-data-service/datafactory-customization.md)   
 [必要的用戶端設定](../../../ado/guide/remote-data-service/required-client-settings.md)   
 [了解自訂檔案](../../../ado/guide/remote-data-service/understanding-the-customization-file.md)   
 [撰寫您自己的自訂處理常式](../../../ado/guide/remote-data-service/writing-your-own-customized-handler.md)



