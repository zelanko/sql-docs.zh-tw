---
description: Oracle 連線管理員
title: Oracle 連線管理員 | Microsoft Docs
ms.custom: ''
ms.date: 08/14/2019
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 428ca450371e452081d548a64e26dba2bd29b3b5
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88430740"
---
# <a name="oracle-connection-manager"></a>Oracle 連線管理員

[!INCLUDE[sqlserver-ssis](../../includes/applies-to-version/sqlserver-ssis.md)]

Oracle 連線管理員是用來讓套件從 Oracle Database 中擷取資料，並將資料載入 Oracle Database。

Oracle 連線管理員的 **ConnectionManagerType** 屬性會設定為 **ORACLE**。

## <a name="configuring-the-oracle-connection-manager"></a>設定 Oracle 連線管理員

Oracle 連線管理員設定變更將會在執行階段由 Integration Services 解析。 使用 [Oracle 連線管理員編輯器]**** 對話方塊，將連線加入 Oracle 資料來源。

![連線管理員](media/oracle-connection-manager.png)

### <a name="options"></a>選項。

#### <a name="connection-manager-information"></a>連線管理員資訊

輸入有關 Oracle 連線的資訊。

**名稱**

輸入 Oracle 連線的名稱。 預設名稱為「Oracle 連線管理員」。 

**說明** 

輸入連線的描述。 這是選擇性的輸入。

**TNS 服務名稱**

輸入您要使用之 Oracle 資料庫的名稱。 TNS 服務名稱可能是：

- tnsnames.ora 檔案中所定義的連接描述元名稱，該檔案位於 Oracle 用戶端的 admin 資料夾中。

- EzConnect 格式：[//]host[:port][/service_name]

如需詳細資訊，請參閱 Oracle 文件集。

#### <a name="connection-manager-logging"></a>連線管理員記錄

選取下列其中一個選項：

- **使用 Windows 驗證**：選取此選項以使用 Windows 驗證。

- **使用 Oracle 驗證**：選取此選項以使用 Oracle 資料庫驗證。 如果您使用此驗證，請輸入您的 Oracle 認證，如下所示：  
    **使用者名稱**：輸入用來連線到 Oracle 資料庫的使用者名稱。  
    **密碼**：針對 [使用者名稱] 欄位中輸入的使用者，輸入 Oracle 資料庫密碼。

> [!NOTE]
>
>Oracle Server 18c 不支援使用 Windows 驗證。

**測試連接**

按一下 [測試連線]****，以確認提供的資訊是否正確。 如果輸入的資訊可以連線到 Oracle 資料庫，您就會收到「測試連接成功」**** 訊息。

### <a name="custom-properties"></a>自訂屬性

Oracle 連線管理員中有下列自訂連線管理員屬性：

- **EnableDetailedTracing**：未使用。

- **OracleHome**：指定連接器要使用的 32 位元 Oracle Home 名稱或資料夾。 (選用)

- **OracleHome64**：以 64 位元模式執行時，指定連接器要使用的 64 位元 Oracle Home 名稱或資料夾。 (選用)

自訂屬性不會列在 [Oracle 連線管理員編輯器] 中。 若要設定 **OracleHome** 與 **OracleHome64** 屬性：

1. 在 [連線管理員] 區域中，以滑鼠右鍵按一下您要使用的 Oracle 連線管理員，然後選取 [屬性]****。

2. 在 [屬性]**** 窗格中，將 **OracleHome** 或 **OracleHome64** 屬性設定為 Oracle 主目錄的完整路徑。

## <a name="next-steps"></a>後續步驟

- 設定 [Oracle 來源](oracle-source.md)。
- 設定 [Oracle 目的地](oracle-destination.md)。
- 如有任何疑問，請瀏覽 [TechCommunity](https://aka.ms/AA5u35j) \(英文\)。
