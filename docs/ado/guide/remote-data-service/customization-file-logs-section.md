---
description: 自訂檔案 Logs 區段
title: 自訂檔案記錄區段 |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 11/09/2018
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- logs section in RDS [ADO]
- customization file in RDS [ADO]
ms.assetid: a368e264-865c-41ee-be00-d9097255c2ea
author: rothja
ms.author: jroth
ms.openlocfilehash: 890ba32615cdd78d9b999958f3ce3cb1e0755b81
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/27/2020
ms.locfileid: "88978239"
---
# <a name="customization-file-logs-section"></a>自訂檔案 Logs 區段
[ **記錄** 檔] 區段包含記錄檔專案，此專案會指定在 **DataFactory**作業期間記錄錯誤之檔案的名稱。  
  
> [!IMPORTANT]
>  從 Windows 8 和 Windows Server 2012 開始，Windows 作業系統中不再包含 RDS 伺服器元件 (如需詳細) 資訊，請參閱 Windows 8 和 [Windows server 2012 相容性操作手冊](https://www.microsoft.com/download/details.aspx?id=27416) 。 未來的 Windows 版本將移除 RDS 用戶端元件。 請避免在新的開發工作中使用這項功能，並規劃修改目前使用這項功能的應用程式。 使用 RDS 的應用程式應該遷移至 [WCF 資料服務](https://go.microsoft.com/fwlink/?LinkId=199565)。  
  
## <a name="syntax"></a>語法  
 記錄檔專案的格式如下：  
  
```console
  
err=  
FileName  
  
```  
  
## <a name="remarks"></a>備註  
  
|部分|描述|  
|----------|-----------------|  
|**犯 錯**|表示這是記錄檔專案的常值字串。|  
|*FileName*|完整的路徑和檔案名。 一般的檔案名是 **c:\msdfmap.log**。|  
  
 記錄檔會包含每個錯誤的使用者名稱、HRESULT、日期和時間。  
  
## <a name="see-also"></a>另請參閱  
 [自訂檔案連接區段](./customization-file-connect-section.md)   
 [自訂檔案 SQL 區段](./customization-file-sql-section.md)   
 [自訂檔案 UserList 區段](./customization-file-userlist-section.md)   
 [DataFactory 自訂](./datafactory-customization.md)   
 [必要的用戶端設定](./required-client-settings.md)   
 [瞭解自訂檔案](./understanding-the-customization-file.md)   
 [撰寫您自己的自訂處理常式](./writing-your-own-customized-handler.md)