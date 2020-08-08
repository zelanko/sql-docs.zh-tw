---
title: )  (SybaseToSQL) 的全域設定 (記錄檔 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: 4cb4da20-3b99-4aae-8c80-329ee23e796e
author: nahk-ivanov
ms.author: alexiva
ms.openlocfilehash: 10a0b901a8e3681e4d74eccbe31e74119ad1ad6e
ms.sourcegitcommit: e8f6c51d4702c0046aec1394109bc0503ca182f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/07/2020
ms.locfileid: "87931613"
---
# <a name="global-settings-logging-sybasetosql"></a>全域設定 (記錄) (SybaseToSQL)
使用 [**通用設定**] 對話方塊來指定 SSMA 的記錄設定。 一般而言，只有在使用產品支援時，才會變更這些設定。  
  
若要存取此對話方塊，請在 [**工具**] 功能表上選取 [**通用設定**]，然後按一下左窗格底部的 [**記錄**] 按鈕。  
  
## <a name="options"></a>選項。  
**訊息層級**  
下列選項適用于 [**訊息層級**] 底下：  
  
|選項|描述|  
|----------|---------------|  
|**[所有類別]**|用來設定下列所有選項的記錄層級。|  
|**收集器**|收集有關來源架構的中繼資料，並將其儲存至專案。|  
|**Converter**|將源資料庫物件的結構（例如資料表和預存程式）轉換成對應 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的結構。|  
|**資料移轉**|將源資料庫中的資料移轉至 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 。|  
|**格式器**|轉換器的子元件，會產生架構的腳本 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 。|  
|**圖形化使用者介面**|當您使用 SSMA 工具時所顯示的訊息。|  
|**連結器**|解析 SQL 識別碼並提供資訊給其他元件。|  
|**其他**|所有不在其他類別中的訊息。|  
|**剖析器**|剖析來源架構。|  
|**同步器**|將源資料庫物件載入至 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 。|  
|**TreeConverter**|將來源中繼資料中的物件轉換成 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中繼資料。|  
  
針對 [**訊息層級**] 底下的每個選項，設定 SSMA 的下列其中一個記錄層級：  
  
|||  
|-|-|  
|**嚴重錯誤**|只將嚴重錯誤訊息寫入記錄檔。|  
|**錯誤**|將錯誤和嚴重錯誤訊息寫入記錄檔。|  
|**警告**|將警告、錯誤和嚴重錯誤訊息寫入記錄檔。|  
|**資訊**|將資訊、警告、錯誤和嚴重錯誤訊息寫入記錄檔。|  
|**偵錯**|將所有訊息（包括調試訊息）寫入至記錄檔。|  
  
**記錄檔路徑**  
SSMA 記錄檔的檔案路徑和名稱。 若要指定不同的名稱，請按一下目前的路徑，然後按一下 [流覽 (**...** ]) ] 按鈕。  
  
**記錄檔大小**  
記錄檔的大小上限（以 KB 為單位）。 大小下限為 10 KB。 預設大小為 10240 KB。  
  
**記錄檔總數**  
當其中一個記錄檔填滿時，SSMA 會將記錄檔重新命名並啟動新的記錄檔。 藉由使用此設定，指定要保留的記錄檔數目上限。 最小值為2。  
  
