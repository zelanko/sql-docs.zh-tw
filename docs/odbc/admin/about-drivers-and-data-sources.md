---
title: "驅動程式和資料來源的相關 |Microsoft 文件"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: odbc
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords: ODBC data source administrator [ODBC], concepts
ms.assetid: 2bb83ef1-4bbe-4be3-8c32-c4d1140aae1d
caps.latest.revision: "5"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: 6422e855b126245fd7118ce2518538aa0305484a
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/21/2017
---
# <a name="about-drivers-and-data-sources"></a>關於驅動程式與資料來源
*驅動程式*是可處理 ODBC 要求，以及將資料傳回給應用程式的元件。 必要時，驅動程式會修改成格式以了解資料來源的應用程式的要求。 您必須新增或刪除從您的電腦的驅動程式使用驅動程式的安裝程式。  
  
 *資料來源*資料庫或驅動程式所存取的檔案，而且由資料來源名稱 (DSN)。 若要加入、 設定及從系統中刪除資料來源使用 ODBC 資料來源管理員。 下表詳述可用的資料來源的類型。  
  
|資料來源|描述|  
|-----------------|-----------------|  
|使用者|使用者名稱 （dsn） 的電腦本機，而且可用只能由目前的使用者。 他們會註冊在 HKEY_CURRENT_USER 登錄樹狀子目錄中。|  
|系統|這些是本機電腦而不是專用使用者系統 Dsn。 系統或任何具有權限的使用者可以使用資料來源設定與系統 DSN。 系統 Dsn 會登錄的 HKEY_LOCAL_MACHINE 登錄樹狀子目錄中。|  
|檔案|檔案名稱 （dsn） 會以檔案為基礎的來源，可以安裝相同驅動程式的所有使用者之間共用，因此需要資料庫的存取權。 這些資料來源不需要專用的使用者也不能是本機電腦。 檔案資料來源名稱不會識別專用的登錄項目。相反地，而是副檔名為.dsn 識別由檔案名稱。|  
  
 使用者和系統資料來源統稱為*機器*資料來源，因為它們是本機電腦。  
  
 每一個資料來源中有一個索引標籤**ODBC 資料來源管理員** 對話方塊。 如需資料來源的詳細資訊，請參閱 [資料來源](../../odbc/reference/data-sources.md)。
