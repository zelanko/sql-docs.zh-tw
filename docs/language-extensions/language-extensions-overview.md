---
title: 什麼是 SQL Server 語言延伸模組？
titleSuffix: ''
description: 語言延伸模組是 SQL Server 的一個功能，用來執行外部程式碼。 SQL Server 支援 Java、Python 與 R。 藉由使用擴充性架構，即可在外部程式碼中使用關聯式資料。
author: dphansen
ms.author: davidph
ms.date: 11/06/2020
ms.topic: overview
ms.prod: sql
ms.technology: language-extensions
monikerRange: '>=sql-server-ver15||>=sql-server-linux-ver15'
ms.openlocfilehash: 7ee2efbd49ff1d04ae9ed2ffe442a2a9479e35cf
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/14/2020
ms.locfileid: "97471759"
---
# <a name="what-is-sql-server-language-extensions"></a>什麼是 SQL Server 語言延伸模組？
[!INCLUDE [SQL Server 2019 and later](../includes/applies-to-version/sqlserver2019.md)]

語言延伸模組是 SQL Server 的一個功能，用來執行外部程式碼。 關聯式資料可使用[擴充性架構](concepts/extensibility-framework.md)，用於外部程式碼中。 SQL Server 2019 支援 Java、Python 與 R 執行階段。

> [!NOTE]
> 若要在 SQL Server 中執行 Python 或 R，請參閱[機器學習服務](../machine-learning/sql-server-machine-learning-services.md)文件。 使用 SQL Server 2019 和更新版本，即可使用自訂的 Python 和 R 執行階段搭配語言延伸模組。 如需詳細資訊，請參閱如何安裝 [Python 自訂執行階段](../machine-learning/install/custom-runtime-python.md)與 [R 自訂執行階段](../machine-learning/install/custom-runtime-r.md)。

## <a name="what-you-can-do-with-language-extensions"></a>語言延伸模組的用途

語言延伸模組會使用[擴充性架構](concepts/extensibility-framework.md)來執行外部程式碼。 程式碼執行與核心引擎流程隔離，但與 SQL Server 查詢執行完全整合。 您可在資料來源執行程式碼，而不用在網路中提取資料。

外部語言是使用 [CREATE EXTERNAL LANGUAGE](../t-sql/statements/create-external-language-transact-sql.md) 定義的。 系統預存程序 [sp_execute_external_script](../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md) 用來當作執行程式碼的介面使用。

語言延伸模組提供多項優點：

+ 資料安全性。 讓外部語言執行更接近資料來源，可以避免不安全的資料移動。
+ 速度。 資料庫已針對集合型操作進行最佳化。 
+ 簡化部署和整合。 [!INCLUDE [ssNoVersion](../includes/ssnoversion-md.md)] 是許多其他資料管理工作和應用程式的作業中心點。 使用資料庫中的資料，可確保語言延伸模組使用最新且一致的資料。

## <a name="next-steps"></a>後續步驟

+ 安裝 [Windows 的 SQL Server 語言延伸模組](install/windows-java.md)或 [Linux 的 SQL Server 語言延伸模組](../linux/sql-server-linux-setup-language-extensions-java.md)
+ 安裝[適用於 SQL Server 的 Python 自訂執行階段](../machine-learning/install/custom-runtime-python.md)
+ 安裝[適用於 SQL Server 的 R 自訂執行階段](../machine-learning/install/custom-runtime-r.md)
+ 安裝[適用於 Java 的 Microsoft 擴充性 SDK](how-to/extensibility-sdk-java-sql-server.md)
