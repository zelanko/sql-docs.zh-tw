---
title: 自訂檔案 UserList 區段 |Microsoft 文件
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- UserList section in rds [ADO]
- customization file in RDS [ADO]
ms.assetid: 42e8ec20-eaac-4a95-8cb8-4bba93a75bcb
caps.latest.revision: 13
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: dcf8649af2695fa354659f13e891521eb14f39cb
ms.sourcegitcommit: 62826c291db93c9017ae219f75c3cfeb8140bf06
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/11/2018
ms.locfileid: "35273827"
---
# <a name="customization-file-userlist-section"></a>自訂檔案 UserList > 一節
**Userlist**區段屬於**連接**區段中具有相同的區段*識別碼*參數。  
  
 這個區段包含*使用者存取項目*，其中指定存取指定的使用者權限，並覆寫*預設**存取項目*中比對**連接**> 一節。  
  
> [!IMPORTANT]
>  從 Windows 8 和 Windows Server 2012 開始，RDS 伺服器元件已不再包含在 Windows 作業系統中 (請參閱 < Windows 8 和[Windows Server 2012 相容性手冊](https://www.microsoft.com/en-us/download/details.aspx?id=27416)如需詳細資訊)。 Windows 的未來版本將移除 RDS 用戶端元件。 請避免在新的開發工作中使用這項功能，並規劃修改目前使用這項功能的應用程式。 使用 RDS 的應用程式應該移轉到[WCF 資料服務](http://go.microsoft.com/fwlink/?LinkId=199565)。  
  
## <a name="syntax"></a>語法  
 格式是使用者存取項目：  
  
 *userName* **=**   
 ***accessRights***  
  
|部分|描述|  
|----------|-----------------|  
|*userName*|*使用者名*採用此連接的人員。 有效的使用者名稱使用 IIS 建立**Service Manager**對話方塊。|  
|***accessRights***|其中一個的下列存取權限：<br /><br /> -   **NoAccess** -使用者無法存取資料來源。<br />-   **ReadOnly** — 使用者可以讀取的資料來源。<br />-   **ReadWrite** — 使用者可讀取或寫入至資料來源。|  
  
## <a name="see-also"></a>另請參閱  
 [自訂檔案連接 > 一節](../../../ado/guide/remote-data-service/customization-file-connect-section.md)   
 [自訂檔案記錄檔 > 一節](../../../ado/guide/remote-data-service/customization-file-logs-section.md)   
 [自訂檔案 SQL > 一節](../../../ado/guide/remote-data-service/customization-file-sql-section.md)   
 [DataFactory 自訂](../../../ado/guide/remote-data-service/datafactory-customization.md)   
 [必要的用戶端設定](../../../ado/guide/remote-data-service/required-client-settings.md)   
 [了解自訂檔](../../../ado/guide/remote-data-service/understanding-the-customization-file.md)   
 [撰寫您自己的自訂處理常式](../../../ado/guide/remote-data-service/writing-your-own-customized-handler.md)


