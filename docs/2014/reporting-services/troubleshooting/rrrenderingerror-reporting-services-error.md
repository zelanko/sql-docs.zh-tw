---
title: rrRenderingError - Reporting Services 錯誤 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- rrRenderingError
ms.assetid: 0751efc3-b81b-44ee-8aac-8560f86ca322
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 390cd2efde37d5d04b7b7ef3a3799222e024b7e4
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/23/2019
ms.locfileid: "66099274"
---
# <a name="rrrenderingerror---reporting-services-error"></a>rrRenderingError - Reporting Services 錯誤
    
## <a name="details"></a>詳細資料  
  
|||  
|-|-|  
|產品名稱|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|  
|事件識別碼|rrRenderingError|  
|事件來源|Microsoft.ReportingServices.Diagnostics.Utilities.ErrorStrings.resources.Strings|  
|元件|[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]|  
|訊息文字|轉譯報表期間發生錯誤。 (rrRenderingError) %1|  
  
## <a name="explanation"></a>說明  
 當 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 無法轉譯或匯出報表時，就會傳回這個訊息。  
  
 當指定的 RDL 頁面大小無效時，通常會產生一個訊息，指出不支援該大小。 請指定有效的 RDL 頁面大小，然後重試一遍。  
  
 當指定了不支援的單位類型時，通常會產生一個訊息，指出不支援 RDL 大小度量。 有效的單位類型為 cm、in、mm、pc 和 pt。 請指定有效的單位類型，然後重試一遍。  
  
 當指定了頁面大小的負數度量 (如 -5 cm) 時，通常會產生一個訊息，指出不支援負數大小。 請為頁面大小指定正數，然後重試一遍。  
  
 當頁面大小的度量超出有效頁面邊界大小時，通常會產生一個訊息，指出指定的 RDL 大小超出範圍。 請針對頁面大小指定在有效頁面邊界大小內的度量。  
  
 當 RDL 中指定的色彩無效時，通常會產生一個訊息，指出指定的色彩無效。 請選擇 RDL 支援的色彩，然後重試一遍。  
  
 當指定的動作標籤無效時，通常會產生一個訊息，指出動作標籤在使用單一動作時只是選擇性，而且加入多個動作需要每一個動作的標籤。 請針對每一個動作指定有效的動作標籤。  
  
 當針對資料類型指定了不正確的樣式值時，通常會產生一個訊息，指出樣式引數必須是特定的類型。 RDL 規格會識別您可以在不同 RDL 元素的樣式值中使用的有效類型。 例如，背景色彩的不正確樣式值為 "2pt"，而不正確的高度值為 "true"。 請指定一個正確的值，然後再試一次。  
  
 當指定的框線樣式無效時，通常會產生一個訊息，指出不支援此框線樣式。 請指定支援的框線樣式，然後重試一遍。  
  
 當影像報表項目的指定 mimetype 無效時，通常會產生一個訊息，指出不支援該影像 mimetype。 請為此報表項目指定支援的 mimetype，然後重試一遍。  
  
 當超出 Excel 工作表內的資料列數時，通常會產生一個訊息，指出資料列數超出每一工作表的最大可能資料列數。 Excel 最多支援 65,000 個資料列。  
  
 當超出 Excel 工作表內的資料行數時，通常會產生一個訊息，指出資料行數超出每一工作表的最大可能資料行數。  
  
## <a name="user-action"></a>使用者動作  
  
## <a name="internal-only"></a>僅供內部使用  
  
