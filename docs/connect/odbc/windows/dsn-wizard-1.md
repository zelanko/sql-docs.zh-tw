---
title: "資料來源精靈 畫面 1 (ODBC Driver for SQL Server) |Microsoft 文件"
ms.custom: 
ms.date: 09/27/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: odbc
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 76326eeb-1144-4b9f-85db-50524c655d30
caps.latest.revision: "22"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 83474fa2c3acef62e015c62abff7ed17445a0389
ms.sourcegitcommit: 2713f8e7b504101f9298a0706bacd84bf2eaa174
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/18/2017
---
# <a name="data-source-wizard-screen-1"></a>資料來源精靈 畫面 1

指定名稱和描述的資料來源，並執行 SQL Server 資料來源將連接的伺服器名稱。 
    
## <a name="options"></a>選項。

### <a name="name"></a>名稱

當 ODBC 應用程式要求連接到資料來源時所使用的資料來源名稱。 例如，Personnel。 資料來源名稱會顯示於 [ODBC 資料來源系統管理員] 對話方塊中。

### <a name="description"></a>Description

(選擇性) 資料來源的描述。 例如，「所有員工的雇用日期、薪資記錄以及目前的複查」。

### <a name="select-or-enter-a-server-name"></a>選取或輸入伺服器名稱

您的網路上的 SQL Server 執行個體名稱。 您必須在下一個編輯方塊中指定伺服器。

在大部分情況下，ODBC 驅動程式可以使用預設通訊協定順序及此方塊中提供的伺服器名稱連接。 如果您想要建立伺服器別名或設定用戶端網路程式庫，請使用 SQL Server 組態管理員。

您可以輸入"(local)"在伺服器中使用相同的電腦與 SQL Server 時。 使用者可以連接到 SQL Server，即使當執行是非網路版的 SQL Server 本機執行個體。 多個 SQL Server 執行個體可以在相同電腦上執行。 若要指定 SQL Server 的具名執行個體，伺服器名稱指定為_ServerName_\\_InstanceName_。

如需有關不同網路類型的伺服器名稱的詳細資訊，請參閱 SQL Server 線上叢書 》 中的 SQL Server 安裝文件。

### <a name="finish"></a>完成

如果在這個畫面上指定的資訊所需要的是連接到 SQL Server，您可以按一下**完成**。 在精靈其他螢幕上指定的所有屬性都使用預設值。

### <a name="next"></a>下一個

若要繼續進行精靈的下一個畫面，按一下**下一步**。

## <a name="next-steps"></a>後續的步驟

[資料來源精靈螢幕 2](../../../connect/odbc/windows/dsn-wizard-2.md)
