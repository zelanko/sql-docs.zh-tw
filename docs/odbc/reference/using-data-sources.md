---
title: "使用資料來源 |Microsoft 文件"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords: data sources [ODBC], about data sources
ms.assetid: d5550619-22b2-4b16-bd08-fbabb6554c40
caps.latest.revision: "5"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: a3dd93903909fd4dccd0ef2c800846597b68614d
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/20/2017
---
# <a name="using-data-sources"></a>使用資料來源
建立資料來源通常會由終端使用者或程式的技術人員稱為*ODBC 管理員*。 ODBC 管理員會提示使用者輸入驅動程式來使用，然後再呼叫該驅動程式。 驅動程式會顯示對話方塊，要求需要連接到資料來源的資訊。 使用者輸入的資訊之後，驅動程式會將它儲存在系統上。  
  
 更新版本中，應用程式呼叫驅動程式管理員，並將其傳遞機器資料來源的名稱或包含檔案資料來源的檔案路徑。 當傳遞機器資料來源名稱，驅動程式管理員會搜尋系統以尋找資料來源所使用的驅動程式。 然後會載入驅動程式，並將資料來源的名稱傳遞給它。 驅動程式會使用資料來源的名稱尋找需要連接到資料來源的資訊。 最後，它會連接到資料來源，通常為通常不會儲存其使用者識別碼和密碼，提示使用者。  
  
 當傳遞檔案資料來源時，驅動程式管理員開啟檔案，並載入指定的驅動程式。 如果檔案也包含連接字串，它將傳遞此驅動程式。 連接字串中使用的資訊，此驅動程式會連接到資料來源。 如果不傳遞任何連接字串，則驅動程式通常會提示使用者輸入所需的資訊。
