---
title: "自訂檔案記錄區段 |Microsoft 文件"
ms.prod: sql-non-specified
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- logs section in RDS [ADO]
- customization file in RDS [ADO]
ms.assetid: a368e264-865c-41ee-be00-d9097255c2ea
caps.latest.revision: 14
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 99d22cd98548548463f1cbd5516d26faaf4b9bf1
ms.contentlocale: zh-tw
ms.lasthandoff: 09/09/2017

---
# <a name="customization-file-logs-section"></a>自訂檔案記錄檔 > 一節
**記錄**區段包含指定名稱的作業期間會將錯誤記錄檔的記錄檔項目**DataFactory**。  
  
> [!IMPORTANT]
>  從 Windows 8 和 Windows Server 2012 開始，RDS 伺服器元件已不再包含在 Windows 作業系統中 (請參閱 < Windows 8 和[Windows Server 2012 相容性手冊](https://www.microsoft.com/en-us/download/details.aspx?id=27416)如需詳細資訊)。 Windows 的未來版本將移除 RDS 用戶端元件。 請避免在新的開發工作中使用這項功能，並規劃修改目前使用這項功能的應用程式。 使用 RDS 的應用程式應該移轉到[WCF 資料服務](http://go.microsoft.com/fwlink/?LinkId=199565)。  
  
## <a name="syntax"></a>語法  
 格式是記錄檔項目：  
  
```  
  
err=  
FileName  
  
```  
  
## <a name="remarks"></a>備註  
  
|部分|Description|  
|----------|-----------------|  
|**錯誤**|常值字串，表示這是記錄檔項目。|  
|*FileName*|完整路徑和檔案名稱。 典型的檔案名稱是**c:\msdfmap.log**。|  
  
 記錄檔會包含使用者名稱、 HRESULT、 日期和時間的每個錯誤。  
  
## <a name="see-also"></a>另請參閱  
 [自訂檔案連接 > 一節](../../../ado/guide/remote-data-service/customization-file-connect-section.md)   
 [自訂檔案 SQL > 一節](../../../ado/guide/remote-data-service/customization-file-sql-section.md)   
 [自訂檔案 UserList > 一節](../../../ado/guide/remote-data-service/customization-file-userlist-section.md)   
 [DataFactory 自訂](../../../ado/guide/remote-data-service/datafactory-customization.md)   
 [必要的用戶端設定](../../../ado/guide/remote-data-service/required-client-settings.md)   
 [了解自訂檔](../../../ado/guide/remote-data-service/understanding-the-customization-file.md)   
 [撰寫您自己的自訂處理常式](../../../ado/guide/remote-data-service/writing-your-own-customized-handler.md)



