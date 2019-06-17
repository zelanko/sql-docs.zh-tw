---
title: 資料庫屬性對話方塊 (SSAS-表格式) |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.ssmsimbi.DatabaseProperties.f1
ms.assetid: 0f0ec02f-7b55-40ea-8a04-ed0deb1efd7a
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 8361508d678e407be9bed6eb18e8c221364daf61
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "66082356"
---
# <a name="database-properties-dialog-box-ssas---tabular"></a>資料庫屬性對話方塊 (SSAS - 表格式)
  此對話方塊提供時間戳記和其他描述性資訊，再加上決定資料庫是否使用快取資料的可自訂屬性。 其他可自訂屬性包含變更資料庫名稱和指定模擬選項。  
  
## <a name="options"></a>選項  
  
|詞彙|定義|  
|----------|----------------|  
|**名稱**|**[名稱]** 是唯一識別伺服器資料庫的資料庫名稱。 在變更資料庫名稱時，請考慮對現有連接字串中使用目前名稱的報表和用戶端應用程式造成的影響。 您需要更新現有報告中的連接字串，以避免存取被拒錯誤。 此外，此資料庫的來源表格式模型最可能使用原始名稱。 請考慮更新模型中的資料庫部署屬性，以確保該模型未來的更新會發行至預期的資料庫。|  
|**ID**|顯示資料庫的識別碼。|  
|**說明**|鍵入以變更資料庫的描述。|  
|**建立時間戳記**|顯示建立資料庫的日期和時間。|  
|**上次結構描述更新**|顯示上次更新資料庫的中繼資料的日期和時間。|  
|**上次更新**|顯示上次更新資料庫之資料的日期和時間。|  
|**讀寫模式**|這是唯讀屬性，但是您可以利用一連串的 [中斷連結]  與 [連結]  命令加以變更，因為此屬性是 [連結]  命令的參數。 如需詳細資訊，請參閱 [資料庫 ReadWriteModes](multidimensional-models/database-readwritemodes.md)。|  
|**DirectQueryMode**|指定資料庫只使用記憶體中儲存體 (沒有磁碟儲存體)、只使用磁碟儲存體，或使用兩者的某種組合。 有效值是 InMemory、DirectQuery、InMemoryWithDirectQuery (大部分是以記憶體為主，少部分分頁至磁碟)，或 DirectQueryWithInMemory (大部分是以磁碟為主，少部分是記憶體中儲存體)。 如需詳細資訊，請參閱 < [DirectQuery 部署案例&#40;SSAS 表格式&#41;](directquery-deployment-scenarios-ssas-tabular.md)。|  
|**資料來源模擬資訊**|指定用於下列項目的模擬帳戶：在處理或重新整理本機或遠端資料分割的資料時的資料庫連接、針對關聯式資料存放區執行的查詢 (透過 DirectQuery)、非正規 (out-of-line) 繫結，以及從目標到來源的資料庫同步處理。<br /><br /> 有效值包含 Analysis Services 服務帳戶或一組特定的 Windows 認證。 請勿指定 **[使用目前使用者的認證]** 。 表格式模型資料庫不支援該認證選項。|  
|**上次處理**|顯示上次處理資料庫的日期和時間。|  
|**估計的大小**|顯示資料庫之估計的大小。|  
|**儲存體位置**|指定資料庫的位置。 如果資料庫位於預設資料目錄中，此值為空白。|  
  
  
