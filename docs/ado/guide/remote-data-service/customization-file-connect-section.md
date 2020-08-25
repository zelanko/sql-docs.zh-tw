---
description: 自訂檔案 Connect 區段
title: 自訂檔案連接區段 |Microsoft Docs
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
author: rothja
ms.author: jroth
ms.openlocfilehash: a8c712efc368d9b84158697d3b7e6eedfb4224ff
ms.sourcegitcommit: c4d564435c008e2c92035efd2658172f20f07b2b
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/24/2020
ms.locfileid: "88759844"
---
# <a name="customization-file-connect-section"></a>自訂檔案 Connect 區段
處理常式的預設行為是拒絕所有連接。 **Connect**區段會指定該行為的例外狀況。 例如，如果所有 **connect** 區段都不存在或空白，則預設不會進行任何連接。  
  
 **Connect**區段可以包含：  
  
-   預設存取專案，指定此連接所允許的預設讀取和寫入作業。 如果區段中沒有預設存取專案，將會忽略區段。  
  
-   取代用戶端連接字串的新連接字串。  
  
> [!IMPORTANT]
>  從 Windows 8 和 Windows Server 2012 開始，Windows 作業系統中不再包含 RDS 伺服器元件 (如需詳細) 資訊，請參閱 Windows 8 和 [Windows server 2012 相容性操作手冊](https://www.microsoft.com/download/details.aspx?id=27416) 。 未來的 Windows 版本將移除 RDS 用戶端元件。 請避免在新的開發工作中使用這項功能，並規劃修改目前使用這項功能的應用程式。 使用 RDS 的應用程式應該遷移至 [WCF 資料服務](https://go.microsoft.com/fwlink/?LinkId=199565)。  
  
## <a name="syntax"></a>語法  
 預設存取專案的格式如下：  
  
```console
  
Access=  
accessRight  
  
```  
  
 取代連接字串專案的形式如下：  
  
```console
  
Connect=  
connectionString  
  
```  
  
## <a name="remarks"></a>備註  
  
|部分|描述|  
|----------|-----------------|  
|**[連接]**|表示這是連接字串專案的常值字串。|  
|**_connectionString_**|取代整個用戶端連接字串的字串。|  
|**存取**|表示這是存取專案的常值字串。|  
|**_accessRight_**|下列其中一個存取權限：<br /><br /> -   **NoAccess** -使用者無法存取資料來源。<br />-   **ReadOnly** 使用者可以讀取資料來源。<br />-   **ReadWrite** -使用者可以讀取或寫入資料來源。|  
  
 如果您想要允許任何 (作用中的連接，請停用預設的處理常式行為) ，將 [**連接預設]** 區段中的存取專案設定為 `Access=ReadWrite` ，然後刪除或批註其他任何 **[連接**_識別碼_] 區段。  
  
## <a name="see-also"></a>另請參閱  
 [自訂檔案記錄區段](./customization-file-logs-section.md)   
 [自訂檔案 SQL 區段](./customization-file-sql-section.md)   
 [自訂檔案 UserList 區段](./customization-file-userlist-section.md)   
 [DataFactory 自訂](./datafactory-customization.md)   
 [必要的用戶端設定](./required-client-settings.md)   
 [瞭解自訂檔案](./understanding-the-customization-file.md)   
 [撰寫您自己的自訂處理常式](./writing-your-own-customized-handler.md)