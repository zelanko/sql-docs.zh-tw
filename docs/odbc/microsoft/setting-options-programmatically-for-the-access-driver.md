---
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
ms.openlocfilehash: 9a90f0a20569a2a0a5bb93dec7aa4b95b50093dc
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "81300788"
---
# <a name="setting-options-programmatically-for-the-access-driver"></a>以程式設計方式設定 Access 驅動程式的選項

|選項|描述|方法|  
|------------|-----------------|------------|  
|緩衝區大小|內部緩衝區的大小（以 kb 為單位），由 Microsoft Access 用來將資料傳輸到磁片或從中傳送資料。 預設緩衝區大小為 2048 KB （顯示為2048）。 可以輸入256整除的任何整數值。|若要動態設定此選項，請在[SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-access-driver.md)的呼叫中使用 MAXBUFFERSIZE 關鍵字。|  
|資料來源名稱|識別資料來源的名稱，例如薪資或人員。|若要動態設定此選項，請在[SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-access-driver.md)的呼叫中使用**DSN**關鍵字。|  
|資料庫|您可以設定 Microsoft Access 資料來源，而不需要選取或建立資料庫。 如果在安裝時未提供任何資料庫，則在連接到資料來源時，系統會提示使用者選擇資料庫檔案。|若要動態設定此選項，請在[SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-access-driver.md)的呼叫中使用**DBQ**關鍵字。|  
|描述|資料來源中資料的選擇性描述;例如，「雇用日期、薪資歷程記錄，以及所有員工的目前評論」。|若要動態設定此選項，請在[SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-access-driver.md)的呼叫中使用**DESCRIPTION**關鍵字。|  
|獨佔|如果選取 [**獨佔**] 方塊，資料庫將會以獨佔模式開啟，而且一次只能由一個使用者存取。 在獨佔模式中執行時，效能會增強。|若要動態設定此選項，請在[SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-access-driver.md)的呼叫中使用**EXCLUSIVE**關鍵字。|  
|ImplicitCommitSync|決定如何將交易外部所做的變更寫入至資料庫。 這個值一開始是設定為 "Yes"，這表示 Microsoft Access 驅動程式會等待內部/隱性交易中的認可完成。|此選項包含在 Microsoft Access 驅動程式的 [**設定高級選項**] 對話方塊中。|  
|頁面超時|指定在移除之前，頁面（如果未使用）保留在緩衝區中的時間長度（以毫秒為單位）。 若為 Microsoft Access 驅動程式，預設值為500毫秒（0.5 秒）。 此選項適用于使用 ODBC 驅動程式的所有資料來源。<br /><br /> 頁面超時不可以是0，因為有固有的延遲。 頁面超時不能小於固有的延遲，即使 page timeout 選項設為低於該值也一樣。|若要動態設定此選項，請在[SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-access-driver.md)的呼叫中使用**PAGETIMEOUT**關鍵字。|  
|唯讀|將資料庫指定為唯讀。|若要動態設定此選項，請在[SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-access-driver.md)的呼叫中使用**READONLY**關鍵字。|  
|系統資料庫|要與您要存取的 Microsoft Access 資料庫搭配使用的 Microsoft Access 系統資料庫的完整路徑。<br /><br /> 按一下 [**系統資料庫**] 按鈕，以選取要使用的系統資料庫。 ODBC Microsoft Access 驅動程式會提示使用者輸入名稱和密碼。 預設名稱為 Admin，而 Microsoft Access 中系統管理員使用者的預設密碼為空字串。<br /><br /> 若要提高 Microsoft Access 資料庫的安全性，請建立新的使用者來取代系統管理員使用者，並刪除系統管理員使用者，或變更系統管理員使用者擁有存取權的物件。|若要動態設定此選項，請在[SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-access-driver.md)的呼叫中使用**SYSTEMDB**關鍵字。|  
|執行緒|要使用之引擎的背景執行緒數目。 若為 Microsoft Access 驅動程式，此值預設為3，但可以變更。 如果資料庫中有大量活動，使用者可能會想要增加執行緒的數目。<br /><br /> 此選項包含在 Microsoft Access 驅動程式的 [**設定高級選項**] 對話方塊中。|若要動態設定此選項，請在[SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-access-driver.md)的呼叫中使用**THREADS**關鍵字。|  
|UserCommitSync|判斷 Microsoft Access 驅動程式是否會以非同步方式執行明確的使用者定義交易。 這個值一開始是設定為 "Yes"，這表示 Microsoft Access 驅動程式會等待使用者定義交易中的認可完成。<br /><br /> 將此選項設定為 False，可能會在多使用者環境中造成無法預期的結果。|若要動態設定此選項，請在[SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-access-driver.md)的呼叫中使用**USERCOMMITSYNC**關鍵字。|
