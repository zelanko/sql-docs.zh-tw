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
ms.openlocfilehash: 558fd9c8379808e6c2f109a9c9584e8831cddd0f
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "67922768"
---
# <a name="customization-file-userlist-section"></a>自訂檔案 UserList 區段
**Userlist**區段適用于具有相同區段*識別碼*參數的**connect**區段。  
  
 此區段可以包含*使用者存取專案*，以指定指定使用者的存取權限，並覆寫 [比對**連接]** 區段中的*預設**存取專案*。  
  
> [!IMPORTANT]
>  從 Windows 8 和 Windows Server 2012 開始，Windows 作業系統不再包含 RDS 伺服器元件（如需詳細資訊，請參閱 Windows 8 和[Windows Server 2012 相容性操作手冊](https://www.microsoft.com/download/details.aspx?id=27416)）。 RDS 用戶端元件將會在未來的 Windows 版本中移除。 請避免在新的開發工作中使用這項功能，並規劃修改目前使用這項功能的應用程式。 使用 RDS 的應用程式應該遷移至[WCF 資料服務](https://go.microsoft.com/fwlink/?LinkId=199565)。  
  
## <a name="syntax"></a>語法  
 使用者存取專案的格式如下：  
  
 使用者_名稱_**=**   
 **_accessRights_**  
  
|部分|描述|  
|----------|-----------------|  
|*userName*|採用此連接之人員的*使用者名稱*。 系統會使用 [IIS **Service Manager** ] 對話方塊來建立有效的使用者名稱。|  
|**_accessRights_**|下列其中一個存取權限：<br /><br /> -   **NoAccess** -使用者無法存取資料來源。<br />-   **ReadOnly** -使用者可以讀取資料來源。<br />-   **ReadWrite** -使用者可以讀取或寫入資料來源。|  
  
## <a name="see-also"></a>另請參閱  
 [自訂檔案連接區段](../../../ado/guide/remote-data-service/customization-file-connect-section.md)   
 [自訂檔案記錄區段](../../../ado/guide/remote-data-service/customization-file-logs-section.md)   
 [自訂檔案 SQL 區段](../../../ado/guide/remote-data-service/customization-file-sql-section.md)   
 [DataFactory 自訂](../../../ado/guide/remote-data-service/datafactory-customization.md)   
 [必要的用戶端設定](../../../ado/guide/remote-data-service/required-client-settings.md)   
 [瞭解自訂檔案](../../../ado/guide/remote-data-service/understanding-the-customization-file.md)   
 [撰寫您自己的自訂處理常式](../../../ado/guide/remote-data-service/writing-your-own-customized-handler.md)


