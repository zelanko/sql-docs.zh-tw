---
title: SQL Server 中的 R 語言支援的架構概觀 |Microsoft 文件
ms.prod: sql
ms.technology: machine-learning
ms.date: 04/15/2018
ms.topic: conceptual
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: 3784fe62669b3f6d29e94bea799e19f9eadad5f0
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/16/2018
---
# <a name="architecture-overview-for-r-in-sql-server"></a>SQL Server 中 R 的架構概觀
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

本章節提供 SQL Server 2016 R Services 和 SQL Server 2017 機器學習服務架構的概觀。

擴充性架構的架構是相同或非常類似的 SQL Server 2016 和 SQL Server 2017 版本，也類似 R 和 Python。 不過，為了簡化的討論，本文將討論只 R 元件，包括支援外部指令碼執行、 安全性、 R 程式庫和互通性開放原始碼 r 與 SQL Server database engine 中所加入的新元件

每個區段的連結中提供其他詳細資料。

## <a name="r-interoperability"></a>R 互通性

SQL Server 2016 R Services 和 SQL Server 2017 機器學習服務 （資料庫） 安裝 R，以及 Microsoft 所提供的封裝，支援分散式和/或平行處理的開放原始碼散發。

架構是設計成使用 R 的外部指令碼在不同的處理序中執行從 SQL Server。 目前的 R 使用者只要透過小幅度的修改，應該就能移植他們的 R 程式碼並在 T-SQL 中執行它。

若要調整您的方案，或使用平行處理，我們建議您使用[RevoScaleR](https://docs.microsoft.com/r-server/r-reference/revoscaler/revoscaler)封裝或[MicrosoftML](https://docs.microsoft.com/r-server/r-reference/microsoftml/microsoftml-package)封裝。 如果您不使用這些程式庫所提供的分散式運算能力，可以仍可使用一些效能改進 SQL Server 的內容中執行 R 程式碼。

如需有關已安裝的外部指令碼元件或互動的 R 與 SQL Server 的詳細資訊，請參閱[R 互通性](../../advanced-analytics/r/r-interoperability-in-sql-server.md)

## <a name="components-to-support-r-integration"></a>若要支援的 R 整合的元件

SQL Server 2017 中繼續 SQL Server 2016 所導入的擴充性架構。 SQL Server 所用的擴充性元件來啟動 R、 R 和 database engine 之間傳遞資料，並協調 R 作業所需的平行工作的外部執行階段。

這些其他元件的角色是要提升資料交換速度和壓縮，同時提供安全且高效能的平台執行外部指令碼。

如需詳細說明的元件，例如支援 R，[!INCLUDE[rsql_launchpad_md](../../includes/rsql-launchpad-md.md)]和 RLauncher，請參閱[新元件](../../advanced-analytics/r/new-components-in-sql-server-to-support-r.md)。

## <a name="security"></a>Security

當您執行使用機器學習服務或 SQL Server R 服務的 R 程式碼時，在 SQL Server 處理序，以提供安全性和更高的管理性之外執行所有的 R 指令碼。 這種隔離的處理序會保存 true，不論是否隨預存程序中，執行 R 指令碼或從遠端電腦連線到 SQL Server 電腦作業並啟動工作，當成計算內容會使用伺服器。

SQL Server 會攔截所有的工作要求、 工作和使用 Windows 工作物件，其資料保護和維護安全性，透過使用 SQL Server 使用者帳戶和資料庫角色的資料。

藉由強制執行 SQL Server 資料表、 資料庫和執行個體層級的安全性相容性界限內保留資料。 資料庫管理員可以控制誰執行 R 工作的能力，以及誰可以安裝或共用的 R 封裝的能力。 系統管理員也可以監視使用 R 指令碼，遠端或本機使用者和監視和管理所使用的資源。

## <a name="next-steps"></a>後續的步驟

[支援 R 整合的元件](new-components-in-sql-server-to-support-r.md)

[R 互通性](r-interoperability-in-sql-server.md)

[安全性概觀](security-overview-sql-server-r.md)
