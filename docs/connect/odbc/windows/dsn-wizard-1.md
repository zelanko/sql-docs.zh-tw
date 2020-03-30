---
title: 資料來源精靈畫面 1 (ODBC Driver for SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 09/27/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 76326eeb-1144-4b9f-85db-50524c655d30
author: MightyPen
ms.author: genemi
ms.openlocfilehash: f6edf465f5b853008c9bdc8c420f6e862e360593
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/29/2020
ms.locfileid: "67936607"
---
# <a name="data-source-wizard-screen-1"></a>資料來源精靈畫面 1

指定資料來源的名稱及描述，以及資料來源將連接之執行 SQL Server 的伺服器名稱。 
    
## <a name="options"></a>選項。

### <a name="name"></a>名稱

當 ODBC 應用程式要求連接到資料來源時所使用的資料來源名稱。 例如，Personnel。 資料來源名稱會顯示於 [ODBC 資料來源系統管理員] 對話方塊中。

### <a name="description"></a>描述

(選擇性) 資料來源的描述。 例如，「所有員工的雇用日期、薪資記錄以及目前的複查」。

### <a name="select-or-enter-a-server-name"></a>選取或輸入伺服器名稱

網路上 SQL Server 執行個體的名稱。 您必須在下一個編輯方塊中指定伺服器。

在大多數情況下，ODBC 驅動程式都可以使用預設通訊協定順序及此方塊中提供的伺服器名稱進行連接。 如果您要為伺服器建立別名或設定用戶端網路程式庫，請使用 SQL Server 設定管理員。

如果您使用的電腦與 SQL Server 的相同，則您可以在伺服器方塊中輸入 "(local)"。 接著，即使執行的是非網路版的 SQL Server，使用者也可連接到 SQL Server 的本機執行個體。 多個 SQL Server 執行個體可以在同一部電腦上執行。 若要指定 SQL Server 的具名執行個體，請將伺服器名稱指定為 _ServerName_\\_InstanceName_。

如需不同網路類型伺服器名稱的詳細資訊，請參閱《SQL Server 線上叢書》中的 SQL Server 安裝文件。

### <a name="finish"></a>[完成]

如果在此畫面上指定的資訊即為連接到 SQL Server 所需全部資訊，可按一下 [完成]。  在精靈其他螢幕上指定的所有屬性都使用預設值。

### <a name="next"></a>下一頁

若要繼續前往精靈的下一個畫面，按一下 [下一頁]  。

## <a name="next-steps"></a>後續步驟

[資料來源精靈畫面 2](../../../connect/odbc/windows/dsn-wizard-2.md)
