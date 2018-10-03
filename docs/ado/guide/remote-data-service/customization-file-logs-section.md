---
title: 自訂檔案記錄區段 |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- logs section in RDS [ADO]
- customization file in RDS [ADO]
ms.assetid: a368e264-865c-41ee-be00-d9097255c2ea
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 64512857af5ed42e9c91a52e5a00f9a7f642520a
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47726466"
---
# <a name="customization-file-logs-section"></a>自訂檔案 Logs 區段
**記錄檔**一節包含記錄檔項目，指定的作業期間會將錯誤記錄檔的名稱**DataFactory**。  
  
> [!IMPORTANT]
>  從 Windows 8 和 Windows Server 2012 開始，RDS 伺服器元件不會再包含在 Windows 作業系統中 (請參閱 Windows 8 和[Windows Server 2012 相容性操作手冊](https://www.microsoft.com/en-us/download/details.aspx?id=27416)如需詳細資訊)。 RDS 用戶端元件將會在 Windows 的未來版本中移除。 請避免在新的開發工作中使用這項功能，並規劃修改目前使用這項功能的應用程式。 使用 RDS 的應用程式應該移轉至[WCF 資料服務](http://go.microsoft.com/fwlink/?LinkId=199565)。  
  
## <a name="syntax"></a>語法  
 記錄檔項目屬於表單：  
  
```  
  
err=  
FileName  
  
```  
  
## <a name="remarks"></a>備註  
  
|部分|描述|  
|----------|-----------------|  
|**err**|常值字串，表示這是記錄檔項目。|  
|*FileName*|完整路徑和檔案名稱。 典型的檔案名稱是**c:\msdfmap.log**。|  
  
 記錄檔會包含使用者名稱、 HRESULT、 日期和時間的每個錯誤。  
  
## <a name="see-also"></a>另請參閱  
 [自訂檔案 Connect 區段](../../../ado/guide/remote-data-service/customization-file-connect-section.md)   
 [自訂檔案 SQL 區段](../../../ado/guide/remote-data-service/customization-file-sql-section.md)   
 [自訂檔案 UserList 區段](../../../ado/guide/remote-data-service/customization-file-userlist-section.md)   
 [DataFactory 自訂](../../../ado/guide/remote-data-service/datafactory-customization.md)   
 [必要的用戶端設定](../../../ado/guide/remote-data-service/required-client-settings.md)   
 [了解自訂檔案](../../../ado/guide/remote-data-service/understanding-the-customization-file.md)   
 [撰寫您自己的自訂處理常式](../../../ado/guide/remote-data-service/writing-your-own-customized-handler.md)


