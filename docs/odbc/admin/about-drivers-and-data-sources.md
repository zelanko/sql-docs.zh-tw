---
title: 關於驅動程式和資料來源 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- ODBC data source administrator [ODBC], concepts
ms.assetid: 2bb83ef1-4bbe-4be3-8c32-c4d1140aae1d
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 69516a613cbd9071686067350ced2ce5ca166a27
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "63294446"
---
# <a name="about-drivers-and-data-sources"></a>關於驅動程式和資料來源
*驅動程式*是可處理 ODBC 要求，並將資料傳回給應用程式的元件。 如有必要，驅動程式會修改成格式以了解資料來源的應用程式的要求。 您必須使用驅動程式的安裝程式來新增或刪除驅動程式從您的電腦。  
  
 *資料來源*資料庫或驅動程式所存取的檔案，並以資料來源名稱 (DSN) 會識別。 若要加入、 設定及從系統中刪除資料來源使用 ODBC 資料來源管理員。 下表說明可用的資料來源的類型。  
  
|資料來源|描述|  
|-----------------|-----------------|  
|使用者|使用者名稱 （dsn） 的電腦本機，而且可用僅供目前的使用者。 它們都會註冊在 HKEY_CURRENT_USER 登錄樹狀子目錄。|  
|系統|系統 Dsn 是而不是專門用來在使用者本機電腦。 在系統或任何具有權限的使用者可以使用資料來源設定與系統 DSN。 系統名稱 （dsn） 都會註冊在 HKEY_LOCAL_MACHINE 登錄樹狀子目錄。|  
|檔案|檔案名稱 （dsn） 皆為檔案為基礎的來源，可以安裝相同驅動程式的所有使用者之間共用，因此資料庫的存取權。 這些資料來源不需要專用的使用者也不能是本機電腦。 檔案資料來源名稱不會識別專用的登錄項目;相反地，它們會以名稱來識別檔案副檔名為.dsn。|  
  
 使用者和系統資料來源通稱為*機器*資料來源，因為它們是本機電腦。  
  
 每一個資料來源有一個索引標籤**ODBC 資料來源管理員** 對話方塊。 如需資料來源的詳細資訊，請參閱 [資料來源](../../odbc/reference/data-sources.md)。
