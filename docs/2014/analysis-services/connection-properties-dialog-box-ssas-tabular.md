---
title: 連接屬性對話方塊（SSAS-表格式） |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.ssmsimbi.ConnectionProperties.F1
ms.assetid: 17bae8ae-2ba0-4978-be70-61c687f59d54
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 26fa80cc770d4bee9163ec18c21b35bd8c807bde
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/26/2020
ms.locfileid: "66086986"
---
# <a name="connection-properties-dialog-box-ssas---tabular"></a>連接屬性對話方塊 (SSAS - 表格式)
  在 SQL Server Management Studio 中，使用此頁面檢視或修改表格式模型資料庫所用之資料來源的連接屬性。  
  
 此對話方塊提供時間戳記和其他描述性資訊，再加上決定連接特性的可自訂屬性。  
  
## <a name="options"></a>選項。  
  
|詞彙|定義|  
|----------|----------------|  
|**名稱**|指定資料來源的名稱。|  
|**識別碼**|顯示資料來源物件的識別碼。|  
|**描述**|顯示資料來源物件的描述。|  
|**建立時間戳記**|顯示建立資料庫的日期和時間。|  
|**上次結構描述更新**|顯示上次更新資料庫的中繼資料的日期和時間。|  
|**連接字串**|顯示連接字串，這個連接字串用於連接到提供資料給模型的資料來源。|  
|**最大連接數目**|指定這個資料庫的用戶端連接數目上限。|  
|**實施**|有效值是 ReadCommitted 或快照集。 如需詳細資訊，請參閱 [Isolation 元素 &#40;ASSL&#41;](https://docs.microsoft.com/bi-reference/assl/properties/isolation-element-assl)。|  
|**查詢超時**|指定一段時間 (以秒為單位)，經過這段時間之後，嘗試擷取資料的行為就會逾時。|  
|**Managed 提供者**|指定 Managed 提供者的名稱。 如果資料來源連接使用原生 OLE DB 提供者，此值為空白。|  
|**模擬資訊**|指定用於下列項目的模擬帳戶：在處理或重新整理資料時的資料庫連接、針對關聯式資料存放區執行的查詢 (透過 DirectQuery)、非正規 (out-of-line) 繫結，遠端資料分割，以及從目標到來源的資料庫同步處理。<br /><br /> 有效值包含 Analysis Services 服務帳戶或一組特定的 Windows 認證。 請勿指定 **[使用目前使用者的認證]** 或 **[繼承]**。 表格式模型資料庫不支援這些認證選項。|  
  
  
