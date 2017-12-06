---
title: "SQL Server 中的機器學習的安全性考量 |Microsoft 文件"
ms.date: 11/16/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology: r-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: d5065197-69e6-4fce-9654-00acaecc148b
caps.latest.revision: "15"
author: jeannt
ms.author: jeannt
manager: cgronlund
ms.workload: Inactive
ms.openlocfilehash: a32980d02215435e5bbcc3a2ca0f95b3f57f8d14
ms.sourcegitcommit: 531d0245f4b2730fad623a7aa61df1422c255edc
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/01/2017
---
# <a name="security-considerations-for-machine-learning-in-sql-server"></a>SQL Server 中的機器學習的安全性考量

本文列出的系統管理員或架構設計人員應該牢記使用機器學習服務時的安全性考量。

**適用於：** SQL Server 2016 R Services、 SQL Server 2017 機器學習服務

## <a name="use-a-firewall-to-restrict-network-access"></a>使用防火牆來限制網路存取

在預設安裝中，Windows 防火牆規則會封鎖來自外部執行階段處理序的所有輸出網路存取權。 應該建立防火牆規則，以防止外部執行階段處理序下載封裝或進行其他可能是惡意的網路呼叫。

如果您使用其他防火牆程式，您也可以建立規則來封鎖傳出的網路連接的外部執行階段，藉由設定規則的本機使用者帳戶或使用者帳戶集區所代表的群組。

我們強烈建議您開啟 Windows 防火牆 （或您選擇的其他防火牆） 的 R 或 Python 執行階段，防止不受限制的網路存取。

## <a name="authentication-methods-supported-for-remote-compute-contexts"></a>遠端計算內容所支援的驗證方法

[!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)]建立之間的連線時，支援 Windows 整合式驗證和 SQL 登入[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]和遠端資料科學用戶端。

例如，假設您在您的膝上型電腦上開發 R 解決方案，而且想要 SQL Server 電腦上執行計算。 您也會使用時，建立 SQL Server 資料來源**rx**函式和定義連接字串取決於您的 Windows 認證。

當您變更_計算內容_從膝上型電腦到 SQL Server 電腦，所有的 R 程式碼執行的 SQL Server 電腦上，如果您的 Windows 帳戶具有必要的權限。 此外，以及您的認證下執行的 R 程式碼的一部分時執行了任何 SQL 查詢。

在此案例中也支援使用 SQL 登入。 不過，這需要 SQL Server 執行個體設定為允許混合的模式驗證。

### <a name="implied-authentication"></a>隱含驗證

 一般情況下，[!INCLUDE[rsql_launchpad](../../includes/rsql-launchpad-md.md)]啟動外部指令碼執行階段，並執行它自己的帳戶下的指令碼。 不過，如果外部執行階段會 ODBC 呼叫，[!INCLUDE[rsql_launchpad](../../includes/rsql-launchpad-md.md)]模擬傳送命令，以確保 ODBC 呼叫不會失敗的使用者認證。 這稱為「隱含驗證」。
 
 > [!IMPORTANT]
 > 為了使隱含驗證成功，包含背景工作帳戶的 Windows 使用者群組 (預設為 **SQLRUser**)，必須有該執行個體之 master 資料庫中的帳戶，且此帳戶必須具有連線到該執行個體的權限。
 > 
 > 群組**SQLRUser**也會使用執行 Python 指令碼時。 

一般情況下，我們建議您事先，移至 SQL Server 的較大的資料集，而不要試著使用 RODBC 或另一個文件庫讀取資料。 此外，使用 SQL Server 查詢或檢視表做為主要資料來源，以提升效能。 

例如，您可能會從 SQL Server 取得定型資料 （通常的最大的資料），並從外部來源取得的因素清單。 您可以定義連結的伺服器從大部分的 ODBC 資料來源取得資料。 如需詳細資訊，請參閱[建立連結的伺服器](https://docs.microsoft.com/sql/relational-databases/linked-servers/create-linked-servers-sql-server-database-engine)。

ODBC 呼叫外部資料來源上的相依性降到最低，您可能也執行資料工程當做個別處理序，並將結果儲存在資料表中，或使用 T-SQL。 請參閱本教學課程中的資料在 SQL vs 中的工程團隊的理想範例。:[建立資料的功能使用 T-SQL](../tutorials/sqldev-create-data-features-using-t-sql.md)。

## <a name="no-support-for-encryption-at-rest"></a>不支援靜態加密

[透明資料加密 (TDE)](https://docs.microsoft.com/sql/relational-databases/security/encryption/transparent-data-encryption)資料傳送或接收來自外部指令碼執行階段不支援。 原因是 SQL Server 處理序; 外部 R （或 Python） 執行因此，外部執行階段所用的資料不受 database engine 的加密功能。  這種行為並無不同，會從資料庫讀取資料，並會複製 SQL Server 電腦上執行的其他任何用戶端。

因此，TDE**不**套用到您在 R 或 Python 指令碼中使用的任何資料或儲存至磁碟，或任何持續性的中繼結果的任何資料。 不過，其他類型的加密，例如 Windows BitLocker 加密或第三方加密套用到檔案或資料夾層級，還是套用。

如果是[永遠加密](https://docs.microsoft.com/sql/relational-databases/security/encryption/overview-of-key-management-for-always-encrypted)，外部執行階段不需要加密金鑰的存取權，因此，無法傳送資料到指令碼。

## <a name="resources"></a>資源

如需有關管理服務，以及如何佈建用來執行機器學習指令碼的使用者帳戶的詳細資訊，請參閱[設定及管理進階分析擴充功能](../../advanced-analytics/r/configure-and-manage-advanced-analytics-extensions.md)。

如需一般安全性架構的說明，請參閱：

+ [R 的安全性概觀](security-overview-sql-server-r.md)
+ [Python 的安全性概觀](../python/security-overview-sql-server-python-services.md)
