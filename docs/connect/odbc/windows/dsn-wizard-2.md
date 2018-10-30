---
title: 資料來源精靈畫面 2 (ODBC Driver for SQL Server) |Microsoft Docs
ms.custom: ''
ms.date: 03/21/2018
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 76326eeb-1144-4b9f-85db-50524c655d30
author: MightyPen
ms.author: v-jizho2
manager: craigg
ms.openlocfilehash: 7d352b02d118c3de14cd437daf012885d7491c1b
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MTE75
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47639516"
---
# <a name="data-source-wizard-screen-2"></a>資料來源精靈螢幕 2

指定驗證的方法，並設定 Microsoft SQL Server 進階用戶端項目，以及在設定資料來源時，ODBC Driver for SQL Server 用來連接至 SQL Server 的登入與密碼。

## <a name="options"></a>選項。

### <a name="with-integrated-windows-authentication"></a>整合式 Windows 驗證

指定驅動程式要求 SQL Server 的安全 （或信任） 連線。 選取之後，不論伺服器目前的登入安全性模式為何，SQL Server 都會透過此資料來源，使用整合式登入安全性來建立連接。 所有提供的登入識別碼或密碼都會被忽略。 SQL Server 系統管理員必須具有相關聯您的 Windows 登入與 SQL Server 登入識別碼 （例如，藉由使用 SQL Server Management Studio）。

(選擇性) 您可以指定伺服器的服務主體名稱 (SPN)。

### <a name="with-active-directory-integrated-authentication"></a>使用 Active Directory 整合式驗證

指定驅動程式會向使用 Azure Active Directory 的 SQL Server。 選取之後，不論伺服器目前的登入安全性模式為何，SQL Server 都會透過此資料來源，使用 Azure Active Directory 整合式登入安全性來建立連接。

### <a name="with-sql-server-authentication"></a>使用 SQL Server 驗證

指定驅動程式會向 SQL Server 使用的登入識別碼和密碼。

### <a name="with-active-directory-password-authentication"></a>使用 Active Directory 密碼驗證

指定驅動程式會向使用 Azure Active Directory 登入識別碼和密碼的 SQL Server。

### <a name="with-active-directory-interactive-authentication"></a>使用 Active Directory 互動式驗證

指定驅動程式會向 SQL Server 使用 Azure Active Directory 互動模式，藉由提供登入識別碼。 這會觸發 Windows Azure 驗證提示對話方塊。

### <a name="login-id"></a>登入識別碼

指定當連接到 SQL Server 中，如果驅動程式會使用登入識別碼**與使用 SQL Server 驗證登入識別碼和使用者所輸入的密碼**或**與 Active Directory 密碼驗證登入識別碼和使用者所輸入的密碼**或是**使用登入識別碼與 Active Directory 互動式驗證使用者輸入**已選取。 這僅適用於用來決定伺服器預設值的連接，而不適用於建立此連接之後，使用資料來源所建立的後續連接。

### <a name="password"></a>[密碼]

指定當連接到 SQL Server 中，如果驅動程式會使用的密碼**與使用 SQL Server 驗證登入識別碼和使用者所輸入的密碼**或**與 Active Directory 密碼驗證登入識別碼與使用者所輸入的密碼**已選取。 這僅適用於用來決定伺服器預設值的連接，而不適用於使用新的資料來源建立的後續連接。

這兩個**登入識別碼**並**密碼**方塊會停用，如果**使用整合式 Windows 驗證**或**與 Active Directory 整合式驗證**已選取。

### <a name="next"></a>下一個

繼續進行精靈的下一個畫面。

### <a name="back"></a>上一頁

若要返回精靈的前一個畫面。

## <a name="next-steps"></a>後續步驟

[資料來源精靈畫面 1](../../../connect/odbc/windows/dsn-wizard-1.md)

[資料來源精靈畫面 3](../../../connect/odbc/windows/dsn-wizard-3.md)

