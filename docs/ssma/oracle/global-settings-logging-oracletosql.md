---
title: 全域設定 （記錄） (OracleToSQL) |Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.technology: ssma
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 12dbcd77-2b90-4fa1-9cf9-239231ea5773
caps.latest.revision: 4
author: Shamikg
ms.author: Shamikg
manager: v-thobro
ms.openlocfilehash: 9110798fe2c599e24642ef2f9cfd9fd772f250f1
ms.sourcegitcommit: 603d2e588ac7b36060fa0cc9c8621ff2a6c0fcc7
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/14/2018
ms.locfileid: "40394612"
---
# <a name="global-settings-logging-oracletosql"></a>全域設定 (記錄) (OracleToSQL)
使用**全域設定**對話方塊來指定 SSMA 的記錄設定。 一般而言，您會在與產品支援人員合作時，才變更這些設定。  
  
若要存取此對話方塊中，在**工具**功能表上，選取**全域設定**，然後按一下 **記錄**在左窗格底部的按鈕。  
  
## <a name="options"></a>選項。  
**訊息層級**  
底下有下列選項**訊息層級**:  
  
|選項|描述|  
|----------|---------------|  
|**[所有類別目錄]**|用來設定下列選項的所有的記錄層級。|  
|**Collector**|會收集有關來源結構描述的中繼資料，並將它儲存至專案。|  
|**轉換子**|將來源資料庫物件，例如資料表和預存程序的結構轉換成對應[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]結構。|  
|**資料遷移程式**|將資料從來源資料庫移轉[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。|  
|**格式器**|產生的指令碼轉換子的子元件[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]結構描述。|  
|**圖形化使用者介面**|當您使用 SSMA 工具時出現的訊息。|  
|**連結器**|解析的 SQL 識別項，並提供其他元件的資訊。|  
|**其他**|不在任何其他分類中的所有訊息。|  
|**剖析器**|剖析來源結構描述。|  
|**同步器**|載入來源資料庫物件[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。|  
|**TreeConverter**|將來源中繼資料中的物件轉換[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]中繼資料。|  
|**軟體測試人員**|使用 SSMA 測試人員時，會出現的訊息。|  
  
每個選項底下**訊息層級**，設定其中一個下列的記錄層級的 SSMA:  
  
|||  
|-|-|  
|**嚴重錯誤**|僅嚴重的錯誤訊息寫入記錄檔。|  
|**錯誤**|錯誤和嚴重錯誤訊息寫入記錄檔。|  
|**警告**|寫入記錄檔的警告、 錯誤和嚴重的錯誤訊息。|  
|**資訊**|寫入記錄檔的資訊、 警告、 錯誤和嚴重的錯誤訊息。|  
|**偵錯**|寫入所有的訊息，包括偵錯訊息，記錄檔。|  
  
**記錄檔路徑**  
檔案路徑和名稱的 SSMA 記錄檔。 若要指定不同的名稱，按一下目前路徑，然後按一下 瀏覽 (**...**) 按鈕。  
  
**記錄檔大小**  
記錄檔，以 kb 為單位的大小上限。 最小的大小為 10 KB。 預設大小為 10240 KB。  
  
**記錄檔的總數**  
當一個記錄檔填滿時，SSMA 會重新命名記錄檔，並啟動一個新。 使用此設定，指定要保留的記錄檔的數目上限。 最小值為 2。  
  
