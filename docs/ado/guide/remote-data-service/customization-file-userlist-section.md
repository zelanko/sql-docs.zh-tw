---
title: 自訂檔案 UserList 區段 |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 11/09/2018
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- UserList section in rds [ADO]
- customization file in RDS [ADO]
ms.assetid: 42e8ec20-eaac-4a95-8cb8-4bba93a75bcb
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: e38b253cdebcc5ab976de8c8eb355f7f6fb03aec
ms.sourcegitcommit: 074d44994b6e84fe4552ad4843d2ce0882b92871
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/05/2019
ms.locfileid: "66699538"
---
# <a name="customization-file-userlist-section"></a>自訂檔案 UserList 區段
**Userlist**一節有關**連線**相同的區段與區段*識別碼*參數。  
  
 此區段可以包含 *使用者存取項目* ，以指定的存取權限指定的使用者，且會覆寫 *預設* *存取項目* 中比對 **連線** 一節。  
  
> [!IMPORTANT]
>  從 Windows 8 和 Windows Server 2012 開始，RDS 伺服器元件不會再包含在 Windows 作業系統中 (請參閱 Windows 8 和[Windows Server 2012 相容性操作手冊](https://www.microsoft.com/download/details.aspx?id=27416)如需詳細資訊)。 RDS 用戶端元件將會在 Windows 的未來版本中移除。 請避免在新的開發工作中使用這項功能，並規劃修改目前使用這項功能的應用程式。 使用 RDS 的應用程式應該移轉至[WCF 資料服務](https://go.microsoft.com/fwlink/?LinkId=199565)。  
  
## <a name="syntax"></a>語法  
 使用者存取項目屬於表單：  
  
 _userName_ **=**    
 **_accessRights_**  
  
|部分|描述|  
|----------|-----------------|  
|*userName*|*使用者名*採用此連線的人員。 有效的使用者名稱建立與 IIS **Service Manager**對話方塊。|  
|**_accessRights_**|其中一個下列的存取權限：<br /><br /> -   **NoAccess** -使用者無法存取資料來源。<br />-   **ReadOnly** -使用者可以讀取的資料來源。<br />-   **ReadWrite** -使用者可以讀取或寫入至資料來源。|  
  
## <a name="see-also"></a>另請參閱  
 [自訂檔案 Connect 區段](../../../ado/guide/remote-data-service/customization-file-connect-section.md)   
 [自訂檔案 Logs 區段](../../../ado/guide/remote-data-service/customization-file-logs-section.md)   
 [自訂檔案 SQL 區段](../../../ado/guide/remote-data-service/customization-file-sql-section.md)   
 [DataFactory 自訂](../../../ado/guide/remote-data-service/datafactory-customization.md)   
 [必要的用戶端設定](../../../ado/guide/remote-data-service/required-client-settings.md)   
 [了解自訂檔案](../../../ado/guide/remote-data-service/understanding-the-customization-file.md)   
 [撰寫您自己的自訂處理常式](../../../ado/guide/remote-data-service/writing-your-own-customized-handler.md)


