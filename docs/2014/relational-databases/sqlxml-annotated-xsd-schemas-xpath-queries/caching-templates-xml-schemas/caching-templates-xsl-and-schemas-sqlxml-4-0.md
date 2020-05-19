---
title: 快取範本、XSL 和架構（SQLXML 4.0） |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: xml
ms.topic: reference
helpviewer_keywords:
- SQLXML, caching
- cache [SQLXML]
- memory [SQLXML]
ms.assetid: 80b4fa79-243f-442c-9f22-74ad66186501
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 3758409cef566c41f55dc90d3f508a12bb3236a9
ms.sourcegitcommit: b72c9fc9436c44c6a21fd96223c73bf94706c06b
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/01/2020
ms.locfileid: "82703319"
---
# <a name="caching-templates-xsl-and-schemas-sqlxml-40"></a>快取範本、XSL 和結構描述 (SQLXML 4.0)
  為增進效能，[!INCLUDE[msCoName](../../../includes/msconame-md.md)] SQLXML 4.0 支援快取範本、XSL 和結構描述。  
  
 系統會快取所有結構描述、範本和 XSL 檔案 (除了來自 http:// 或 ftp:// 位置的檔案之外)。 當程序正在執行時，快取的檔案仍然在記憶體中。 當程序結束時，所有快取都會消失。 因此，如果每個查詢執行一個程序，快取的效益可能就不明顯。  
  
 本節中的主題提供有關快取的詳細資訊。  
  
## <a name="in-this-section"></a>本節內容  
 [&#40;SQLXML 4.0&#41;的範本快取](template-caching-sqlxml-4-0.md)  
 描述並提供範本快取的登錄機碼。  
  
 [XSL Caching &#40;SQLXML 4.0&#41;](xsl-caching-sqlxml-4-0.md)  
 描述並提供 XSL 快取的登錄機碼。  
  
 [架構快取 &#40;SQLXML 4.0&#41;](schema-caching-sqlxml-4-0.md)  
 討論與結構描述快取相關的 SQLXML 並行安裝問題，並提供結構描述快取的登錄機碼。  
  
  
