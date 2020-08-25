---
description: 自訂檔案 UserList 區段
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
author: rothja
ms.author: jroth
ms.openlocfilehash: 14308aeda28311b73dc34a323a9a9bf662770e8b
ms.sourcegitcommit: c4d564435c008e2c92035efd2658172f20f07b2b
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/24/2020
ms.locfileid: "88759812"
---
# <a name="customization-file-userlist-section"></a>自訂檔案 UserList 區段
**Userlist**區段適用于具有相同區段*識別碼*參數的**connect**區段。  
  
 這個區段可以包含*使用者存取專案*，此專案會指定指定之使用者的存取權限，並覆寫 [相符的**連接]** 區段中的*預設**存取專案*。  
  
> [!IMPORTANT]
>  從 Windows 8 和 Windows Server 2012 開始，Windows 作業系統中不再包含 RDS 伺服器元件 (如需詳細) 資訊，請參閱 Windows 8 和 [Windows server 2012 相容性操作手冊](https://www.microsoft.com/download/details.aspx?id=27416) 。 未來的 Windows 版本將移除 RDS 用戶端元件。 請避免在新的開發工作中使用這項功能，並規劃修改目前使用這項功能的應用程式。 使用 RDS 的應用程式應該遷移至 [WCF 資料服務](https://go.microsoft.com/fwlink/?LinkId=199565)。  
  
## <a name="syntax"></a>語法  
 使用者存取專案的形式如下：  
  
 使用者_名稱_**=**   
 **_accessRights_**  
  
|部分|描述|  
|----------|-----------------|  
|*userName*|採用此連接之人員的 *使用者名稱* 。 有效的使用者名稱會與 [IIS **Service Manager** ] 對話方塊建立。|  
|**_accessRights_**|下列其中一個存取權限：<br /><br /> -   **NoAccess** -使用者無法存取資料來源。<br />-   **ReadOnly** 使用者可以讀取資料來源。<br />-   **ReadWrite** -使用者可以讀取或寫入資料來源。|  
  
## <a name="see-also"></a>另請參閱  
 [自訂檔案連接區段](./customization-file-connect-section.md)   
 [自訂檔案記錄區段](./customization-file-logs-section.md)   
 [自訂檔案 SQL 區段](./customization-file-sql-section.md)   
 [DataFactory 自訂](./datafactory-customization.md)   
 [必要的用戶端設定](./required-client-settings.md)   
 [瞭解自訂檔案](./understanding-the-customization-file.md)   
 [撰寫您自己的自訂處理常式](./writing-your-own-customized-handler.md)