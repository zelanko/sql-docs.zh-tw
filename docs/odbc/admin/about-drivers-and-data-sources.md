---
description: 關於驅動程式和資料來源
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 141a8e99a219923fa8e658c2600e79cad6f4ae93
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88386584"
---
# <a name="about-drivers-and-data-sources"></a>關於驅動程式和資料來源
*驅動程式* 是處理 ODBC 要求並將資料傳回給應用程式的元件。 必要時，驅動程式會將應用程式的要求修改為數據源可理解的表單。 您必須使用驅動程式的安裝程式來新增或刪除電腦中的驅動程式。  
  
 *資料來源* 是由驅動程式存取的資料庫或檔案，而且是由 (DSN) 的資料來源名稱所識別。 使用「ODBC 資料來源管理員」來新增、設定和刪除您系統中的資料來源。 下表說明可使用的資料來源類型。  
  
|資料來源|描述|  
|-----------------|-----------------|  
|User|使用者 Dsn 是電腦的本機使用者，只能由目前的使用者使用。 它們會註冊在 HKEY_CURRENT_USER 登錄子樹中。|  
|系統|系統 Dsn 是電腦本機的，而不是使用者專用的。 系統或具有許可權的任何使用者都可以使用與系統 DSN 一起設定的資料來源。 系統 Dsn 會註冊在 HKEY_LOCAL_MACHINE 登錄子樹中。|  
|檔案|檔案 Dsn 是以檔案為基礎的來源，可以在安裝相同驅動程式的所有使用者之間共用，因此可以存取資料庫。 這些資料來源不需要專用於使用者，也不能在本機電腦上。 專用的登錄專案不會識別檔案資料來源名稱;相反地，它們是由副檔名為 dsn 的檔案名所識別。|  
  
 使用者和系統資料來源統稱為 *電腦資料來源，因為* 它們是電腦的本機資料來源。  
  
 在 [ **ODBC 資料來源管理員** ] 對話方塊中，每個資料來源都有一個索引標籤。 如需資料來源的詳細資訊，請參閱 [資料來源](../../odbc/reference/data-sources.md)。
