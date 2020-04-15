---
title: ODBC 驅動程式體繫結構 |微軟文件
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- ODBC drivers [ODBC], architecture
ms.assetid: 21a62c7c-192e-4718-a16e-aa12b0de4419
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 712de6a7a3f80ce1cd3ca854a88765dbfa531356
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81294556"
---
# <a name="odbc-driver-architecture"></a>ODBC 驅動程式架構
驅動程式編寫器必須注意驅動程式體系結構可能會影響應用程式是否可以使用特定於 DBMS 的 SQL。  
  
 ![顯示 ODBC 驅動程式架構](../../../odbc/reference/develop-driver/media/odbcdriverovruarch.gif "ODBCDriverOvruArch")  
  
 [基於檔案的驅動程式](../../../odbc/reference/file-based-drivers.md)  
  
 當驅動程式直接存取實體資料時,驅動程式同時充當驅動程式和資料來源。 驅動程式必須同時處理 ODBC 調用和 SQL 語句。 基於文件的驅動程式的開發人員必須編寫自己的資料庫引擎。  
  
 [以 DBMS 為基礎的驅動程式](../../../odbc/reference/dbms-based-drivers.md)  
  
 當使用單獨的資料庫引擎存取實體資料時,驅動程式僅處理ODBC調用。 它將 SQL 語句傳遞給資料庫引擎進行處理。  
  
 [網路架構](../../../odbc/reference/network-example.md)  
  
 檔和 DBMS ODBC 設定可以存在於單個網路上。  
  
 [其他驅動程式架構](../../../odbc/reference/other-driver-architectures.md)  
  
 當需要驅動程式處理各種數據源時,它可以用作中間件。 異構聯接引擎體系結構可以使驅動程式顯示為驅動程式管理器。 驅動程式也可以安裝在伺服器上,也可以由一系列用戶端共享它們。  
  
 有關驅動程式體系結構的詳細資訊,請參閱[有關 ODBC 架構結構](../../../odbc/reference/odbc-architecture.md)的一節中[的驅動程式管理器](../../../odbc/reference/the-driver-manager.md)和[驅動程式體系結構](../../../odbc/reference/driver-architecture.md)。  
  
 有關驅動程式問題的詳細資訊,請參閱下表中描述的位置。  
  
|問題|主題|Location|  
|-----------|-----------|--------------|  
|與應用程式與驅動程式的相容性問題|[應用程式/驅動程式相容性](../../../odbc/reference/develop-app/application-and-driver-compatibility.md)|[程式設計注意事項](../../../odbc/reference/develop-app/programming-considerations.md),在ODBC程式師的參考|  
|編寫 ODBC 驅動程式|[撰寫 ODBC 3.x 驅動程式](../../../odbc/reference/develop-app/writing-odbc-3-x-drivers.md)|[程式設計注意事項](../../../odbc/reference/develop-app/programming-considerations.md),在ODBC程式師的參考|  
|向後相容性的驅動程式指南|[回溯相容性的驅動程式方針](../../../odbc/reference/appendixes/appendix-g-driver-guidelines-for-backward-compatibility.md)|[附錄 G:向後相容性的驅動程式指南](../../../odbc/reference/appendixes/appendix-g-driver-guidelines-for-backward-compatibility.md),在 ODBC 程式師參考中|  
|連接到驅動程式|[選擇資料來源或驅動程式](../../../odbc/reference/develop-app/choosing-a-data-source-or-driver.md)|[連接到資料來源或驅動程式](../../../odbc/reference/develop-app/connecting-to-a-data-source-or-driver.md),在 ODBC 程式設計師參考|  
|識別驅動程式|[檢視驅動程式](../../../odbc/admin/viewing-drivers.md)|在 Microsoft ODBC 資料來源管理員線上說明中[檢視驅動程式](../../../odbc/admin/viewing-drivers.md)|  
|開啟連線池|[ODBC 連線池](../../../odbc/reference/develop-app/driver-manager-connection-pooling.md)|[連接到資料來源或驅動程式](../../../odbc/reference/develop-app/connecting-to-a-data-source-or-driver.md),在 ODBC 程式設計師參考|  
|Unicode/ANSI 驅動程式與連線問題|[Unicode 驅動程式](../../../odbc/reference/develop-app/unicode-drivers.md)|[程式設計注意事項](../../../odbc/reference/develop-app/programming-considerations.md),在ODBC程式師的參考|  
  
## <a name="see-also"></a>另請參閱  
 [開發 ODBC 驅動程式](../../../odbc/reference/develop-driver/developing-an-odbc-driver.md)
