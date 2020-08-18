---
description: 以程式設計方式設定 Access 驅動程式的選項
title: 以程式設計方式設定 Access 驅動程式的選項 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- Access driver [ODBC], setting options programmatically
- ODBC desktop database drivers [ODBC], Access driver
- Jet-based ODBC drivers [ODBC], Access driver
- desktop database drivers [ODBC], Access driver
ms.assetid: 1690eb71-0cd3-4c00-9e15-f6a3ac5316dd
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 9ae798b3c3d91917e461bb6b5a58cb06734870d1
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88412414"
---
# <a name="setting-options-programmatically-for-the-access-driver"></a>以程式設計方式設定 Access 驅動程式的選項

|選項|描述|方法|  
|------------|-----------------|------------|  
|緩衝區大小|以 kb 為單位的內部緩衝區大小（以 kb 為單位），這是 Microsoft Access 用來將資料傳入和傳出磁片的大小。 預設緩衝區大小為 2048 KB (顯示為 2048) 。 可以輸入256可整除的任何整數值。|若要動態設定這個選項，請在 [SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-access-driver.md)的呼叫中使用 MAXBUFFERSIZE 關鍵字。|  
|資料來源名稱|識別資料來源的名稱，例如薪資或人員。|若要動態設定此選項，請在[SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-access-driver.md)的呼叫中使用**DSN**關鍵字。|  
|資料庫|您可以設定 Microsoft Access 資料來源，而不需選取或建立資料庫。 如果在安裝時未提供任何資料庫，則在連接至資料來源時，系統會提示使用者選擇資料庫檔案。|若要動態設定這個選項，請在[SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-access-driver.md)的呼叫中使用**DBQ**關鍵字。|  
|描述|資料來源中資料的選擇性描述;例如，「雇用日期、薪資歷程記錄和目前的員工評論」。|若要動態設定這個選項，請在[SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-access-driver.md)的呼叫中使用**DESCRIPTION**關鍵字。|  
|獨佔|如果選取 [ **獨佔** ] 方塊，資料庫將會在獨佔模式中開啟，而且一次只能由一個使用者存取。 在獨佔模式中執行時，效能會增強。|若要動態設定這個選項，請在[SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-access-driver.md)的呼叫中使用**EXCLUSIVE**關鍵字。|  
|ImplicitCommitSync|決定如何將在交易外所做的變更寫入資料庫。 此值一開始會設定為 "Yes"，這表示 Microsoft Access 驅動程式會等候內部/隱性交易中的認可完成。|此選項包含在 Microsoft Access 驅動程式的 [ **設定 Advanced Options** ] 對話方塊中。|  
|頁面超時|以毫秒為單位，指定頁面 (（如果未使用）) 在被移除之前保留在緩衝區中的時間長度（以毫秒為單位）。 若為 Microsoft Access 驅動程式，預設值為500毫秒 (0.5 秒) 。 此選項適用于所有使用 ODBC 驅動程式的資料來源。<br /><br /> 頁面超時不可以是0，因為有固有的延遲。 即使 page timeout 選項設定為低於該值，頁面的超時時間也不能小於固有的延遲。|若要動態設定這個選項，請在[SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-access-driver.md)的呼叫中使用**PAGETIMEOUT**關鍵字。|  
|唯讀|將資料庫指定為唯讀。|若要動態設定這個選項，請在[SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-access-driver.md)的呼叫中使用**READONLY**關鍵字。|  
|系統資料庫|要與您想要存取的 Microsoft Access 資料庫搭配使用的 Microsoft Access 系統資料庫完整路徑。<br /><br /> 按一下 [ **系統資料庫** ] 按鈕，以選取要使用的系統資料庫。 ODBC Microsoft Access 驅動程式會提示使用者輸入名稱和密碼。 預設名稱為 Admin，且管理使用者的 Microsoft Access 中的預設密碼為空字串。<br /><br /> 若要提高 Microsoft Access 資料庫的安全性，請建立新的使用者以取代系統管理員使用者並刪除系統管理員使用者，或變更系統管理員使用者可存取的物件。|若要動態設定這個選項，請在[SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-access-driver.md)的呼叫中使用**SYSTEMDB**關鍵字。|  
|Threads|引擎要使用的背景執行緒數目。 若為 Microsoft Access 驅動程式，此值預設為3，但可以變更。 如果資料庫中有大量活動，使用者可能會想要增加執行緒的數目。<br /><br /> 此選項包含在 Microsoft Access 驅動程式的 [ **設定 Advanced Options** ] 對話方塊中。|若要動態設定這個選項，請在[SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-access-driver.md)的呼叫中使用**THREADS**關鍵字。|  
|UserCommitSync|判斷 Microsoft Access 驅動程式是否會以非同步方式執行明確的使用者定義交易。 此值最初會設定為 "Yes"，這表示 Microsoft Access 驅動程式會等候使用者定義交易中的認可完成。<br /><br /> 將此選項設定為 False 可能會在多使用者環境中產生無法預期的結果。|若要動態設定這個選項，請在[SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-access-driver.md)的呼叫中使用**USERCOMMITSYNC**關鍵字。|
