---
title: 資料來源精靈螢幕 2 (ODBC Driver for SQL Server) |Microsoft 文件
ms.custom: ''
ms.date: 03/21/2018
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 76326eeb-1144-4b9f-85db-50524c655d30
caps.latest.revision: 22
author: MightyPen
ms.author: v-jizho2
manager: craigg
ms.openlocfilehash: 96907675f7bdb1072923da9ad56412dd7dcd59c4
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="data-source-wizard-screen-2"></a>資料來源精靈螢幕 2

指定的驗證方法，並設定 Microsoft SQL Server 進階用戶端項目以及登入和密碼的 ODBC driver for SQL Server 將用來連接到 SQL Server 時設定資料來源。

## <a name="options"></a>選項

### <a name="with-integrated-windows-authentication"></a>使用整合式的 Windows 驗證

指定驅動程式要求 SQL Server 的安全 （或信任） 連接。 選取之後，不論伺服器目前的登入安全性模式為何，SQL Server 都會透過此資料來源，使用整合式登入安全性來建立連接。 所有提供的登入識別碼或密碼都會被忽略。 SQL Server 系統管理員必須有關聯的 Windows 登入與 SQL Server 登入識別碼 （例如，透過使用 SQL Server Management Studio）。

(選擇性) 您可以指定伺服器的服務主體名稱 (SPN)。

### <a name="with-active-directory-integrated-authentication"></a>使用 Active Directory 整合式驗證

指定驅動程式會向使用 Azure Active Directory 的 SQL Server。 選取時，SQL Server 會使用 Azure Active Directory 整合式登入安全性來建立連接，透過此資料來源，不論伺服器上目前的登入安全性模式為何。

### <a name="with-sql-server-authentication"></a>使用 SQL Server 驗證

指定驅動程式會向 SQL Server 使用的登入識別碼和密碼。

### <a name="with-active-directory-password-authentication"></a>使用 Active Directory 密碼驗證

指定驅動程式會向使用 Azure Active Directory 登入識別碼和密碼的 SQL Server。

### <a name="with-active-directory-interactive-authentication"></a>使用 Active Directory 互動式驗證

指定驅動程式會向使用 Azure Active Directory 互動模式，藉由提供登入識別碼。 SQL Server 這將會觸發 Windows Azure 驗證提示對話方塊。

### <a name="login-id"></a>登入識別碼

指定登入識別碼的驅動程式會使用連接到 SQL Server 時如果**與使用 SQL Server 驗證登入識別碼和使用者所輸入的密碼**或**使用登入識別碼與 Active Directory 密碼驗證和使用者所輸入的密碼**或**使用登入識別碼與 Active Directory 互動式驗證使用者輸入**已選取。 這僅適用於用來決定伺服器預設值的連接，而不適用於建立此連接之後，使用資料來源所建立的後續連接。

### <a name="password"></a>密碼

指定驅動程式會使用連接到 SQL Server 時如果密碼**與使用 SQL Server 驗證登入識別碼和使用者所輸入的密碼**或**使用登入識別碼與 Active Directory 密碼驗證和使用者所輸入的密碼**已選取。 這僅適用於用來決定伺服器預設值的連接，而不適用於使用新的資料來源建立的後續連接。

這兩個**登入識別碼**和**密碼**方塊會停用**的整合式 Windows 驗證**或**與 Active Directory 整合驗證**已選取。

### <a name="next"></a>下一個

繼續進行精靈的下一個畫面。

### <a name="back"></a>上一頁

傳回上一個精靈的螢幕。

## <a name="next-steps"></a>後續的步驟

[資料來源精靈 畫面 1](../../../connect/odbc/windows/dsn-wizard-1.md)

[資料來源精靈畫面 3](../../../connect/odbc/windows/dsn-wizard-3.md)

