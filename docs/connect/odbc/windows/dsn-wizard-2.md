---
description: 資料來源精靈畫面 2 (ODBC Driver for SQL Server)
title: 資料來源精靈畫面 2 (ODBC Driver for SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 08/06/2020
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 76326eeb-1144-4b9f-85db-50524c655d30
author: David-Engel
ms.author: v-jizho2
ms.openlocfilehash: d1e18939ab9d3f2e86452dd3f1847971157ca92c
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88462207"
---
# <a name="data-source-wizard-screen-2"></a>資料來源精靈螢幕 2

指定驗證的方法，並設定 Microsoft SQL Server 進階用戶端項目，以及在設定資料來源時，ODBC Driver for SQL Server 用來連接至 SQL Server 的登入與密碼。

## <a name="options"></a>選項

### <a name="with-integrated-windows-authentication"></a>整合式 Windows 驗證

指定驅動程式要求安全 (或信任) 的 SQL Server 連線。 選取之後，不論伺服器目前的登入安全性模式為何，SQL Server 都會透過此資料來源，使用整合式登入安全性來建立連接。 所有提供的登入識別碼或密碼都會被忽略。 SQL Server 系統管理員必須已將您的 Windows 登入與 SQL Server 登入識別碼建立關聯 (例如，透過使用 SQL Server Management Studio)。

(選擇性) 您可以指定伺服器的服務主體名稱 (SPN)。

### <a name="with-active-directory-integrated-authentication"></a>使用 Active Directory 整合式驗證

指定使用 Azure Active Directory 向 SQL Server 進行驅動程式驗證。 選取之後，不論伺服器目前的登入安全性模式為何，SQL Server 都會透過此資料來源，使用 Azure Active Directory 整合式登入安全性來建立連接。

### <a name="with-sql-server-authentication"></a>使用 SQL Server 驗證

指定使用登入識別碼與密碼向 SQL Server 進行驅動程式驗證。

### <a name="with-active-directory-password-authentication"></a>使用 Active Directory 密碼驗證

指定使用 Azure Active Directory 登入識別碼與密碼向 SQL Server 進行驅動程式驗證。

### <a name="with-active-directory-interactive-authentication"></a>使用 Active Directory 互動式驗證

指定透過提供登入識別碼，使用 Azure Active Directory 互動模式向 SQL Server 進行驅動程式驗證。 此選項將會觸發 [Azure 驗證] 提示對話方塊。

### <a name="with-managed-identity-authentication"></a>使用受控識別驗證

指定驅動程式使用受控識別向 SQL Server 進行驗證。

### <a name="login-id"></a>登入識別碼

指定在選取下列項目時，當驅動程式連線到 SQL Server 時所使用的登入識別碼：**由使用者所輸入的登入識別碼及密碼進行 SQL Server 帳戶驗證**、**利用使用者所輸入的登入識別碼與密碼，進行 Active Directory 密碼驗證**，或**透過 Active Directory 互動式驗證，其使用由使用者輸入的登入識別碼**。 如果已選取 [With Managed Identity authentication] \(使用受控識別驗證\)，請指定受控識別的物件識別碼，或是保留空白以使用預設身分識別。 此欄位僅適用於用來決定伺服器預設設定的連線，而不適用於在建立連線後使用資料來源建立的後續連線 (使用受控識別驗證除外)。

### <a name="password"></a>密碼

指定在選取下列項目時，當驅動程式連線到 SQL Server 時所使用的密碼：**由使用者所輸入的登入識別碼及密碼進行 SQL Server 帳戶驗證**或**利用使用者所輸入的登入識別碼與密碼，進行 Active Directory 密碼驗證**。 此欄位僅適用於用來決定伺服器預設設定的連線，而不適用於使用新的資料來源建立的後續連線。

如果已選取 [整合式 Windows 驗證]**** 或 [利用 Active Directory 整合式驗證]****，會停用 [登入識別碼]**** 與 [密碼]**** 方塊。

### <a name="next"></a>下一個

繼續前往精靈的下一個畫面。

### <a name="back"></a>上一步

返回精靈的上一個畫面。

## <a name="next-steps"></a>後續步驟

[資料來源精靈畫面 1](../../../connect/odbc/windows/dsn-wizard-1.md)

[資料來源精靈畫面 3](../../../connect/odbc/windows/dsn-wizard-3.md)

