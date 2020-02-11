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
ms.openlocfilehash: 4e9b7229882b3b7f94e6b059e04c6496bde09641
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "67938046"
---
# <a name="about-drivers-and-data-sources"></a>關於驅動程式和資料來源
*驅動程式*是處理 ODBC 要求並將資料傳回給應用程式的元件。 如有必要，驅動程式會將應用程式的要求修改為數據源所瞭解的表單。 您必須使用驅動程式的安裝程式，從您的電腦新增或刪除驅動程式。  
  
 *資料來源*是由驅動程式存取的資料庫或檔案，而且是由資料來源名稱（DSN）所識別。 使用 [ODBC 資料來源管理員] 來新增、設定和刪除系統中的資料來源。 下表描述可使用的資料來源類型。  
  
|資料來源|描述|  
|-----------------|-----------------|  
|User|使用者 Dsn 位於電腦的本機，而且只能由目前的使用者使用。 它們會在 HKEY_CURRENT_USER 登錄子樹中註冊。|  
|系統|系統 Dsn 是電腦的本機，而不是專供使用者使用。 系統或任何具有許可權的使用者都可以使用與系統 DSN 一併設定的資料來源。 系統 Dsn 會在 HKEY_LOCAL_MACHINE registry 子樹中註冊。|  
|檔案|檔案 Dsn 是以檔案為基礎的來源，可在已安裝相同驅動程式的所有使用者之間共用，因此可以存取資料庫。 這些資料來源不需要專門提供給使用者，也不能在本機電腦上使用。 專用登錄專案不會識別檔案資料來源名稱;相反地，它們是以副檔名為 .dsn 的檔案名來識別。|  
  
 使用者和系統資料來源統稱為*電腦資料來源，因為*它們在電腦的本機上。  
  
 這些資料來源中的每一個都有 [ **ODBC 資料來源管理員**] 對話方塊中的索引標籤。 如需資料來源的詳細資訊，請參閱 [資料來源](../../odbc/reference/data-sources.md)。
