---
description: ODBC 驅動程式架構
title: ODBC 驅動程式架構 |Microsoft Docs
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
ms.openlocfilehash: 1789d5799ed9eb15ace7ea263d1a5804c8e86e74
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88476244"
---
# <a name="odbc-driver-architecture"></a>ODBC 驅動程式架構
驅動程式寫入器必須留意驅動程式架構可能會影響應用程式是否可以使用 DBMS 特定的 SQL。  
  
 ![顯示 ODBC 驅動程式架構](../../../odbc/reference/develop-driver/media/odbcdriverovruarch.gif "ODBCDriverOvruArch")  
  
 [以檔案為基礎的驅動程式](../../../odbc/reference/file-based-drivers.md)  
  
 當驅動程式直接存取實體資料時，驅動程式會作為驅動程式和資料來源。 驅動程式必須同時處理 ODBC 呼叫和 SQL 語句。 以檔案為基礎之驅動程式的開發人員必須撰寫自己的資料庫引擎。  
  
 [以 DBMS 為基礎的驅動程式](../../../odbc/reference/dbms-based-drivers.md)  
  
 當使用不同的資料庫引擎來存取實體資料時，驅動程式只會處理 ODBC 呼叫。 它會將 SQL 語句傳遞至資料庫引擎進行處理。  
  
 [網路架構](../../../odbc/reference/network-example.md)  
  
 檔案和 DBMS ODBC 設定可以存在於單一網路上。  
  
 [其他驅動程式架構](../../../odbc/reference/other-driver-architectures.md)  
  
 需要驅動程式才能使用各種不同的資料來源時，可以將它當做中介軟體使用。 異類聯結引擎架構可讓驅動程式顯示為驅動程式管理員。 驅動程式也可以安裝在伺服器上，而這些伺服器可由一系列的用戶端共用。  
  
 如需驅動程式架構的詳細資訊，請參閱[ODBC 架構](../../../odbc/reference/odbc-architecture.md)一節中的[驅動程式管理員](../../../odbc/reference/the-driver-manager.md)和[驅動程式架構](../../../odbc/reference/driver-architecture.md)。  
  
 如需有關驅動程式問題的詳細資訊，請參閱下表所述的位置。  
  
|問題|主題|Location|  
|-----------|-----------|--------------|  
|應用程式和驅動程式的相容性問題|[應用程式/驅動程式相容性](../../../odbc/reference/develop-app/application-and-driver-compatibility.md)|ODBC 程式設計人員參考中的程式[設計考慮](../../../odbc/reference/develop-app/programming-considerations.md)|  
|撰寫 ODBC 驅動程式|[撰寫 ODBC 3.x 驅動程式](../../../odbc/reference/develop-app/writing-odbc-3-x-drivers.md)|ODBC 程式設計人員參考中的程式[設計考慮](../../../odbc/reference/develop-app/programming-considerations.md)|  
|回溯相容性的驅動程式方針|[回溯相容性的驅動程式方針](../../../odbc/reference/appendixes/appendix-g-driver-guidelines-for-backward-compatibility.md)|附錄 G：《 ODBC 程式設計人員參考》中的回溯[相容性驅動程式指導方針](../../../odbc/reference/appendixes/appendix-g-driver-guidelines-for-backward-compatibility.md)|  
|連接到驅動程式|[選擇資料來源或驅動程式](../../../odbc/reference/develop-app/choosing-a-data-source-or-driver.md)|[連接到資料來源或驅動程式](../../../odbc/reference/develop-app/connecting-to-a-data-source-or-driver.md)，位於 ODBC 程式設計人員參考|  
|識別驅動程式|[檢視驅動程式](../../../odbc/admin/viewing-drivers.md)|在 Microsoft ODBC 資料來源管理員線上說明中[查看驅動程式](../../../odbc/admin/viewing-drivers.md)|  
|啟用連接共用|[ODBC 連接共用](../../../odbc/reference/develop-app/driver-manager-connection-pooling.md)|[連接到資料來源或驅動程式](../../../odbc/reference/develop-app/connecting-to-a-data-source-or-driver.md)，位於 ODBC 程式設計人員參考|  
|Unicode/ANSI 驅動程式和連接問題|[Unicode 驅動程式](../../../odbc/reference/develop-app/unicode-drivers.md)|ODBC 程式設計人員參考中的程式[設計考慮](../../../odbc/reference/develop-app/programming-considerations.md)|  
  
## <a name="see-also"></a>另請參閱  
 [開發 ODBC 驅動程式](../../../odbc/reference/develop-driver/developing-an-odbc-driver.md)
