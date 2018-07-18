---
title: 全域設定 （記錄） (AccessToSQL) |Microsoft 文件
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.technology: ssma
ms.tgt_pltfrm: ''
ms.topic: conceptual
applies_to:
- Azure SQL Database
- SQL Server
ms.assetid: 835b09b5-eb42-47ea-b46e-e115d4d6461f
caps.latest.revision: 4
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.openlocfilehash: aaf2ccc19a6acdaba9aa1d44d563293ae8e0e390
ms.sourcegitcommit: 8aa151e3280eb6372bf95fab63ecbab9dd3f2e5e
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/05/2018
ms.locfileid: "34774304"
---
# <a name="global-settings-logging-accesstosql"></a>全域設定 （記錄） (AccessToSQL)
使用**通用設定**對話方塊來指定 SSMA 的記錄設定。 一般而言，您需要在使用產品支援時，才變更這些設定。  
  
若要存取此對話方塊，請在**工具**功能表上，選取**通用設定**，然後按一下 **記錄**在左窗格底部的按鈕。  
  
## <a name="options"></a>選項。  
**訊息層級**  
底下的下列選項可用**訊息層級**:  
  
|選項|描述|  
|----------|---------------|  
|**[所有類別目錄]**|用來設定下列選項的所有的記錄層級。|  
|**Collector**|會收集有關來源結構描述的中繼資料，並將它儲存至專案。|  
|**轉換程式**|將來源資料庫物件，例如資料表和預存程序的結構轉換成對應[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]結構。|  
|**資料遷移程式**|將資料從來源資料庫遷移[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]。|  
|**格式器**|產生指令碼轉換子的子元件[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]結構描述。|  
|**圖形化使用者介面**|當您使用 SSMA 工具時出現的訊息。|  
|**連結器**|解析的 SQL 識別碼，並提供其他元件的資訊。|  
|**其他**|不在任何其他類別目錄中的所有訊息。|  
|**剖析器**|剖析來源結構描述。|  
|**同步器**|載入來源資料庫將物件到[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]。|  
|**TreeConverter**|將轉換成來源中繼資料中的物件[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]中繼資料。|  
  
每個選項在**訊息層級**，SSMA 設定下列的記錄層級的其中一個：  
  
|||  
|-|-|  
|**嚴重錯誤**|僅嚴重的錯誤訊息寫入記錄檔。|  
|**錯誤**|錯誤和嚴重錯誤訊息寫入記錄檔。|  
|**警告**|警告、 錯誤和嚴重錯誤訊息寫入記錄檔。|  
|**資訊**|寫入記錄檔的資訊、 警告、 錯誤和嚴重錯誤訊息。|  
|**偵錯**|寫入所有的訊息，包括偵錯訊息，記錄檔。|  
  
**記錄檔路徑**  
檔案路徑和 SSMA 記錄檔的名稱。 若要指定不同的名稱，按一下 目前的路徑，然後按一下 瀏覽 (**...**) 按鈕。  
  
**記錄檔大小**  
記錄檔，以 kb 為單位的大小上限。 大小下限是 10 KB。 預設大小為 10240 KB。  
  
**記錄檔的總數**  
當一個記錄檔填滿時，SSMA 會重新命名記錄檔，並啟動新。 使用此設定，指定要保留的記錄檔的數目上限。 最小值為 2。  
  
