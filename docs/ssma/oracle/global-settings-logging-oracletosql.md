---
description: 全域設定 (記錄) (OracleToSQL)
title: 全域設定 (記錄)  (OracleToSQL) |Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: 12dbcd77-2b90-4fa1-9cf9-239231ea5773
author: nahk-ivanov
ms.author: alexiva
manager: alexiva
ms.openlocfilehash: fbc74e9129c642ea1b6655deb4e01ee04d92d0ee
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88480500"
---
# <a name="global-settings-logging-oracletosql"></a>全域設定 (記錄) (OracleToSQL)
使用 [ **通用設定** ] 對話方塊，即可指定 SSMA 的記錄設定。 一般而言，您只會在使用產品支援時變更這些設定。  
  
若要存取此對話方塊，請在 [ **工具** ] 功能表上選取 [ **全域設定** ]，然後按一下左窗格底部的 [ **記錄** ] 按鈕。  
  
## <a name="options"></a>選項。  
**訊息層級**  
下列選項可在 [ **訊息層級**] 底下取得：  
  
|選項|描述|  
|----------|---------------|  
|**[所有類別]**|用來設定下列所有選項的記錄層級。|  
|**收集器**|收集與來源架構相關的中繼資料，並將其儲存至專案。|  
|**Converter**|將源資料庫物件（例如資料表和預存程式）的結構轉換成對應的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 結構。|  
|**資料移轉**|將源資料庫的資料移轉至 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 。|  
|**格式器**|產生架構腳本之轉換器的子元件 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 。|  
|**圖形化使用者介面**|當您使用 SSMA 工具時所顯示的訊息。|  
|**連結器**|解析 SQL 識別碼並提供資訊給其他元件。|  
|**其他**|所有不在其他類別中的訊息。|  
|**剖析器**|剖析來源架構。|  
|**同步**|將源資料庫物件載入至 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 。|  
|**TreeConverter**|將來源中繼資料中的物件轉換成 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中繼資料。|  
|**測試人員**|當您使用 SSMA 測試人員時所顯示的訊息。|  
  
針對 [ **訊息層級**] 下的每個選項，設定下列其中一個 SSMA 記錄層級：  
  
|||  
|-|-|  
|**嚴重錯誤**|只將嚴重錯誤訊息寫入記錄檔。|  
|**錯誤**|將錯誤和嚴重錯誤訊息寫入記錄檔。|  
|**警告**|將警告、錯誤和嚴重錯誤訊息寫入記錄檔。|  
|**資訊**|將資訊、警告、錯誤和嚴重錯誤訊息寫入至記錄檔。|  
|**偵錯**|將所有訊息（包括調試訊息）寫入記錄檔。|  
  
**記錄檔路徑**  
SSMA 記錄檔的檔案路徑和名稱。 若要指定不同的名稱，請按一下目前的路徑，然後按一下 [流覽 (**...**) ] 按鈕。  
  
**記錄檔大小**  
記錄檔的大小上限（以 KB 為單位）。 大小下限為 10 KB。 預設大小為 10240 KB。  
  
**記錄檔總數**  
當一個記錄填滿時，SSMA 會重新命名記錄檔並開始新的記錄檔。 使用此設定可指定要保留的記錄檔數目上限。 最小值為2。  
  
