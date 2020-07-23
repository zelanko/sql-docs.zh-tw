---
title: 使用 Teradata 連線管理員 |Microsoft Docs
ms.custom: ''
ms.date: 11/22/2019
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
author: chugugrace
ms.author: chugu
ms.openlocfilehash: a0aa51c868ae89062320640015ad01ef79134e8d
ms.sourcegitcommit: c8e1553ff3fdf295e8dc6ce30d1c454d6fde8088
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/22/2020
ms.locfileid: "86917754"
---
# <a name="use-the-teradata-connection-manager"></a>使用 Teradata 連線管理員

[!INCLUDE[sqlserver-ssis](../../includes/applies-to-version/sqlserver-ssis.md)]

使用 Teradata 連線管理員，您可以讓套件從 Teradata 資料庫中擷取資料，並將資料載入 Teradata 資料庫。

您將 Teradata 連線管理員 `ConnectionManagerType` 屬性設定為 *TERADATA*。

## <a name="configure-the-teradata-connection-manager"></a>設定 Teradata 連線管理員

連線管理員設定變更將會在執行階段由 Integration Services 解析。 若要加入 Teradata 資料來源的連線，請完成 [Teradata 連線管理員編輯器]  窗格中的資訊。

![[Teradata 連線管理員編輯器] 窗格](media/teradata-connection-manager.png)

1. 在 [名稱]  方塊中輸入連線的名稱。 預設名稱為 **Teradata 連線管理員**。

1. (選擇性) 在 [描述]  方塊中，輸入連線的描述。

1. 在 [伺服器名稱]  方塊中，輸入要連線的 Teradata 伺服器名稱。

1. 在 [驗證]  下，執行下列其中一項動作：

   - 若要使用 Windows 驗證，請選取 [使用 Windows 驗證]  。
   - 若要使用 Teradata 資料庫驗證，請選取 [使用 Teradata 驗證]  ，然後輸入下列認證來進行這種類型的驗證：
     - 在 [機制]  方塊中，輸入您要使用的安全性檢查機制。 有效的機制值包括 TD1、TD2、LDAP、KRB5、KRB5C、NTLM 和 NTLMC。
     - 在 [參數]  方塊中，輸入您所輸入的安全性檢查機制所需的參數類型。
     - 在 [使用者名稱]  方塊中，輸入您用來連線到 Teradata 資料庫的使用者名稱。  
     - 在 [密碼]  方塊中，輸入使用者的 Teradata 資料庫密碼。

1. (選擇性) 在 [預設資料庫]  下拉式清單中，選取要連線的 Teradata 資料庫。 如果此資料庫存取權限不正確，則會顯示錯誤，然後您可以手動輸入資料庫名稱。

1. (選擇性) 在 [帳戶]  方塊中，輸入對應使用者名稱的帳戶名稱。 如果此值是空的，則會使用資料庫的直屬擁有者帳戶。
1. 選取 [確定]  。

## <a name="custom-property"></a>自訂屬性

自訂屬性 `UseUTF8CharSet` 指定是否使用 UTF-8 字元集。 預設值為 *True*。

若要設定屬性：

1. 開啟 SQL Server Data Tools (SSDT)。
1. 在 [連線管理員]  區域中，以滑鼠右鍵按一下 [Teradata 連線管理員]  ，然後選取 [屬性]  。
1. 在 [屬性]  窗格中，針對 `UseUTF8CharSet` 屬性選取 [True]  或 [False]  。

## <a name="troubleshoot-the-teradata-connection-manager"></a>針對 Teradata 連線管理員進行疑難排解

若要記錄 Teradata 連線管理員對 Teradata 開放式資料庫連接 (ODBC) 驅動程式的呼叫，請在 Windows ODBC 資料來源管理員中啟用 Windows ODBC 追蹤。

## <a name="next-steps"></a>後續步驟

- 設定 [Teradata 來源](teradata-source.md)。
- 設定 [Teradata 目的地](teradata-destination.md)。
- 如有任何疑問，請瀏覽[技術社群](https://aka.ms/AA5u35j)。
