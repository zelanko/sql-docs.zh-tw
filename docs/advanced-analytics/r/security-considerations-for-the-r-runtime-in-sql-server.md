---
title: "SQL Server 中的機器學習的安全性考量 |Microsoft 文件"
ms.custom:
- SQL2016_New_Updated
ms.date: 07/31/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- r-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: d5065197-69e6-4fce-9654-00acaecc148b
caps.latest.revision: 15
author: jeannt
ms.author: jeannt
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: d9b5fba856cc40c11f218faf0a61f66ee5451aa4
ms.contentlocale: zh-tw
ms.lasthandoff: 09/01/2017

---
# <a name="security-considerations-for-machine-learning-in-sql-server"></a>SQL Server 中的機器學習的安全性考量

本文列出的系統管理員或架構設計人員應該牢記使用機器學習服務時的安全性考量。

**適用於：** SQL Server 2016 R Services、 SQL Server 2017 機器學習服務

## <a name="use-a-firewall-to-restrict-network-access-by-r"></a>使用防火牆來限制 R 的網路存取

在預設安裝中，Windows 防火牆規則用來封鎖從 R 執行階段處理序的所有輸出網路存取。 您應該建立防火牆規則，以防止 R 執行階段處理序下載封裝或進行其他可能是惡意的網路呼叫。

如果您使用其他防火牆程式，您也可以設定本機使用者帳戶或使用者帳戶集區所代表群組的規則，以建立規則來封鎖 R 執行階段傳出的網路連接。

我們強烈建議您開啟 Windows 防火牆 （或您選擇的其他防火牆） 來防止多的網路存取的 R 或 Python 執行階段。

## <a name="authentication-methods-supported-for-remote-compute-contexts"></a>遠端計算內容所支援的驗證方法

[!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)]建立之間的連線時，支援 Windows 整合式驗證和 SQL 登入[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]和遠端資料科學用戶端。

例如，如果您是在膝上型電腦上開發 R 解決方案，並且想在 SQL Server 電腦上執行計算，則您可以使用 **rx** 函數並根據您的 Windows 認證定義連接字串，以使用 R 建立 SQL Server 資料來源。

當您變更_計算內容_從膝上型電腦到 SQL Server 電腦，如果您的 Windows 帳戶具有必要的權限，所有的 R 程式碼會執行 SQL Server 電腦上。 此外，以及您的認證下執行的 R 程式碼的一部分時執行了任何 SQL 查詢。

使用 SQL 登入也支援在此案例中，這需要 SQL Server 執行個體設定為允許混合的模式驗證。

### <a name="implied-authentication"></a>隱含驗證

 一般情況下，[!INCLUDE[rsql_launchpad](../../includes/rsql-launchpad-md.md)]啟動外部指令碼執行階段，並執行它自己的帳戶下的指令碼。 不過，如果外部執行階段會 ODBC 呼叫，[!INCLUDE[rsql_launchpad](../../includes/rsql-launchpad-md.md)]模擬傳送命令，以確保 ODBC 呼叫不會失敗的使用者認證。 這稱為「隱含驗證」。
 
 > [!IMPORTANT]
 >
 > 為了使隱含驗證成功，包含背景工作帳戶的 Windows 使用者群組 (預設為 **SQLRUser**)，必須有該執行個體之 master 資料庫中的帳戶，且此帳戶必須具有連線到該執行個體的權限。
 > 
 > 群組**SQLRUser**也會使用執行 Python 指令碼時。 

## <a name="no-support-for-encryption-at-rest"></a>不支援靜態加密

資料傳送或接收來自外部指令碼執行階段不支援透明資料加密。 因此，靜態加密**不**套用任何您使用 R 或 Python 指令碼中，儲存到磁碟或任何持續性的中繼結果的任何資料的資料。

## <a name="resources"></a>資源

如需有關管理服務，以及如何佈建用來執行 R 指令碼的使用者帳戶的詳細資訊，請參閱[設定及管理進階分析擴充功能](../../advanced-analytics/r/configure-and-manage-advanced-analytics-extensions.md)。

如需安全性架構的說明，請參閱：

+ [R 的安全性概觀](security-overview-sql-server-r.md)
+ [Python 的安全性概觀](../python/security-overview-sql-server-python-services.md)
